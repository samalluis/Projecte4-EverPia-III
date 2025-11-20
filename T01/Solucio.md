# Fase 1: Treball individual
De forma individual, heu de donar resposta a les següents preguntes basant-se en el cas pràctic:

### 1.  Què copiar? (Priorització): Quines són les dades més crítiques del servidor? Cal fer còpia dels 10 equips clients? Justifica-ho.

Primer de tot jo prioritzaria fer copias del **servidor de fitxers**, ja que es la part mes important, on es guarden documents de projectes, bases de dades i carpetes personals dels usuaris, es la base de tot, si perden el servidor perden tot, i sobre els equips jo no faria cap copia de seguretat, ja que no contenen informacio del tot important, l'unic que poden tenir de important es la carpeta de documents, pero aquesta ja esta guardada en el server **(carpetes personal d'usuaris)**.
   
### 2.  Periodicitat i Tipus de Còpia: Proposa un calendari bàsic per a la setmana (Diari/Setmanal/Mensual) i quin tipus de còpia aplicaràs (Completa, Diferencial, Incremental) per a les dades crítiques.

- Primer de tot jo faria una copia mensual del servidor de manera completa, ja que es important anan fent copies totals per aixi en el moment de voler fer copias diferencials e icrementals, no s'aixi de tornar molt enrera.

- Ara, de manera mes especifica, com els **Documents de Projectes**, al ser una part molt important pero amb un pes bastant elevat farem una copa setmanalment, ja que si la fem diariament perdriam molt de temps, i si fos de manera mensual si es perd encara que el podriam recuperar es perdria bastanta informació important, i utilitzarem un format de copia incremental.

- Per la base de dades, al ser nomes poc mes de 20 GB i per mi ser la informacio mes important al tenir informacio credencial de clients i com be diu el nom es la base, farem una copia diariament de manera diferencial.

- I per les carpetes personals d'usuaris, conte informació important de la feina, pero nomes hens interesa fer copia de la carpeta de documents del usuaris, la qual van modificant i guardan informacio important cada dia, tot l'ho altre no es important, ja que son imatges o aplicacions, per aixo, farem una copia diariament de manera diferencial.

   
### 3.  Mitjans i Ubicació: Quin tipus de mitjà de còpia utilitzaries (Discs durs externs, NAS, Cloud, Cintes)? On s'hauria de guardar físicament la còpia més recent (Regla 3-2-1).

Per fer les còpies de seguretat utilitzaria diferents sistemes, ja que és important seguir la regla 3-2-1, que vol dir tenir 3 còpies de les dades, en 2 tipus de suports diferents i 1 d’aquestes còpies guardada fora de l’empresa.

- Primer utilitzaria un NAS dins de l’empresa, perquè permet fer còpies automàtiques i és molt ràpid a l’hora de recuperar informació si es perd alguna dada. Aquest seria el sistema principal on es guardarien les còpies més recents, com les diàries i les setmanals.

- Després també utilitzaria algun servei de núvol (Cloud) per tenir una còpia fora de l’empresa. Això és útil per si passa alguna cosa greu a les instal·lacions, com un incendi o un robatori, així sempre quedaria una còpia segura a un altre lloc.

- Finalment, també faria servir discos durs externs o cintes per tenir còpies addicionals. Les cintes són més professionals i duren molt, però si el pressupost és limitat un disc dur extern ja va bé per tenir còpies setmanals o mensuals que no es consulten sovint.

Seguint la regla 3-2-1, la còpia més recent s’hauria de guardar al NAS, ja que és la que es pot necessitar recuperar més ràpidament. Una altra còpia es guardaria en un altre suport (disc dur o cinta) dins de l’empresa, i la tercera còpia s’hauria de guardar fora de l’empresa, al núvol, per assegurar que les dades estiguin protegides passi el que passi.

# Fase 2: Treball per parelles  
## Esquema 3-2-1 de Còpies (Proposta Unificada)

| **Element**          | **Proposta de la Parella** | **Justificació** |
|----------------------|-----------------------------|-------------------|
| **Dades Crítiques**  | Base de dades               | La base de dades és la més important, ja que conté dades personals i informació clau de clients. |
| **Periodicitat (BD)** | Diàriament                 | Una còpia mensual podria provocar pèrdues greus. Fer-la diàriament garanteix seguretat i no ocupa massa espai. |
| **Tipus de Còpia (BD)** | Diferencial              | Permet restaurar exactament l’estat d’un dia concret i és més ràpid que una còpia completa diària. |
| **Mitjà 1 (Local)** | RDX                          | Perquè és ràpid, segur i fàcil de substituir. A més, queda protegit físicament dins de l’empresa. |
| **Mitjà 2 (Extern)** | Cloud                       | Si hi ha un desastre físic a l’empresa, sempre queda una còpia segura fora de les instal·lacions. |

---

# Fase 3: Treball en grup

## 1) Datos Objeto de Copia

### 1.1 Servidor

#### **Datos críticos**
- Base de dades  
- Documents de projectes  
- Carpeta de documents dels usuaris  

#### **Datos no críticos**
- Altres carpetes personals d’usuaris (imatges, descàrregues, aplicacions…)

---

### **Frecuencia de copia del servidor**

#### **Dades crítiques**

**Base de dades**  
- Frecuencia: Diària  
- Tipo: Diferencial  

**Carpeta de documents dels usuaris**  
- Frecuencia: Diària  
- Tipo: Incremental  

**Documents de projectes**  
- Frecuencia: Setmanal  
- Tipo: Completa  

#### **Dades no crítiques**
- Frecuencia: Mensual  
- Tipo: Completa  

---

### 1.2 Equipos Clientes

#### **Datos críticos (documents, treballs, etc.)**
- Frecuencia: Setmanal  
- Tipo de copia: Incremental (només Documents)

#### **Datos no críticos**
- Frecuencia: Mensual  
- Tipo de copia: Completa (si es fa)

---

## 2) Cronograma Semanal Detallado

| **Día**     | **Datos**                                  | **Tipo de copia**                      | **Medio**           |
|-------------|---------------------------------------------|-----------------------------------------|----------------------|
| **Lunes**    | Base de dades + Carpeta documents          | Diferencial / Incremental               | NAS (RDX)           |
| **Martes**   | Base de dades + Carpeta documents          | Diferencial / Incremental               | NAS                 |
| **Miércoles**| Base de dades + Carpeta documents          | Diferencial / Incremental               | NAS                 |
| **Jueves**   | Base de dades + Carpeta documents          | Diferencial / Incremental               | NAS                 |
| **Viernes**  | BD + Carpeta documents + Projectes         | Diferencial / Incremental / Completa    | NAS                 |
| **Sábado**   | Replicació al Cloud                        | —                                       | Cloud               |
| **Domingo**  | Còpia mensual (dades no crítiques)         | Completa                                 | Disc extern / cinta |

---

## 3) Elección de Medios y Ubicación (Regla 3-2-1)

### 3.1 Medio 1 (Local)
- **Tipo:** RDX / NAS  
- **Ubicación:** Sala de servidors, dins del rack  
- **Responsable:** Tècnic de sistemes / Administrador de xarxes  

### 3.2 Medio 2 (Externo)
- **Tipo:** Cloud  
- **Proveedor:** Google Cloud, Azure o AWS  
- **Frecuencia:** Diàriament (rèplica automàtica nocturna)  
- **Responsable:** Responsable IT  

### 3.3 Ubicación Fuera de Lugar
- **Ubicación:** Núvol (zona geogràfica diferent a l’empresa)  
- **Tipo de datos:** Dades crítiques (BD, documents, projectes)  
- **Seguretat:**  
  - Accés xifrat  
  - Autenticació multifactor  
  - Polítiques d’accés basades en rols  
- **Responsable:** Responsable de Còpies i Recuperació  

---

## 4) Estrategia de Recuperación (RTO / RPO)

### **Objectius**
- **RPO:** 4 hores  
- **RTO:** 4 hores  

### **Com es garanteix el compliment**
- **Tipus de còpia:** Diferencial i incremental  
- **Còpies ràpides guardades a:** NAS / RDX local  

### **Procediment de recuperació**
1. Identificar el punt de restauració més recent segons el RPO.  
2. Carregar la còpia diferencial o incremental des del NAS.  
3. Verificar la integritat de la restauració.  
4. Restaurar serveis segons prioritat (BD → projectes → documents).  
5. Validació final amb l’equip tècnic.  

### **Personal responsable**
- Administrador de sistemes  
- Tècnic de suport  
- Supervisor IT  

---

## **Firma del grup**
- **Alumne 1:** …  
- **Alumne 2:** …  
- **Alumne 3:** …  
- **Alumne 4:** …  
