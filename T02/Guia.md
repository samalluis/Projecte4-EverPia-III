GUIA TÈCNICA: Implementació de Polítiques de Còpia de Seguretat
Client: Muntatges i Serveis Tècnics SL
Objectiu: Proves de concepte (PoC) per a entorns Windows i Linux.

PART 1: Còpia de seguretat en equips clients (Windows 11)
1. Preparació de l'entorn (Màquina Virtual)
Crea una Màquina Virtual (MV) amb Windows 11.
Afegeix un segon disc dur virtual de 10 GB a la configuració de la MV.
Inicia la MV.
Dins de Windows, ves a Gestor de discos (diskmgmt.msc).
Inicialitza el nou disc de 10 GB, crea un volum simple i assigna-li una lletra (per exemple, D:). Aquesta serà la unitat de còpia local.
2. Generació de dades de prova
Crea una carpeta de prova a Documents.
Genera arxius grans per simular dades reals. Obre el CMD (Símbol del sistema) com a administrador i usa fsutil (segons els recursos):
cmd

fsutil file createnew C:\Users\ElTeuUsuari\Documents\ArxiuImportant1.dat 104857600
(Això crea un arxiu de 100MB. Crea'n uns quants).
3. Instal·lació de Duplicati
Descarrega l'instal·lador des de duplicati.com.
Executa l'instal·lador i segueix els passos (Next > Next > Install).
Al finalitzar, s'obrirà el navegador web automàticament a http://localhost:8200. Si és el primer cop, et demanarà si vols posar contrasenya a la interfície (opcional per aquesta prova).
4. Configuració de la Còpia 1: Local (Cada hora)
Al menú de Duplicati, clica a "Add backup" > "Configure a new backup".
General:
Name: Còpia Local
Encryption: Pots deixar-lo en AES-256 o "No encryption" per la prova.
Destination:
Storage Type: Local folder or drive.
Folder path: Selecciona el disc D: (ex: D:\Backups\Local).
Source Data:
Selecciona la carpeta de l'usuari (especialment Documents).
Schedule (Horari):
Marca "Automatically run backups".
Run again every: 1 hour.
Options: Deixa per defecte i guarda (Save).
5. Configuració de la Còpia 2: Cloud (Google Drive - 18:00)
Afegeix una nova còpia ("Add backup").
General: Name: Còpia Cloud.
Destination:
Storage Type: Google Drive.
Path on server: Duplicati/Backups (o el nom que vulguis).
AuthID: Clica a l'enllaç blau que diu "AuthID". S'obrirà una finestra per iniciar sessió amb el compte de Google (el creat per a la prova). Accepta els permisos i copia el codi generat. Enganxa'l al camp AuthID de Duplicati.
Clica "Test connection" per verificar.
Source Data: Igual que abans (Documents).
Schedule:
Marca "Automatically run backups".
Next time: Posa la data d'avui a les 18:00.
Repeat: 1 Day.
Guarda la configuració.
6. Execució i Prova de Restauració
Executar: Força l'execució de les dues tasques clicant a "Run now" al costat de cada pla per tenir una primera còpia.
Simulació de desastre: Esborra tots els arxius de la carpeta Documents original.
Restauració Local:
A Duplicati, ves a Restore > Selecciona "Còpia Local".
Tria els arxius i clica "Continue".
Selecciona "Original location" i clica "Restore". Verifica que els arxius han tornat.
Restauració Cloud:
Torna a esborrar els arxius.
Ves a Restore > Selecciona "Còpia Cloud".
Segueix el mateix procés i verifica que es descarreguen del Google Drive.
PART 2: Còpia de seguretat Servidor Linux (Ubuntu Server)
1. Preparació de l'entorn (Discos i Sistema d'arxius)
Afegeix un disc de 10GB a la MV Ubuntu.
Identifica el disc (sol ser /dev/sdb):
Bash

lsblk
Crea la carpeta de muntatge:
Bash

sudo mkdir -p /media/backup
Formata el disc en XFS i munta'l manualment:
Bash

sudo apt update
sudo apt install xfsprogs -y
sudo mkfs.xfs /dev/sdb
sudo mount /dev/sdb /media/backup
2. Instal·lació de programari i creació d'usuaris
Instal·la Duplicity i dependències:
Bash

sudo apt install duplicity python3-boto -y
(Nota: ncftp solia ser necessari, però per còpia local no cal).
Crea usuaris i dades de prova:
Bash

# Crear usuaris
sudo adduser usuari1
sudo adduser usuari2

# Crear arxius grans de 10MB al teu home
dd if=/dev/zero of=~/arxiu1.img bs=1M count=10
dd if=/dev/zero of=~/arxiu2.img bs=1M count=10
dd if=/dev/zero of=~/arxiu3.img bs=1M count=10
dd if=/dev/zero of=~/arxiu4.img bs=1M count=10
3. Còpia Manual i Restauració
Còpia completa manual (Full):
Bash

# La unitat ha d'estar muntada
duplicity full /home file:///media/backup
Et demanarà una Passphrase. Posa una senzilla i recorda-la (ex: "muntatges").
Prova de desastre i Restore:
Bash

rm ~/arxiu*
ls -l ~  # Comprova que no hi ha res
duplicity restore file:///media/backup /home
# Et demanarà la Passphrase. Comprova que els arxius han tornat.
Còpia Incremental:
Bash

# Crea un arxiu nou de 4MB
dd if=/dev/zero of=~/arxiu_nou.img bs=1M count=4
# Fes backup (Duplicity detecta automàticament si pot fer incremental)
duplicity /home file:///media/backup
Desmuntar la unitat:
Bash

sudo umount /media/backup
4. Automatització amb Scripts i Cron
Ara crearem els scripts que munten el disc, fan la còpia i el desmunten.

Nota: Crea una carpeta per guardar els scripts, per exemple /root/scripts o a la teva home. Aquí assumiré /usr/local/bin per seguir bones pràctiques o la carpeta de l'usuari root. Fem-ho com a root.

Canvia a root: sudo -i

A. Script Full Backup (fullbackup.sh)
Crea l'arxiu: nano /root/fullbackup.sh

Bash

#!/bin/bash

# Variables
EXPORT PASSPHRASE="muntatges"
SOURCE="/home"
DEST="file:///media/backup"
DEVICE="/dev/sdb"
MOUNTPOINT="/media/backup"

# 1. Muntar la unitat
echo "Muntant unitat de backup..."
mount $DEVICE $MOUNTPOINT

# Comprovació si s'ha muntat bé
if mountpoint -q $MOUNTPOINT; then
    echo "Unitat muntada correctament."

    # 2. Executar Duplicity FULL
    echo "Iniciant còpia COMPLETA..."
    duplicity full $SOURCE $DEST

    # 3. Desmuntar la unitat
    echo "Desmuntant unitat..."
    umount $MOUNTPOINT
    echo "Còpia finalitzada."
else
    echo "Error: No s'ha pogut muntar la unitat."
fi
Dona permisos d'execució:

Bash

chmod +x /root/fullbackup.sh
B. Script Incremental Backup (incrementalbackup.sh)
Crea l'arxiu: nano /root/incrementalbackup.sh

Bash

#!/bin/bash

# Variables
EXPORT PASSPHRASE="muntatges"
SOURCE="/home"
DEST="file:///media/backup"
DEVICE="/dev/sdb"
MOUNTPOINT="/media/backup"

# 1. Muntar la unitat
echo "Muntant unitat de backup..."
mount $DEVICE $MOUNTPOINT

# Comprovació si s'ha muntat bé
if mountpoint -q $MOUNTPOINT; then
    echo "Unitat muntada correctament."

    # 2. Executar Duplicity INCREMENTAL
    # Si no posem 'full', duplicity intenta fer incremental per defecte si troba una còpia prèvia
    echo "Iniciant còpia INCREMENTAL..."
    duplicity incremental $SOURCE $DEST

    # 3. Desmuntar la unitat
    echo "Desmuntant unitat..."
    umount $MOUNTPOINT
    echo "Còpia finalitzada."
else
    echo "Error: No s'ha pogut muntar la unitat."
fi
Dona permisos d'execució:

Bash

chmod +x /root/incrementalbackup.sh
5. Programació amb Cron
Edita el crontab de l'usuari root:

Bash

crontab -e
Afegeix les línies següents al final del fitxer:

Bash

# Còpia COMPLETA: Diumenges (0) a les 23:00
0 23 * * 0 /root/fullbackup.sh >> /var/log/backup_full.log 2>&1

# Còpia INCREMENTAL: De Dilluns (1) a Dissabte (6) a les 23:00
0 23 * * 1-6 /root/incrementalbackup.sh >> /var/log/backup_inc.log 2>&1
(Nota: La part >> /var/log... és opcional però recomanable per veure si ha funcionat, ja que cron no té sortida per pantalla).

Guarda i surt.

6. Verificació Final
Per comprovar que els scripts funcionen sense esperar a les 23:00, pots executar-los manualment una vegada:

Bash

/root/incrementalbackup.sh
Si no dona error i en acabar fas un lsblk i veus que el disc sdb no té cap punt de muntatge (MOUNTPOINTS està buit), el sistema funciona tal com s'ha demanat (munta, copia, desmunta).






