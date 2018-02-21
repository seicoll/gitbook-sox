# Accedir a recursos compartits en Windows des de Linux

## Compartir arxius i carpetes en Windows

[Apunts sobre compartició d'arxius i carpetes en Windows](https://seicoll.gitbooks.io/sox/content/UF3/uf3-compartir-arxius-windows.html#compartici%C3%B3-de-carpetes)

## Preparar Linux per accedir a carpetes compartides en Windows

> Tot el que s'explica a continuació també serveix per accedir a una carpeta que s'ha compartit en Linux utilitzant el protocol **Samba**.

Per accedir a un recurs compartit amb Windows o Samba \(mitjançant el protocol **SMB/CIFS**\) des de Linux cal instal·lar el **client Samba** \(paquet **smbclient**\):

`sudo apt install smbclient cifs-utils`

Per defecte, aquest paquet ja està instal·lat en Ubuntu Desktop.

Es pot comprovar si està instal·lat amb la comanda dpkg:

```bash
usuari@ucxxx:~$ dpkg -s smbclient
Package: smbclient
Status: install ok installed
...
```

La comanda `smbclient` obre un petita aplicació que ens permet accedir a un recurs del servidor Samba.

* Per **exemple**, si volem accedir a la carpeta compartida '_alumnes_' del servidor, executarem:

  `smbclient //IP_servidor/alumnes`

Aquesta comanda s'utilitza, sobretot, per **llistar els recursos compartits** d’una màquina remota:

`smbclient -L IP_servidor`

Si el recurs està protegit amb contrasenya, també podem indicar amb quin usuari hi accedim fent.

`smbclient -U usuari -L IP_servidor`

### Accedir a carpetes compartides de forma gràfica

L’Ubuntu ens permet accedir **gràficament** als recursos disponibles dels grups de treball del Samba amb el navegador Nautilus.

Es pot fer de vàries formes:

* Per mitjà del menú _**Xarxa**_ &gt; `IP_servidor` .
* **Conectar con el servidor** \(`smb://IP_servidor`\)
* **Ctrl + L** per poder escriure a la barra d'adreces i escriure `smb://IP_servidor`

També es pot accedir directament a una de les carpetes compartides si es coneix el nom del recurs compartit:

`smb://IP_servidor/alumnes`

### Muntar carpetes compartides

També hi ha la possibilitat **muntar les carpetes compartides** en carpetes del nostre sistema com si es tractés d'una carpeta local.

* És igual com en els recursos **NFS**.
* La **diferència **entre **NFS** i **SMB **és que NFS no requereix que l’usuari que fa la connexió s’autentifiqui i amb SMB sí cal autentificació.

Cal instal·lar el paquet **cifs-utils**:

`sudo apt-get install cifs-utils`

**Per exemple**, si volem accedir des de l’equip d’un professor a una carpeta compartida amb el nom de professors al servidor, executarem:

`mount –t cifs //IP_servidor/alumnes /mnt/alumnes –o username=usuari,password=pass`

Si el servidor no requereix que l’usuari s’autentiqui \(permet accés a convidats\), els paràmetres username, password i workgroup es poden obviar.

`mount –t cifs //IP_servidor/alumnes /mnt/alumnes`

> **ATENCIÓ:** per saber els permisos efectius d'accés a una carpeta compartida cal tenir en compte els permisos que té l'usuari que es connecta a la carpeta remota \(usuari Samba\) i els permisos que té l'usuari actual sobre la carpeta local on està muntada la carpeta compartida.

### Muntar carpetes compartides de forma automàtica

Si volem que una carpeta compartida **es connecti sempre de forma automàtica** quan iniciem el nostre Linux, cal afegir a l'arxiu `/etc/fstab` una línia com:

Si el recurs compartit permet l’accés a convidats \(guests\):

`//IP_servidor/professors  /mnt/professors  cifs  guest  0  0`

Si el recurs compartit està protegit per contrassenya:

`//IP_servidor/professors /mnt/professors cifs  username=usuari,password=constrasenya,sec=ntlm  0  0`

Per muntar automàticament els recussos definits a `/etc/fstab` sense necessitat de reiniciar el sistema podeu executar.

`sudo mount -a`

Per comprovar si s'han muntat correctament les carpetes es pot utilitzar la comanda `mount`.

**Més informació**: 
[https://wiki.ubuntu.com](https://wiki.ubuntu.com/MountWindowsSharesPermanently)
[ITE Educacion: Cliente de Samba](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m4/cliente_de_samba.html)

