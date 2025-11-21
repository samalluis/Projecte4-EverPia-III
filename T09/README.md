# T09: Servidor Fitxers Linux – NFS  
### Tasca Individual

## Breu Descripció

### Introducció
Molt bé, equip de consultors júniors.

En el nostre projecte ens trobem amb un requisit tècnic molt habitual per part dels nostres clients: **centralitzar dades en entorns Linux**.

---

## El Cas Client: DevOptimize Solutions

El nostre client és **DevOptimize Solutions**, una petita startup de desenvolupament de programari que treballa exclusivament amb Linux.

Problema crític:

- El codi font i els actius (documents de disseny, scripts) estan descontrolats.  
- Cada desenvolupador té còpies locals, provocant errors de versió constants i **pèrdua d’eficiència**.

Solució proposada:

- Implementar un **servidor de fitxers centralitzat**.  
- Atès que tot l’entorn és Linux, la solució **nativa, ràpida i eficient** és **NFS (Network File System)**.

Nota del client:

- De moment, treballa **sense entorn d’autenticació centralitzada**.  
- No preveu fer aquest pas en un futur proper.

---

## Objectiu de la Tasca

Per mostrar al client com quedarà la solució i les seves limitacions, heu de:

1. Crear un **servidor NFS (NFSv3)**.  
2. Crear un **client Linux** que consumeixi els recursos compartits.  
3. Crear **usuaris i grups** per simular l’entorn del client.  
4. Demostrar el **control d’accés** utilitzant:  
   - Opcions d’exportació (`/etc/exports`)  
   - Permisos del sistema de fitxers (`chmod`, `chown`)  

> Repositori amb descripció completa de la tasca:  
> [Projecte04-NFS GitHub](https://github.com/SMX2n/Projecte04-NFS)

---

## Materials i Links de Suport

- **Material propi:** UD5. AA1. NFS. Disponible al Moodle del mòdul de Sistemes Operatius en Xarxa.  
- Ruiz, P. (2021, novembre 22). **NFS (parte 1): Instalación en un servidor Ubuntu 20.04 LTS**. SomeBooks.es  
  [https://somebooks.es/nfs-parte-1-instalacion-en-un-servidor-ubuntu-20-04-lts/](https://somebooks.es/nfs-parte-1-instalacion-en-un-servidor-ubuntu-20-04-lts/)  
- Ruiz, P. (2021, desembre 2). **NFS (parte 2): Instalación en un cliente Ubuntu 20.04 LTS**. SomeBooks.es  
  [https://somebooks.es/nfs-parte-2-instalacion-en-un-cliente-ubuntu-20-04-lts/](https://somebooks.es/nfs-parte-2-instalacion-en-un-cliente-ubuntu-20-04-lts/)  
- **Network File System (NFS)**. Ubuntu Server  
  [https://documentation.ubuntu.com/server/how-to/networking/install-nfs/](https://documentation.ubuntu.com/server/how-to/networking/install-nfs/)

