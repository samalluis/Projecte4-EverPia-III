# GUIA TÈCNICA: Accés Remot via SSH (Client Windows)

**Departament:** IT - Muntatges i Serveis Tècnics SL  
**Autor:** [El teu Nom]  
**Data:** Novembre 2025  
**Objectiu:** Prova de Concepte (PoC) per a la formació de nous becaris en la connexió segura via SSH des d'entorns Windows.

---

## Prerequisits

*   **Servidor:** Màquina virtual amb Ubuntu Server (IP coneguda, ex: `192.168.1.XX`).
*   **Client:** Màquina física o virtual amb Windows 10/11.
*   **Software Client:** Windows PowerShell o Terminal (preinstal·lat), Wireshark (per l'anàlisi de trànsit).

---

## 1. Instal·lació del servei SSH al Servidor (Ubuntu)
*Nota: Aquest pas es realitza al servidor, però és indispensable per connectar-nos des de Windows.*

Per permetre connexions, assegura't que el servei està instal·lat i actiu a l'Ubuntu:

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl status ssh
````

![aaaaaaa](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T05/img/Captura%20de%20pantalla%202025-12-04%20171236.png?raw=true)

![adasdads](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T05/img/Captura%20de%20pantalla%202025-12-04%20171332.png?raw=true)

2. Primera connexió i validació del certificat
   
Des del client Windows, obre PowerShell o Windows Terminal. Utilitzarem la comanda nativa ssh.

Executa la comanda de connexió:

````PowerShell

ssh nom_usuari@192.168.1.XX
````

![lkkl](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T05/img/Captura%20de%20pantalla%202025-12-04%20172039.png?raw=true)

3. Gestió de l'usuari Root i configuració SSHD
   
Un cop connectats via SSH des del Windows, configurarem l'usuari root.

3.1. Habilitar l'usuari root

Per defecte, l'usuari root a Ubuntu no té contrasenya assignada.

````Bash
sudo passwd root
````

![ffdf](https://github.com/samalluis/Projecte4-EverPia-III/blob/main/T05/img/Captura%20de%20pantalla%202025-12-04%20172201.png?raw=true)

Introdueix la nova contrasenya per a root dues vegades.

3.2. Configuració sshd_config

Hem d'examinar la configuració del servei SSH per veure les polítiques d'accés.

````Bash
cat /etc/ssh/sshd_config | grep PermitRootLogin
````
Observarem una línia que diu #PermitRootLogin prohibit-password o similar. Això significa que, per defecte, root NO pot entrar amb contrasenya via SSH.

Evidència (Rúbrica): Captura mostrant el resultat del grep o el fitxer sshd_config.

3.3. Comprovació d'accés de Root

Tanca la sessió actual amb exit.

Des del PowerShell de Windows, intenta connectar-te com a root:

````PowerShell
ssh root@192.168.1.XX
````
Introdueix la contrasenya que has definit al punt 3.1.

Resultat esperat: Permission denied, please try again.

Opcional: Al servidor Ubuntu (físicament/consola virtual), entra com a usuari normal i fes su -. Veuràs que sí pots fer login local, demostrant que la restricció és només del servei SSH.

Evidència (Rúbrica): Captura del PowerShell mostrant l'error "Permission denied" intentant entrar com a root.

4. Transferència d'arxius (SCP)

Utilitzarem la comanda nativa scp de Windows per enviar un fitxer al servidor.

Al Windows, crea un fitxer de prova:

````PowerShell
echo "Aquest és un arxiu secret des de Windows" > C:\Users\Public\secret.txt
````

Envia l'arxiu a la carpeta personal de l'usuari Linux:

````PowerShell
scp C:\Users\Public\secret.txt nom_usuari@192.168.1.XX:/home/nom_usuari/
````

Verifica que s'ha enviat (connectant-te per SSH i fent un ls).
Evidència (Rúbrica): Captura de la comanda scp executant-se correctament al PowerShell amb la barra de progrés o el resultat final.

5. Túnel SSH (Port Forwarding)

Simularem que volem accedir a un servei web del servidor Linux que està tancat al públic, accedint-hi a través del túnel SSH.

Supòsit: El servidor té un servidor web (Apache/Nginx) al port 80. Si no en té, instal·la'l ràpidament amb sudo apt install apache2.

Des de Windows PowerShell, crea el túnel:

````PowerShell
# Sintaxi: ssh -L port_local:localhost:port_remot usuari@ip
ssh -L 8080:localhost:80 nom_usuari@192.168.1.XX
````
Deixa aquesta finestra oberta.

Obre el navegador web (Chrome/Edge) al Windows.

Ves a l'adreça: http://localhost:8080.

Hauries de veure la pàgina de benvinguda d'Apache de l'Ubuntu.

Evidència (Rúbrica): Captura del navegador mostrant la web de l'Ubuntu a l'adreça localhost:8080 i la finestra de PowerShell fent el túnel al costat.

6. Anàlisi de trànsit amb Wireshark

Per demostrar que el túnel xifra la informació:

Obre Wireshark al Windows.
Selecciona la interfície de xarxa activa (Ethernet o Wi-Fi).
Al filtre, escriu: tcp.port == 22. Inicia la captura.
Al navegador web (mentre el túnel del punt anterior està actiu), refresca la pàgina http://localhost:8080.
A Wireshark veuràs molts paquets. Si inspecciones el contingut (Follow TCP Stream), veuràs que tot és text inintel·ligible (xifrat). No veuràs codi HTML ni text pla, malgrat estar visitant una web HTTP.
Evidència (Rúbrica): Captura de Wireshark mostrant paquets del protocol SSHv2 amb el payload xifrat ("Encrypted packet").

7. Autenticació amb Claus Públiques (Certificats)
   
Per millorar la seguretat i no dependre de contrasenyes, configurarem l'accés mitjançant claus RSA.

7.1. Generació de claus al Windows

Al PowerShell:

````PowerShell
ssh-keygen -t rsa -b 4096
````
Prem "Enter" per acceptar la ruta per defecte (.ssh/id_rsa). Pots deixar la passphrase buida per aquest exemple.

7.2. Copiar la clau pública al servidor

Windows no sempre té la comanda ssh-copy-id per defecte. Ho farem manualment amb scp:

Pujar la clau pública:

````PowerShell
scp $env:USERPROFILE\.ssh\id_rsa.pub nom_usuari@192.168.1.XX:~/clau_windows.pub
````
Connectar-se via SSH i instal·lar la clau:
````PowerShell
ssh nom_usuari@192.168.1.XX
````

Un cop dins del Linux:

````
mkdir -p ~/.ssh
````
````
cat ~/clau_windows.pub >> ~/.ssh/authorized_keys
````
````
chmod 600 ~/.ssh/authorized_keys
````
````
rm ~/clau_windows.pub
````
````
exit
````

Evidència (Rúbrica): Captura del procés ssh-keygen i de la còpia de la clau.

7.3. Comprovació de funcionament

Ara, intenta connectar-te de nou des de Windows:

````PowerShell

ssh nom_usuari@192.168.1.XX
````

Resultat: Hauries d'entrar directament al servidor sense que et demani la contrasenya.

Evidència (Rúbrica): Captura mostrant el login automàtic sense prompt de password.
