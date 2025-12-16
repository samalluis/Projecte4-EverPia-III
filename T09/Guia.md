# Projecte04 – Servidor NFS

## Prova de concepte per a DevOptimize Solutions

---

## Introducció

DevOptimize Solutions és una startup de desenvolupament de programari que treballa exclusivament amb sistemes Linux. Actualment, cada desenvolupador treballa amb còpies locals del codi font i dels documents del projecte, fet que provoca problemes constants de versions, errors humans i una pèrdua important d’eficiència.

L’objectiu d’aquesta prova de concepte és implementar un **servidor de fitxers centralitzat mitjançant NFS (Network File System v3)**, mostrant tant el seu funcionament com les seves limitacions, ja que el client **no disposa d’autenticació centralitzada**.

Aquesta guia documenta pas a pas tot el procés d’instal·lació, configuració, proves i conclusions.

---

## Fase 1: Preparació de l’entorn

### 1.1 Infraestructura

S’han creat dues màquines virtuals:

* **Servidor NFS**: Ubuntu Server 24.04 LTS
* **Client NFS**: Zorin OS 18

Ambdues màquines disposen de:

* Una interfície **NAT** (accés a Internet)
* Una interfície **Només-amb-amfitrió** (comunicació entre servidor i client)

Durant la instal·lació d’Ubuntu Server s’ha activat el **servei SSH** per facilitar la gestió remota.

![as](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-16%20153909.png?raw=true)

![adsa](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-16%20154013.png?raw=true)

### 1.2 Actualització del sistema

A les dues màquines:

```bash
sudo apt update && sudo apt upgrade -y
```

### 1.3 Verificació de connectivitat

Des del client:

```bash
ping <IP_SERVIDOR_NFS>
```

Server al client:

![das](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-16%20154751.png?raw=true)

Client al server:

![das](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-16%20154805.png?raw=true)

La resposta correcta confirma la comunicació entre ambdues màquines.

---

## Fase 2: Preparació del servidor NFS

### 2.1 Creació de grups

```bash
sudo groupadd devs
sudo groupadd admins
```

![kjk](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20163059.png?raw=true)

### 2.2 Creació d’usuaris

```bash
sudo useradd -m -g devs dev01
sudo passwd dev01

sudo useradd -m -g admins admin01
sudo passwd admin01
```

![eee](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20163432.png?raw=true)

![eee](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20163531.png?raw=true)

![dsdsd](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-16%20155039.png?raw=true)

![asdadasd](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-09%20152257.png?raw=true)

### 2.3 Creació dels directoris NFS

```bash
sudo mkdir /srv/nfs
sudo mkdir /srv/nfs/dev_projects
sudo mkdir /srv/nfs/admin_tools
```

![qwer](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20163805.png?raw=true)

### 2.4 Assignació de permisos (punt clau)

Els directoris tindran **root com a propietari**, però el control real es delega mitjançant grups:

```bash
sudo chown root:devs /srv/nfs/dev_projects
sudo chmod 770 /srv/nfs/dev_projects

sudo chown root:admins /srv/nfs/admin_tools
sudo chmod 770 /srv/nfs/admin_tools
```

![qwert](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20164248.png?raw=true)

![rrtyu](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20164335.png?raw=true)

Fem una comprovacio amb la comanda:

````
ls -la /srv/nfs/
````

![asdad](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-09%20152338.png?raw=true)

### 2.5 Instal·lació del servidor NFS

```bash
sudo apt install nfs-kernel-server -y
```

![adfgh](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T09/img/Captura%20de%20pantalla%202025-12-02%20160326.png?raw=true)

---

## Fase 3: Exportació d’Administració – root_squash

### 3.1 Prova 1: Error comú (root_squash per defecte)

Editar `/etc/exports`:

```bash
sudo nano /etc/exports
```

Afegir:

```
/srv/nfs/admin_tools *(rw,sync)
```

Aplicar els canvis:

```bash
sudo exportfs -ra
```

#### Al client

Instal·lar NFS client:

```bash
sudo apt install nfs-common -y
```

Muntar el recurs:

```bash
sudo mkdir -p /mnt/admin_tools
sudo mount <IP_SERVIDOR>:/srv/nfs/admin_tools /mnt/admin_tools
```

Com a root, crear un fitxer:

```bash
touch /mnt/admin_tools/prova_root.txt
ls -l /mnt/admin_tools
```

**Resultat**: el fitxer apareix com a propietari `nobody:nogroup`.

#### Explicació tècnica

Per seguretat, NFS aplica **root_squash** per defecte, que transforma l’usuari root del client en un usuari sense privilegis al servidor.

---

### 3.2 Prova 2: Solució amb no_root_squash

Modificar `/etc/exports`:

```
/srv/nfs/admin_tools *(rw,sync,no_root_squash)
```

```bash
sudo exportfs -ra
```

Al client:

```bash
sudo umount /mnt/admin_tools
sudo mount <IP_SERVIDOR>:/srv/nfs/admin_tools /mnt/admin_tools
```

Crear un nou fitxer:

```bash
touch /mnt/admin_tools/prova_root2.txt
ls -l /mnt/admin_tools
```

**Resultat**: el fitxer és propietat de `root:admins`.

#### Explicació

Amb **no_root_squash**, el servidor confia plenament en el root del client, eliminant la protecció de seguretat.

---

## Fase 4: Exportació de Desenvolupament (rw vs ro)

Editar `/etc/exports`:

```
/srv/nfs/dev_projects 192.168.56.0/24(rw,sync)
/srv/nfs/dev_projects 192.168.56.100(ro,sync)
```

```bash
sudo exportfs -ra
```

### 4.1 Prova com a dev01 (IP amb rw)

```bash
sudo mkdir -p /mnt/dev_projects
sudo mount <IP_SERVIDOR>:/srv/nfs/dev_projects /mnt/dev_projects
su - dev01
touch /mnt/dev_projects/codi.c
```

**Resultat**: es pot escriure correctament.

### 4.2 Prova amb IP ro

Canviar IP del client a `192.168.56.100`.

```bash
touch /mnt/dev_projects/error.txt
```

**Resultat**: error de permís (només lectura).

### 4.3 Prova com a admin01

```bash
su - admin01
touch /mnt/dev_projects/admin.txt
```

**Resultat**: error, ja que admin01 no pertany al grup `devs`.

---

## Fase 5: Muntatge automàtic amb /etc/fstab

Editar `/etc/fstab` al client:

```bash
sudo nano /etc/fstab
```

Afegir:

```
<IP_SERVIDOR>:/srv/nfs/admin_tools /mnt/admin_tools nfs defaults 0 0
<IP_SERVIDOR>:/srv/nfs/dev_projects /mnt/dev_projects nfs defaults 0 0
```

Provar sense reiniciar:

```bash
sudo mount -a
```

Reiniciar el sistema i verificar:

```bash
mount | grep nfs
```

---

## Conclusions i recomanacions

Aquesta prova de concepte demostra que NFS és una solució ràpida i eficient per centralitzar fitxers en entorns Linux. No obstant això, també presenta limitacions importants:

* NFS **no autentica usuaris**, només confia en UID i GID
* L’opció `no_root_squash` és un **risc de seguretat greu**
* La gestió manual d’usuaris no escala

### Recomanacions futures

* Implementar **LDAP o FreeIPA** per a autenticació centralitzada
* Migrar a **NFSv4** amb control d’identitat i ACLs
* Valorar alternatives com **Samba amb AD** o **sistemes de control de versions (Git)** per al codi font
* Separar xarxes i aplicar firewall

En conclusió, la solució compleix els requisits actuals del client, però no és adequada per a un entorn de producció a mitjà o llarg termini sense millores de seguretat i gestió.
