# Guia interna de connexió SSH

## Base de coneixement per a becaris — Prova de Concepte (PoC)

Aquesta guia explica, de manera clara i pas a pas, com connectar-se de forma segura als sistemes interns de la consultora utilitzant SSH tant des de **clients Linux** com des de **clients Windows**. L'objectiu és que qualsevol nou tècnic pugui començar a treballar des del primer dia sense dependències.

---

# 1. Introducció a SSH

SSH (Secure Shell) és un protocol segur que permet connectar-se remotament a un altre sistema per línia de comandes. Les seves funcions principals són:

* Connexió segura
* Executar ordres remotes
* Transferència de fitxers
* Gestió de claus públiques i privades

---

# 2. Requisits previs

Abans de començar assegura’t de tenir:

* Credencials facilitades per l'empresa: **usuari**, **IP**, **port**, i **clau privada** (si s'utilitza autenticació amb claus).
* Accés a la màquina virtual interna.
* Connexió a la VPN corporativa (si és obligatori).

---

# 3. Connexió SSH des de Linux

## 3.1. Comprovar que SSH està instal·lat

```
ssh -V
```

Si no està instal·lat:

```
sudo apt install openssh-client
```

## 3.2. Connexió bàsica al servidor

```
ssh usuari@IP-del-servidor
```

## 3.3. Connexió amb port específic

```
ssh -p PORT usuari@IP
```

## 3.4. Connexió utilitzant una clau privada

Primer, donar permisos segurs:

```
chmod 600 clau.pem
```

Després connectar:

```
ssh -i clau.pem usuari@IP
```

## 3.5. Transferència de fitxers (SCP)

Enviar fitxer:

```
scp fitxer.zip usuari@IP:/ruta/de/destinacio
```

Rebre fitxer:

```
scp usuari@IP:/ruta/fitxer.zip .
```

---

# 4. Connexió SSH des de Windows

## 4.1. Utilitzar PowerShell (mètode recomanat)

### Comprovar versió SSH

```
ssh -V
```

PowerShell modern inclou SSH per defecte.

### Connectar-se

```
ssh usuari@IP
```

Amb port:

```
ssh -p PORT usuari@IP
```

Amb clau:

```
ssh -i C:\Ruta\clau.pem usuari@IP
```

## 4.2. Utilitzar el Terminal de Windows

Els passos són exactament iguals que amb PowerShell. Obre Windows Terminal i executa les mateixes ordres.

## 4.3. Transferència de fitxers

Igual que a Linux:

```
scp fitxer.txt usuari@IP:/ruta
```

---

# 5. Connexió entre màquines virtuals internes

## 5.1. Verificar la IP de cada VM

Linux:

```
ip a
```

Windows:

```
ipconfig
```

## 5.2. Comprovar si es veu la màquina remota

```
ping IP-de-la-segona-VM
```

## 5.3. Connexió SSH entre VMs

```
ssh usuari@IP-de-la-VM2
```

---

# 6. Gestió de claus SSH

## 6.1. Generar una clau nova

```
ssh-keygen -t rsa -b 4096
```

La clau pública és la que s'ha d'enviar a l'administrador.

## 6.2. Afegir la clau pública al servidor

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

## 6.3. Permisos necessaris

```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

# 7. Problemes habituals i solucions

**Error: Permission denied** → clau mal posada, permisos incorrectes.
**No route to host** → màquines no es veuen a la xarxa.
**Connection timed out** → port tancat o firewall.

---

# 8. Bones pràctiques de seguretat

* No compartir mai la clau privada.
* Ús obligatori de claus SSH quan sigui possible.
* Canviar ports per defecte quan l'empresa ho indiqui.
* No deixar sessions obertes.

---

# 9. Resum ràpid (per consultes ràpides)

**Connexió Linux:** `ssh usuari@IP`
**Connexió Windows:** igual que Linux.
**Amb clau:** `ssh -i clau.pem usuari@IP`
**Copiar fitxers:** `scp origen destí`

---

Aquesta guia és la base de la documentació oficial. Quan s'incorpori un nou becari, la utilitzarà per aprendre a operar amb SSH de manera immediata.

