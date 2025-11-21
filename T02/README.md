# T02: DPR: Còpies de Seguretat — Cas Pràctic

## Breu descripció

### Introducció al cas
A la tasca anterior heu dissenyat una política de còpies de seguretat pel nostre nou client **"Muntatges i Serveis Tècnics SL"**. Ara toca passar a l’acció i portar a la pràctica l’estudi anterior.  
El client demana que s’elaborin unes guies tècniques amb proves de concepte per tal que el seu personal estigui qualificat per implantar el pla de còpies de seguretat.

---

# Part 1: Còpia de seguretat dels equips clients Windows

Encara que en principi el DPR no contemplaria fer còpia dels arxius locals dels equips clients, se’ns demana fer una excepció amb l’equip Windows del director de l’empresa. En aquest equip es guarda informació important que **no es vol tenir accessible al servidor de fitxers de l’empresa**.

Per aquest motiu és necessari definir una política de còpies de seguretat seguint l’esquema **3-2-1**:

- Una còpia al disc secundari del propi equip.  
- Una segona còpia al **cloud (Google Drive)** utilitzant **Duplicati**.

## Entorn de prova

Com a prova de concepte:

- Crear una màquina virtual **Windows 11** amb **dos discs**:  
  - Disc principal amb el sistema operatiu  
  - Disc secundari de **10 GB** per a còpies  
- Per simular Google Drive, fer servir un **compte extern** (no el de l’escola).

## Requisits de còpia

- Còpia **cada hora** del perfil d’usuari al disc secundari.  
- Còpia **a les 18:00** a Google Drive.

## Tasques a documentar

1. Procediment d’instal·lació de **Duplicati**.  
2. Configuració dels plans de còpies.  
3. Afegir arxius a les carpetes de l’usuari (especialment *Documents*) per observar el funcionament.  
4. Esborrar el contingut de *Documents* i restaurar des del disc secundari.  
5. Comprovar la restauració des de la còpia emmagatzemada al cloud.

---

# Part 2: Còpia de seguretat servidor Linux

Per fer les còpies del servidor Linux, la solució proposada és **Duplicity**, que permet fer còpies tant a un mitjà local com remot.  
Amb **cron**, es poden implementar polítiques de còpia de manera automatitzada.

Has de crear una guia tècnica que expliqui com utilitzar aquesta eina per fer còpies d’un servidor Linux.

## Entorn de prova

- Màquina virtual amb **Ubuntu Server**.  
- Afegir un segon disc de **10 GB** que simularà una unitat auxiliar.

## Tasques a realitzar

1. Inicialitzar i formatar el disc en **XFS**.  
   - Muntar-lo manualment a `/media/backup` (cal crear la carpeta abans).
2. Instal·lar **Duplicity**.
3. Crear dos usuaris nous amb carpeta personal.  
   - Crear també **4 arxius de 10 MB** a la carpeta home del teu usuari.
4. Fer una còpia de seguretat de la carpeta `/home`.
5. Esborrar els arxius i fer una restauració per comprovar que es recuperen.
6. Afegir un nou arxiu de **4 MB** i fer una nova còpia.  
   - Observar com ara es crea una **còpia incremental**.
7. Desmuntar la unitat de backup.

---

# Automatització amb scripts i cron

És important que la **unitat de backup estigui desmuntada per defecte**.  
Els scripts han de muntar-la al principi i desmuntar-la al final.

## 7. Script `fullbackup.sh`

- Fa una còpia **completa** de `/home`.  
- Desa el backup al volum muntat.  
- Fa servir la variable d’entorn **PASSPHRASE** per no haver d’escriure la contrasenya:

```bash
export PASSPHRASE=contrasenya

