# T01: DRP — Còpies de Seguretat  
## Estudi cas client (treball cooperatiu)

---

## Breu descripció

### Introducció
La primera hora el vostre responsable de seguretat us presenta el tema de les còpies de seguretat a partir d’un material didàctic. A continuació, caldrà que hi treballeu els aspectes del tema i ho fareu mitjançant una dinàmica cooperativa.

---

## Presentació del cas client

**"Muntatges i Serveis Tècnics SL"** és una petita empresa dedicada a la instal·lació i manteniment d'equips industrials.

### Infraestructura Tècnica
- **Servidor de Fitxers (Ubuntu Server)**: Conté tota la documentació crítica:
  - Documents de Projectes: Plànols, especificacions tècniques (300 GB, creixement moderat)
  - Bases de Dades: Comptabilitat i Clients (20 GB, canvi constant)
  - Carpetes Personals dels Usuaris: 100 GB

- **10 Equips Clients (Windows 10/11)**  
  Els usuaris treballen majoritàriament amb fitxers del servidor, però alguns tècnics guarden temporalment informes i arxius importants a *Documents*.

- **Connexió a Internet**  
  Fibra òptica 600 Mbps (simètrica)

### Requisits de Recuperació
- **RTO:** Dades de Comptabilitat/Clients disponibles en < 4 hores  
- **RPO:** Pèrdua màxima 24 h, excepte Comptabilitat/Clients (màxim 4 h)  
- **Retenció:** Historial mínim d’un mes  

---

# Fase 1: Treball individual

De forma individual, heu de respondre:

1. **Què copiar? (Priorització)**  
   Quines són les dades més crítiques del servidor?  
   Cal fer còpia dels 10 equips clients? Justifica-ho.

2. **Periodicitat i Tipus de Còpia**  
   Proposa un calendari bàsic setmanal (diari / setmanal / mensual)  
   i el tipus de còpia (completa, diferencial, incremental).

3. **Mitjans i Ubicació**  
   Quin mitjà utilitzar (discs externs, NAS, cloud, cintes)?  
   On guardar la còpia segons la regla **3-2-1**?

---

# Fase 2: Treball per parelles

1. **Discussió i consens**  
   Compareu les respostes individuals.

2. **Proposta unificada**  
   Dissenyar l’esquema de còpies 3-2-1 (3 còpies, 2 mitjans, 1 fora de lloc).

### Taula de treball de parella

| Element | Proposta de la Parella | Justificació |
|--------|-------------------------|--------------|
| **Dades Crítiques** |  |  |
| **Periodicitat (BD)** |  |  |
| **Tipus de Còpia (BD)** |  |  |
| **Mitjà 1 (Local)** |  |  |
| **Mitjà 2 (Extern)** |  |  |

---

# Fase 3: Treball en grup

1. **Debat i Selecció**  
   Cada parella presenta el seu esquema. El grup en valora pros i contres:  
   cost, temps de recuperació, seguretat, simplicitat…

2. **Disseny de la Política Final**  
   El grup redacta la Política de Còpies de Seguretat Definitiva per a l’empresa.

---

# Document Final (Fase 3)

El document final ha d’incloure:

---

## 1) Dades Objecte de Còpia
Especificar:
- Quines dades es copien  
- Amb quina freqüència  
- Separant **Servidor / Clients** i **crítiques / no crítiques**

---

## 2) Cronograma Setmanal Detallat

| Dia | Dades | Tipus de còpia | Mitjà |
|-----|--------|----------------|--------|
| Dilluns |  |  |  |
| Dimarts |  |  |  |
| ... |  |  |  |
| Diumenge |  |  |  |

---

## 3) Elecció de Mitjans i Ubicació (Regla 3-2-1)

- **Mitjà 1 (Local):**  
  (ex: disc dur USB, NAS)

- **Mitjà 2 (Extern):**  
  (ex: Cloud, LTO) i proveïdor (Azure, Google Cloud…)

- **Ubicació Fora de Lloc:**  
  On es guarda, i qui n’és responsable.

---

## 4) Estratègia de Recuperació (RTO / RPO)

Com s’assegura que:  
- **RPO = 4 hores** per a Comptabilitat/Clients  
- **RTO = 4 hores** per restaurar el servei

---

# Materials i links de suport

- Moodle 0226 Seguretat Informàtica — RA2.AA3 Còpies  
- INCIBE — *Copias de seguridad. Guía de aproximación para el empresario*  
- Xataka — Backup 3-2-1 (YouTube, 2017)  
  https://youtu.be/PM_M4Iz6I4o?si=F7DRyDDTZE3hjWn8

