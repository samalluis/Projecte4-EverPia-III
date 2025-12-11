# Guia de Suport Remot: Connexió per Escriptori Remot (RDP)

## 1. Introducció

Aquesta guia forma part de la documentació oficial per a becaris i tècnics de suport d’EverPia. L’objectiu és aprendre a establir connexions d’Escriptori Remot (RDP) tant a equips Windows com a equips basats en GNU/Linux (p. ex., Zorin OS amb GNOME). Aquest protocol permet visualitzar i controlar el ratolí i teclat del client, ideal per resolució d’incidències.

---

## 2. Què és RDP?

**RDP (Remote Desktop Protocol)** és un protocol desenvolupat per Microsoft que permet controlar gràficament equips remots. Inicialment només era disponible per a Windows, però GNOME ha integrat suport per RDP, fent-lo usable en distribucions com Zorin OS.

---

## 3. Requisits previs

### Per connectar-nos a un equip Windows:

* El client ha d’estar en edició Pro, Enterprise o Education.
* L’Escriptori Remot ha d’estar activat.
* El firewall ha de permetre connexions RDP (port TCP 3389).

### Per connectar-nos a un equip GNU/Linux (Zorin OS / GNOME):

* El client ha d’activar el servei d’escriptori remot a Configuració → Compartició.
* Cal tenir usuari i contrasenya configurats.

### Eines del tècnic:

* En Windows: Aplicació **Connexió a Escriptori Remot**.
* En Linux: Clients com **Remmina**, **KRDC** o la comanda `rdesktop`.

---

## 4. Activació de RDP al costat del client

### 4.1. Activar RDP a Windows 10/11

1. Obre **Configuració**.
2. Ves a **Sistema**.
3. Selecciona **Escriptori remot**.
4. Activa l’interruptor.
5. Comprova que l’opció "Permetre connexions només amb autenticació NLA" estigui activada.
6. Indica al client que et faciliti:

   * Nom del dispositiu
   * Adreça IP
   * Usuari i contrasenya

### 4.2. Activar RDP a Zorin OS / GNOME

1. Obre **Configuració**.
2. Ves a **Compartició**.
3. Activa la compartició.
4. Selecciona **Escriptori remot**.
5. Activa:

   * Permetre connexions RDP
   * Requerir contrasenya
6. El client t’ha de donar:

   * IP del dispositiu
   * Usuari i contrasenya

---

## 5. Connexió des d’un equip Windows (tècnic)

1. Cerca **Connexió a Escriptori Remot** al menú Inici.
2. Escriu l’adreça IP del client.
3. Fes clic a **Connectar**.
4. Introdueix les credencials facilitades.
5. Accepta els avisos de seguretat.
6. Ja pots controlar l’equip remot.

**Consells:**

* Si no connecta, comprova que el client està en línia i que el port 3389 no està bloquejat.
* En xarxes d’empresa pot ser necessari VPN.

---

## 6. Connexió des d’un equip Linux (tècnic)

### 6.1. Amb Remmina

1. Obre **Remmina**.
2. Crea una nova connexió.
3. Protocol: **RDP**.
4. Introdueix IP, usuari i contrasenya.
5. Desa i connecta.

### 6.2. Amb KRDC (KDE)

1. Obre KRDC.
2. Introdueix `rdp://IP_DEL_CLIENT`.
3. Connecta i introdueix credencials.

### 6.3. Amb línia de comandes (`xfreerdp`)

```
xfreerdp /v:IP_DEL_CLIENT /u:usuari /p:contrasenya
```

---

## 7. Solució de problemes freqüents

### ❌ Error: "No es pot establir connexió"

* RDP desactivat al client.
* Firewall bloquejant port 3389.
* IP incorrecta.
* El client té el PC adormit o apagat.

### ❌ Credencials incorrectes

* L’usuari no té permís RDP.
* Contrassenya mal escrita.

### ❌ Pantalla negra en connectar

* Problemes amb acceleració gràfica.
* Solució: provar alternativa `xfreerdp` o reconnectar.

---

## 8. Bones pràctiques en suport a clients

* Mantén sempre un to tranquil, encara que el client estigui nerviós.
* Explica cada pas abans de demanar-li fer alguna acció.
* Comprova dues vegades l’IP i credencials.
* Tanca la sessió RDP després d’acabar.

---

## 9. Annexos

* Port utilitzat per RDP: **3389/TCP**.
* Alternatives a RDP: AnyDesk, TeamViewer.

---

## Final

Aquesta guia es pot ampliar amb captures de pantalla o videoguies durant la PoC amb màquines virtuals. Si vols incloure imatges o crear versions imprimibles (PDF), puc generar-les.



