# Fase 1: Treball individual
De forma individual, heu de donar resposta a les següents preguntes basant-se en el cas pràctic:

### 1.  Què copiar? (Priorització): Quines són les dades més crítiques del servidor? Cal fer còpia dels 10 equips clients? Justifica-ho.

Primer de tot jo prioritzaria fer copias del **servidor de fitxers**, ja que es la part mes important, on es guarden documents de projectes, bases de dades i carpetes personals dels usuaris, es la base de tot, si perden el servidor perden tot, i sobre els equips no faria una copia de tot el equip, pero si faria copies de la carpeta de documents, ja que molts tecnics guardan informacio important alla.
   
### 2.  Periodicitat i Tipus de Còpia: Proposa un calendari bàsic per a la setmana (Diari/Setmanal/Mensual) i quin tipus de còpia aplicaràs (Completa, Diferencial, Incremental) per a les dades crítiques.

- Primer direm sobre la carpeta de documents, aquest com cada dia es va modificant i canviant farem una copia d'aquest diariament, i utilitzariam el tipus de copias incremental.

- Sobre el servidor, Documents de Projectes, al ser la una part molt important pero amb un pes bastant elevat farem una copa setmanalment, ja que si la fem diariament perdriam molt de temps, i si fos de manera mensual si es perd encara que el podriam recuperar es perdria bastanta informació important, i utilitzarem un format de copia completa.

- Per la base de dades, al ser nomes poc mes de 20 GB i es informacio molt important la qual pot anar variant cada dia, es fara una copia diaria, i aplicarem les copias diferencials.

- I per les carpetes personals d'usuaris, conte informació important de la feina, pero tampoc es que pesi poc, per  aixo en aquest cas farem una copia setmanal, i utilizarem un format de copia incremental.

   
### 3.  Mitjans i Ubicació: Quin tipus de mitjà de còpia utilitzaries (Discs durs externs, NAS, Cloud, Cintes)? On s'hauria de guardar físicament la còpia més recent (Regla 3-2-1).

Per fer les còpies de seguretat utilitzaria diferents sistemes, ja que és important seguir la regla 3-2-1, que vol dir tenir 3 còpies de les dades, en 2 tipus de suports diferents i 1 d’aquestes còpies guardada fora de l’empresa.

- Primer utilitzaria un NAS dins de l’empresa, perquè permet fer còpies automàtiques i és molt ràpid a l’hora de recuperar informació si es perd alguna dada. Aquest seria el sistema principal on es guardarien les còpies més recents, com les diàries i les setmanals.

- Després també utilitzaria algun servei de núvol (Cloud) per tenir una còpia fora de l’empresa. Això és útil per si passa alguna cosa greu a les instal·lacions, com un incendi o un robatori, així sempre quedaria una còpia segura a un altre lloc.

- Finalment, també faria servir discos durs externs o cintes per tenir còpies addicionals. Les cintes són més professionals i duren molt, però si el pressupost és limitat un disc dur extern ja va bé per tenir còpies setmanals o mensuals que no es consulten sovint.

Seguint la regla 3-2-1, la còpia més recent s’hauria de guardar al NAS, ja que és la que es pot necessitar recuperar més ràpidament. Una altra còpia es guardaria en un altre suport (disc dur o cinta) dins de l’empresa, i la tercera còpia s’hauria de guardar fora de l’empresa, al núvol, per assegurar que les dades estiguin protegides passi el que passi.

# Fase 2: Treball per parelles

Treballant per parelles:

1. **Discussió i Consens:** Comparen les seves respostes individuals (Fase 1).

2. **Elaboració d'una Proposta Unificada:** Heu de consensuar i dissenyar el vostre propi *Esquema 3-2-1 de Còpies* (3 còpies, 2 mitjans, 1 fora de lloc) basat en els requisits del cas.

| **Element**               | **Proposta de la Parella** | **Justificació** |
|---------------------------|-----------------------------|-------------------|
| **Dades Crítiques**       | Base de dades               | La base de dades es la mes important ja que es la que compte dades personal de clients la quals que si perden ho perden tot. |
| **Periodicitat (BD)**     | Setmanalment                | Diariament porque si la hacemos mensualmente seria una perdida de informacion muy importante si es que se llega a perder aunque tenga la copia i semanalmente tampoco por basiamente lo mismo, ademas hacerla diariamente nos ahorramos problemas y tampoco es que pese mucho.                  |
| **Tipus de Còpia (BD)**   |      Diferencial                       |  Porque al contener informacion tan importante, tener la copia de que se ha echo cada dia es bastante seguro, ya que es muy normal que algun usuario te pida la copia exacta de un dia enconcreto        |
| **Mitjà 1 (Local)**       |            RDX                 |   Porque al ser la que estara dentro de la empresa i la que se usara la primera, interesa que sea rapida, ademas que estara protegit de terceras personas que pasan per la empresa                |
| **Mitjà 2 (Extern)**      |             Cloud                |   perque si es perd o hi ha algun desastre en la empresa tenim la seguretat que tindrem una copia de seguretat en el cloud la qual sabem que no s'haura perdun en el desastre de l'empresa                |
