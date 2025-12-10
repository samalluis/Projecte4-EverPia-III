# Guia pas a pas detallada: Projecte 04 – Servidor NFS  
**Client: DevOptimize Solutions**  
**Objectiu:** Implementar i demostrar un servidor NFSv3 amb control d’accés, mostrant tant els avantatges com les limitacions de seguretat.

### Fase 1: Preparació de l’entorn

1. **Crear dues màquines virtuals a VirtualBox/VMware**  
   - **Servidor:** Ubuntu Server 24.04 LTS  
     - 2 GB RAM, 2 nuclis, 20 GB disc  
     - Xarxa 1: NAT (per Internet)  
     - Xarxa 2: Només amfitrió (Host-Only) → IP estàtica 192.168.56.10/24  
   - **Client:** Zorin OS 18 (basat en Ubuntu 24.04)  
     - 2 GB RAM, 2 nuclis, 20 GB disc  
     - Xarxa 1: NAT  
     - Xarxa 2: Només amfitrió → IP estàtica 192.168.56.20/24 (per ara)  

2. **Instal·lació i configuració bàsica**  
   - Idioma: Espanyol (Espanya)  
   - Al servidor Ubuntu: marcar “OpenSSH server” durant la instal·lació.  
   - Actualitzar ambdues màquines:

```bash
sudo apt update && sudo apt upgrade -y
```

3. **Comprovar connectivitat**  
   Des del client:

```bash
ping 192.168.56.10
```

Des del servidor:

```bash
ping 192.168.56.20
```

### Fase 2: Preparació del servidor (Ubuntu 24.04)

1. **Creació de grups i usuaris**  
   (És important que els UID/GID coincideixin exactament amb els del client perquè els permisos funcionin correctament)

```bash
sudo groupadd -g 1001 devs
sudo groupadd -g 1002 admins

sudo useradd -u 1001 -g devs -m -s /bin/bash dev01
sudo passwd dev01

sudo useradd -u 1002 -g admins -m -s /bin/bash admin01
sudo passwd admin01
```

2. **Creació de directoris i permisos**  

```bash
sudo mkdir -p /srv/nfs/dev_projects
sudo mkdir -p /srv/nfs/admin_tools

# Propietari root, però grup corresponent i permisos adequats
sudo chown root:devs /srv/nfs/dev_projects
sudo chmod 2770 /srv/nfs/dev_projects   # SGID perquè els nous fitxers heretin el grup devs

sudo chown root:admins /srv/nfs/admin_tools
sudo chmod 2770 /srv/nfs/admin_tools
```

3. **Instal·lar paquets NFS**  

```bash
sudo apt install nfs-kernel-server -y
```

4. **Configurar /etc/exports (exportació inicial)**  
   Edita el fitxer:

```bash
sudo nano /etc/exports
```

Afegeix:

```text
/srv/nfs/dev_projects   192.168.56.0/24(rw,sync,no_subtree_check)
/srv/nfs/admin_tools    192.168.56.0/24(rw,sync,no_subtree_check)
```

5. **Aplicar canvis i iniciar servei**  

```bash
sudo exportfs -ra
sudo systemctl restart nfs-kernel-server
```

### Fase 3: El dilema del root_squash

1. **Prova 1 – Comportament per defecte (root_squash actiu)**  

   Al client (Zorin OS) instal·lar client NFS:

```bash
sudo apt install nfs-common -y
```

   Crear punt de muntatge i muntar:

```bash
sudo mkdir -p /mnt/admin_tools
sudo mount -t nfs 192.168.56.10:/srv/nfs/admin_tools /mnt/admin_tools
```

   Com a root al client, crear un fitxer:

```bash
sudo touch /mnt/admin_tools/prueba_root.txt
ls -l /mnt/admin_tools/prueba_root.txt
```

   **Resultat esperat:**  
   El fitxer apareix com a propietari **nobody:nogroup** (o 65534:65534).  
   **Explicació:** NFSv3 per defecte activa **root_squash**. L’usuari root del client es mapeja a l’usuari nobody del servidor, impedint que root pugui escriure com a root real.

2. **Prova 2 – Desactivar root_squash**  

   Al servidor, editar /etc/exports:

```text
/srv/nfs/admin_tools    192.168.56.0/24(rw,sync,no_subtree_check,no_root_squash)
```

   Aplicar:

```bash
sudo exportfs -ra
```

   Al client, desmuntar i tornar a muntar:

```bash
sudo umount /mnt/admin_tools
sudo mount -t nfs 192.168.56.10:/srv/nfs/admin_tools /mnt/admin_tools
```

   Crear de nou el fitxer:

```bash
sudo touch /mnt/admin_tools/prueba_root_nosquash.txt
ls -l /mnt/admin_tools/prueba_root_nosquash.txt
```

   **Resultat:** El fitxer és propietari **root:root**.  
   **Explicació:** Amb **no_root_squash**, l’usuari root del client es respecta com a root al servidor.

### Fase 4: Exportació amb permisos rw vs ro segons IP

1. **Modificar /etc/exports al servidor**  

```text
# Per a la xarxa completa (admins i devs) -> lectura i escriptura
/srv/nfs/dev_projects   192.168.56.0/24(rw,sync,no_subtree_check,no_root_squash)

/srv/nfs/dev_projects   192.168.56.100/32(ro,sync,no_subtree_check,no_root_squash)
# La segona línia té precedència per a l'IP 192.168.56.100
```

   Actualitzar:

```bash
sudo exportfs -ra
```

2. **Proves al client (IP 192.168.56.20)**  

```bash
sudo mkdir -p /mnt/dev_projects
sudo mount -t nfs 192.168.56.10:/srv/nfs/dev_projects /mnt/dev_projects
```

   Com a dev01:

```bash
sudo su - dev01
echo "Prova des de dev01" > /mnt/dev_projects/mi_proyecto.txt
ls -l /mnt/dev_projects/mi_proyecto.txt
# Ha de funcionar i ser propietari dev01:devs
```

   Com a admin01:

```bash
sudo su - admin01
echo "Prova des d'admin01" > /mnt/dev_projects/fallara.txt
# Ha de donar error: Permission denied
```

3. **Simular IP de consultor extern (192.168.56.100)**  
   Al client, canviar temporalment la IP de la interfície Host-Only:

```bash
sudo ip addr del 192.168.56.20/24 dev enp0s8
sudo ip addr add 192.168.56.100/24 dev enp0s8
```

   Tornar a muntar:

```bash
sudo umount /mnt/dev_projects
sudo mount -t nfs 192.168.56.10:/srv/nfs/dev_projects /mnt/dev_projects
```

   Com a dev01 intentar escriure → només lectura (ro).

   Restaurar IP original:

```bash
sudo ip addr del 192.168.56.100/24 dev enp0s8
sudo ip addr add 192.168.56.20/24 dev enp0s8
```

### Fase 5: Muntatge automàtic amb /etc/fstab

Al client (Zorin OS) editar /etc/fstab:

```bash
sudo nano /etc/fstab
```

Afegir al final:

```text
192.168.56.10:/srv/nfs/dev_projects   /mnt/dev_projects   nfs   rw,soft,intr,rsize=8192,wsize=8192,timeo=14,retrans=3   0 0
192.168.56.10:/srv/nfs/admin_tools    /mnt/admin_tools    nfs   rw,soft,intr,rsize=8192,wsize=8192,timeo=14,retrans=3   0 0
```

Provar sense reiniciar:

```bash
sudo mount -a
```

Reiniciar el client i comprovar:

```bash
df -h | grep nfs
```

### Conclusió i recomanacions per a DevOptimize Solutions

Aquesta prova de concepte ha demostrat que NFS és una solució ràpida, nativa i eficient per compartir fitxers en entorns Linux purs. Hem aconseguit:

- Control d’accés basat en grups i permisos del sistema de fitxers.
- Exportacions diferenciades per IP (rw vs ro).
- Gestió del comportament del root amb root_squash/no_root_squash.

No obstant això, la solució actual presenta **limitacions i riscos de seguretat importants**:

1. **Manca d’autenticació real** → Qualsevol màquina de la xarxa 192.168.56.0/24 pot accedir als recursos si coneix la IP del servidor.
2. **root_squash/no_root_squash** → Desactivar-lo és perillós en entorns productius perquè permet que un administrador maliciós d’una màquina client pugui escriure com a root al servidor.
3. **Coincidència manual d’UID/GID** → Si un nou usuari es crea en una màquina i no coincideix l’ID, els permisos fallen.
4. **Sense xifratge** → NFSv3 envia dades en clar; qualsevol pot interceptar el tràfic.

**Recomanacions per a una solució més segura i escalable:**

- Implementar **NFSv4** amb **Kerberos** per a autenticació real i xifratge.
- Utilitzar **LDAP o FreeIPA** com a servidor d’autenticació centralitzada perquè tots els usuaris i grups tinguin el mateix UID/GID a totes les màquines.
- Si no es vol Kerberos, almenys activar **NFSv4.2** amb **sec=sys** i **root_squash** activat, i restringir l’accés només a IPs concretes amb firewall (ufw o firewalld).
- Considerar alternatives més modernes com **CephFS**, **GlusterFS** o **Nextcloud** (amb autenticació) si el volum de dades o els requisits de seguretat creixen.
- Per a entorns professionals, migrar a **Git** (GitLab, GitHub Enterprise) per al codi font i **Nextcloud/ownCloud** per als documents, combinat amb backups automàtics.

Amb aquestes millores, DevOptimize Solutions podria passar d’una solució de prova de concepte a una infraestructura robusta, segura i fàcil de gestionar a llarg termini.

Aquesta guia inclou tots els passos, comandes i explicacions tècniques necessàries perquè qualsevol persona pugui reproduir el projecte exactament. Pots afegir les captures de pantalla corresponents als punts clau (ls -l, df -h, resultats de les proves de root_squash, etc.) per completar la documentació.
