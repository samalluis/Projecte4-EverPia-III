# T05: Accés Remot – Connexió via SSH (Tasca Individual)

## Breu descripció

Comencem una de les tasques més crítiques per a la nostra operativa diària a la consultora: la **gestió remota segura**.  
Com sabeu, els servidors dels nostres clients (i els nostres propis servidors interns) no són al nostre costat; estan en **CPDs o al núvol**. L'accés físic és l'excepció, no la norma.

La nostra eina principal per a això és **SSH (Secure Shell)**, l’estàndard absolut de la indústria per administrar màquines —especialment Linux— de manera xifrada, segura i eficient.

---

## La teva missió: Crear la Base de Coneixement

La consultora està creixent, i aviat s’incorporaran **nous becaris** al vostre equip.  
No podem permetre’ns invertir temps formant-los des de zero en tasques bàsiques que tot tècnic hauria de dominar.

Per tant, la teva tasca és elaborar una **Prova de Concepte (PoC)** que servirà com a base per a la **documentació oficial interna** de l'empresa.

Has de crear les **guies d’ús internes** que rebrà qualsevol nou tècnic, explicant com connectar-se als nostres sistemes de manera segura via SSH.

---

## Objectiu de la Pràctica

Utilitzaràs màquines virtuals per documentar clarament el procés de connexió SSH:

### **1. Connexió des de clients Linux**
- Utilitzant la **terminal nativa**.
- Explicant:
  - Instal·lació del client SSH (si cal).
  - Sintaxi bàsica (`ssh usuari@ip`).
  - Gestió de claus pública/privada.
  - Configuració del fitxer `~/.ssh/config`.
  - Connexió amb port no estàndard.
  - Validació del fingerprint.
  - Problemes típics i solucions.

### **2. Connexió des de clients Windows**
- Utilitzant:
  - **Terminal moderna de Windows 10/11**
  - **PowerShell**
- Explicant:
  - Comprovar si SSH està instal·lat.
  - Generació de claus via `ssh-keygen`.
  - Copiar la clau pública al servidor (`scp` o manualment).
  - Connexió bàsica i avançada.
  - Ús de fitxer de configuració SSH a Windows.

Aquestes guies han de seguir els punts que s’indiquen al final del document **Pràctica SSH** disponible al Moodle.

Recorda:  
> **La guia ha de ser impecable**.  
> El pròxim tècnic que arribi dependrà directament de la teva feina per ser operatiu des del primer dia.

---

## Materials i links de suport

- **Moodle 0227 Serveis de Xarxa – UD4.AA2 Pràctica SSH**
- **Vídeo:** SSH amb clau pública/privada (link proporcionat al Moodle)

---

[Clicka aqui per anar a HOME](..)

[Click aqui per anar a la GUIA](Guia.md)
