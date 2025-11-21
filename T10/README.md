# T10: Servidor Impressió Linux – CUPS  
### Tasca Individual

## Breu Descripció

### Introducció
Molt bé, equip.

A la nostra consultora, **EverPia**, busquem optimitzar constantment els recursos dels clients per reduir costos i simplificar la gestió.  
Un dels punts més caòtics en qualsevol oficina és la **gestió d’impressores**:

- Drivers incompatibles  
- Costos de tòner descontrolats  
- Equips que no saben a quina impressora estan enviant la feina  

La solució professional és implementar un **Servidor d’Impressió Centralitzat**.

El client **DevOptimize Solutions** ha demanat una proposta per centralitzar la impressió en tots els seus departaments, que utilitzen una barreja de clients Linux (**Zorin OS**) i servidors (**Ubuntu Server**).

---

## La Vostra Missió: Prova de Concepte (PoC)

Abans de comprar impressores de xarxa cares, el client vol veure una **Prova de Concepte (PoC)** que demostri:

- Un servidor Linux pot gestionar una impressora  
- Compartir-la de manera transparent amb clients Zorin OS

Per simular la impressora sense hardware, utilitzarem **cups-pdf**, que actua com una impressora normal però genera **fitxers PDF** en lloc d’imprimir en paper.

L’objectiu és configurar aquest escenari i demostrar que un client pot enviar una feina d’impressió al servidor.

---

## Escenari de Treball

**Màquina 1 (Servidor):**  
- Ubuntu Server  
- Interfície NAT i una segona Host-Only

**Màquina 2 (Client):**  
- Zorin OS Desktop  
- Mateixa configuració de xarxa que el servidor

> Es pot utilitzar el mateix escenari de la PoC de NFS.

---

## PoC (Prova de Concepe)

1. Instal·lació de **CUPS** al servidor.  
2. Instal·lació de la **impressora virtual cups-pdf**.  
3. Configuració de l’administració de CUPS i permetre que **escolti per totes les interfícies**.  
4. Compartir la impressora utilitzant el **frontal web de CUPS**.  
5. Afegir la impressora al client Zorin OS.  
6. Fer una prova d’impressió amb diversos documents.  
7. Comprovar al servidor que s’han generat els **fitxers PDF** corresponents als treballs impresos.

> Documentar les comandes utilitzades, tal com s’ha explicat a la tasca PDF, i incorporar **captures de pantalla** que demostrin el correcte funcionament de la prova.

---

## Materials i Links de Suport

- **Material propi:** UD5. AA1. CUPS. Disponible al Moodle del mòdul de Sistemes Operatius en Xarxa.  
- J.B. Alex Mantich. (2024, 15 febrer). *Instalación de servidor de impresión en CUPS para Linux* [Vídeo]. YouTube  
  [https://www.youtube.com/watch?v=FNwSTrOSgZQ](https://www.youtube.com/watch?v=FNwSTrOSgZQ)  
- Canonical. *Network File System (NFS)* – Ubuntu Server Documentation  
  [https://documentation.ubuntu.com/server/how-to/networking/install-nfs/](https://documentation.ubuntu.com/server/how-to/networking/install-nfs/)  
- R00t. (2025, 25 abril). *How To Install CUPS Print Server on Ubuntu 24.04 LTS*. Idroot  
  [https://idroot.us/install-cups-print-server-ubuntu-24-04/](https://idroot.us/install-cups-print-server-ubuntu-24-04/)

