# T03: Pla de recuperació davant desastres: imatges del sistema

## Breu descripció

### Introducció al cas
Recordeu el cas del portàtil al qual no es podia accedir? En aquella situació, la vostra perícia tant a l’hora de recuperar l’accés com en la posterior fortificació del sistema va deixar impressionat al client. Per aquest motiu, ha requerit que participeu en el seu nou encàrrec.

Ha encarregat l’elaboració d’un **Pla de Contingència i Continuïtat del Negoci**. Dins d’aquest pla, s’ha de posar en marxa el **Pla de Recuperació davant Desastres (DRP – Disaster Recovery Plan)**.

Aquest pla inclou tots els processos de restauració de dades, hardware i software crític de l’organització davant d’un esdeveniment catastròfic, amb l’objectiu de recuperar l’activitat normal el més ràpid possible.

Un dels aspectes contemplats és assegurar que els treballadors puguin disposar dels seus equips de forma ràpida en cas de robatori, avaria o altres incidents. Per aquest motiu, se’ns demana la creació **d’imatges de restauració del sistema**.  
El temps de posada en marxa és crític i **no és viable** la solució clàssica d’instal·lar el sistema operatiu i configurar-lo manualment.

Cal tenir en compte que tots els equips del client utilitzen **Zorin OS 18**, amb una sèrie d’aplicacions prèviament configurades.

---

## Fase 1: Anàlisi i justificació de la solució tècnica

En aquesta primera fase, cal investigar eines que permetin crear una **imatge completa del disc** d’un equip i restaurar-la posteriorment mantenint totes les configuracions i aplicacions.

Cal elaborar una **comparativa de quatre productes**:
- **2 comercials**
- **2 de comunitat**

La comparativa ha d’incloure:
- Característiques destacades  
- Preu  
- Avantatges i inconvenients  
- Una conclusió comparativa (no còpia de webs)

Finalment, cal proposar una solució justificada en base a la comparativa realizada.

---

## Fase 2: Guia d’ús tècnica (Manual Operatiu)

A partir de la màquina proporcionada pel client (simulada amb una OVA), cal realitzar:

1. **Crear una imatge completa del sistema.**
2. **Restaurar aquesta imatge** en un sistema net (màquina virtual idèntica, però sense SO preinstal·lat).

La guia ha de:
- Estar documentada pas a pas  
- Incloure captures de pantalla significatives  
- Estar pensada perquè el personal de manteniment la pugui seguir sense dificultats

Com que és una prova de concepte i encara no se sap si el client acceptarà la solució final, aquesta guia es farà amb **Rescuezilla**.

> **Tasques individuals.**

---

## Materials i links de suport

- **INCIBE. _¿Ya tienes tu Plan de Recuperación ante Desastres?_** (Agost 2019)  
  Disponible a: https://www.incibe.es/empresas/blog/tienes-tu-plan-recuperacion-desastres

- **Pàgina oficial de Rescuezilla**
