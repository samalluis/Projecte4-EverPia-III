# T06: Accés Remot – Escriptori Remot (RDP)  
### Tasca Individual

## Breu Descripció

Molt bé, equip,

En la tasca anterior vam establir les bases de l’administració remota de servidors mitjançant la línia de comandes (SSH). Però… què passa quan el servidor que administrem és un **Windows Server amb interfície gràfica**?  
O encara més important: què passa quan un client ens diu:

- *"No em funciona el programa X"*
- *"M’ha sortit un error a la pantalla"*
- *"No puc clicar aquest botó"*

Com a consultors d’**EverPia**, no només gestionem backend: també donem **suport directe a l’usuari final**. En moltes incidències, no n’hi ha prou amb una terminal; necessitem **veure el que l’usuari veu** i prendre el control del seu ratolí i teclat.

---

## La vostra missió: Guies de Suport Gràfic (PoC)

La vostra tasca és crear la documentació que rebran els futurs becaris de la consultora per realitzar suport remot gràfic.  
Farem una **Prova de Concepte (PoC)** interna utilitzant màquines virtuals per generar les **guies d’ús oficials** sobre com establir connexions d’Escriptori Remot.

Aquesta documentació serà la base del material de formació oficial, així que ha de ser:

- clara,  
- estructurada,  
- replicable,  
- i orientada a resolució ràpida d’incidències.

---

## Tecnologia a documentar

### **RDP (Remote Desktop Protocol)**

És l’estàndard absolut de Microsoft per accedir de forma remota a sistemes Windows amb entorn gràfic.

Però avui dia, **no és exclusiu de Windows**:

- En entorns GNU/Linux moderns com **Zorin OS**, **GNOME** ha incorporat suport natiu per RDP.
- Això significa que ens podem connectar a un equip Linux igual que ho faríem a un Windows 11.
- Per tant, RDP és una eina transversal tant per administració com per suport tècnic.

---

## Objectiu de la documentació que heu de crear

Heu de preparar una guia pràctica que expliqui:

### **1. Com activar i configurar RDP en equips Windows**
- Activar Remote Desktop.
- Configurar permisos d’usuari.
- Obtenir la IP del client.
- Verificar connectivitat.
- Recomanacions de seguretat.

### **2. Com connectar-se a un Windows des de:**
- **Windows** (Aplicació: Remote Desktop Connection)
- **Linux** (Clients com Remmina o GNOME Connections)

### **3. Com activar i configurar RDP en Zorin OS / Linux**
- Activar opcions de compartició de pantalla RDP.
- Configurar contrasenya i permisos.
- Verificar estat del servei.

### **4. Com connectar-se a un Linux des de:**
- **Windows** (client RDP)
- **Linux** (Remmina / GNOME Connections)

### **5. Bones pràctiques i troubleshooting**
- Problemes freqüents: ports, firewall, permisos.
- Sessions bloquejades o expirades.
- Rendiment lent i com millorar-lo.
- Quan utilitzar alternatives: AnyDesk, TeamViewer, Chrome Remote Desktop.

---

## Objectiu final

> **Crear una guia impecable que permeti a un nou becari connectar-se per RDP a qualsevol màquina en menys de 2 minuts.**

Recorda que:
- Un client nerviós està esperant.
- La rapidesa i eficàcia del suport defineix la qualitat del servei.

---

## Materials i links de suport

- **Moodle 0227 Serveis de Xarxa – UD4.AA3 Escriptoris Remots**



