# Fase 1: Treball individual  
De forma individual, heu de donar resposta a les següents preguntes basant-se en el cas pràctic:

### 1. Què copiar? (Priorització)  
Quines són les dades més crítiques del servidor? Cal fer còpia dels 10 equips clients? Justifica-ho.

Primer de tot, jo prioritzaria fer còpies del **servidor de fitxers**, ja que és la part més important: s’hi guarden els documents de projectes, les bases de dades i les carpetes personals dels usuaris. És la base de tot; si es perd el servidor, es perd tota la informació.  
Pel que fa als equips clients, **no faria cap còpia de seguretat**, ja que no contenen informació especialment rellevant. L’únic element important podria ser la carpeta de documents, però aquesta ja està guardada al servidor (**carpetes personals d’usuaris**).

---

### 2. Periodicitat i Tipus de Còpia  
Proposa un calendari bàsic per a la setmana (Diari/Setmanal/Mensual) i quin tipus de còpia aplicaràs (Completa, Diferencial, Incremental).

- Faria una còpia **mensual completa del servidor**, ja que és important disposar d'una base completa per poder treballar després amb còpies diferencials o incrementals sense haver de retrocedir massa.
  
- En el cas dels **Documents de Projectes**, com que són molt importants però pesen força, faria una còpia **setmanal** en format **complet**. Fer-la diàriament seria massa lent i fer-la mensual faria que es pogués perdre informació rellevant.

- Per a la **base de dades**, que pesa uns 20 GB i conté informació sensible de clients, faria una còpia **diària** de tipus **diferencial**.

- Per a les **carpetes personals d’usuaris**, només interessa copiar la carpeta de documents, que s’actualitza diàriament amb informació de feina. La resta (imatges, aplicacions...) no és important. Per això, faria una còpia **diària** de tipus **incremental**.

---

### 3. Mitjans i Ubicació (Regla 3-2-1)

Per fer les còpies de seguretat utilitzaria diferents sistemes seguint la regla 3-2-1:  
**3 còpies**, **2 tipus de suport**, **1 fora de l’empresa**.

- **NAS a l’empresa**: per a les còpies automàtiques més recents (diàries i setmanals). Recuperació molt ràpida.
- **Còpia al núvol (Cloud)**: per tenir una còpia fora de l’empresa en cas d’incendi, robatori o desastre.
- **Discos durs externs o cintes**: per còpies addicionals mensuals.

La còpia més recent s’ha de guardar al **NAS**, una segona còpia al **disc extern/cinta** dins l’empresa i la tercera al **núvol**.

---

# Fase 2: Treball per parelles  
## Esquema 3-2-1 de Còpies (Proposta Unificada)

| **Element**            | **Proposta de la Parella** | **Justificació** |
|------------------------|-----------------------------|-------------------|
| **Dades Crítiques**    | Base de dades               | És la més important perquè conté dades personals i informació clau dels clients. |
| **Periodicitat (BD)**  | Diàriament                  | Una còpia mensual podria causar grans pèrdues; la còpia diària és segura i lleugera. |
| **Tipus de Còpia (BD)**| Diferencial                 | Permet restaurar l’estat exacte d’un dia i és més eficient que una completa diària. |
| **Mitjà 1 (Local)**    | RDX                         | Ràpid, segur, fàcil de substituir i protegit físicament. |
| **Mitjà 2 (Extern)**   | Cloud                       | Permet tenir una còpia fora de l’empresa en cas de desastre. |

---

# Fase 3: Treball en grup

## 1) Dades Objecte de Còpia

### 1.1 Servidor

#### **Dades crítiques**
- Base de dades  
- Documents de projectes  
- Carpeta de documents dels usuaris  

#### **Dades no crítiques**
- Altres carpetes personals (imatges, descàrregues, aplicacions...)

---

### **Freqüència de còpia del servidor**

#### **Servidor complet**
- **Freqüència:** Mensual  
- **Tipus:** Completa  

#### **Dades crítiques**

**Base de dades**  
- Freqüència: Diària  
- Tipus: Diferencial  

**Carpeta de documents dels usuaris**  
- Freqüència: Diària  
- Tipus: Incremental  

**Documents de projectes**  
- Freqüència: Setmanal  
- Tipus: Completa  

#### **Dades no crítiques**
- Freqüència: Mensual  
- Tipus: Completa  

---

### 1.2 Equips Clients

#### **Dades crítiques (documents, treballs...)**
- Freqüència: Setmanal  
- Tipus: Incremental (només Documents)

#### **Dades no crítiques**
- Freqüència: Mensual  
- Tipus: Completa (si es fa)

---

## 2) Cronograma Setmanal Detallat

| **Dia**        | **Dades**                                   | **Tipus de còpia**                        | **Mitjà**           |
|----------------|----------------------------------------------|--------------------------------------------|----------------------|
| **Dilluns**     | Base de dades + Carpeta de documents         | Diferencial / Incremental                  | NAS (RDX)            |
| **Dimarts**     | Base de dades + Carpeta de documents         | Diferencial / Incremental                  | NAS                  |
| **Dimecres**    | Base de dades + Carpeta de documents         | Diferencial / Incremental                  | NAS                  |
| **Dijous**      | Base de dades + Carpeta de documents         | Diferencial / Incremental                  | NAS                  |
| **Divendres**   | BD + Carpeta docs + Projectes                | Diferencial / Incremental / Completa       | NAS                  |
| **Dissabte**    | Replicació al Cloud                          | —                                          | Cloud                |
| **Diumenge**    | Còpia mensual (dades no crítiques)           | Completa                                   | Disc extern / cinta  |

---

## 3) Elecció de Mitjans i Ubicació (Regla 3-2-1)

### 3.1 Mitjà 1 (Local)
- **Tipus:** RDX / NAS  
- **Ubicació:** Sala de servidors (rack)  
- **Responsable:** Tècnic de sistemes / Administrador de xarxes  

### 3.2 Mitjà 2 (Extern)
- **Tipus:** Cloud  
- **Proveïdor:** Google Cloud, Azure o AWS  
- **Freqüència d’actualització:** Diària (rèplica automàtica nocturna)  
- **Responsable:** Responsable IT  

### 3.3 Ubicació Fora de l’Empresa
- **Ubicació:** Núvol (regió diferent)  
- **Dades emmagatzemades:** Dades crítiques (BD, documents, projectes)  
- **Seguretat:**  
  - Accés xifrat  
  - Autenticació multifactor  
  - Polítiques d’accés basades en rols  
- **Responsable:** Responsable de Còpies i Recuperació  

---

## 4) Estratègia de Recuperació (RTO / RPO)

### **Objectius**
- **RPO:** 4 hores  
- **RTO:** 4 hores  

### **Com es garanteix**
- **Tipus de còpia:** Diferencial i incremental  
- **Còpies ràpides guardades a:** NAS / RDX  

### **Procediment de recuperació**
1. Identificar el punt de restauració més recent (segons RPO).  
2. Carregar la còpia diferencial o incremental des del NAS.  
3. Verificar la integritat de la restauració.  
4. Restaurar serveis per prioritat (BD → projectes → documents).  
5. Validació final amb l’equip tècnic.  

### **Personal responsable**
- Administrador de sistemes  
- Tècnic de suport  
- Supervisor IT  

---

**Click aquí per anar al [README de l’Activitat](README.md)**  
**Click aquí per tornar a la [HOME](..)**  
