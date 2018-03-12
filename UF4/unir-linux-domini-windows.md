# Unir un client Linux a un domini Windows

Hi ha moltes formes d'unir un client Linux a un domini Windows amb Active Directory, però una de les més senzilles és utilitzar un programa que s'encarregui de fer la major part de la configuració del sistema en lloc de fer-ho manualment.

En versions més antigues d'Ubuntu Desktop podem trobar en els mateixos repositoris d'Ubuntu el paquet **_Likewise Open_**, però actualment l'empresa Beyond Trust s'ha encarregat d'actualitzar-lo i li ha canviat el nom per **_PBIS Open_**.

Es pot trobar tota la documentació sobre PBIS a la [web de Beyond Trust](https://www.beyondtrust.com/products/powerbroker-identity-services-ad-bridge/).

## Configuració inicial

### Configuració per un domini .local

> **ATENCIÓ**: en Ubuntu, quan es vol connectar amb un domini de tipus **_.local_**, s'ha de canviar una línia del fitxer `/etc/avahi/avahi-daemon.conf`:

```
#domain-name=local
domain-name=.alocal
```

### Instal·lació del servei SSH

Per motius de seguretat, el programa PBIS Open utilitza ssh per comunicar-se amb el servidor de forma encriptada, i necessita que estigui instal·lat el servei de **ssh** en el client:

`sudo apt install openssh-server`

## Instal·lació del programa PBIS Open en el client Linux

### Descarregar PBIS Open
En un client Linux, descarregar el paquet PBIS Open que es pot trobar en aquesta web: [https://www.beyondtrust.com/powerbroker-identity-services-open-request/?Pass=True](https://www.beyondtrust.com/powerbroker-identity-services-open-request/?Pass=True). Cal triar l'opció adequada en funció del sistema on es vulgui instal·lar.

Si no es disposa d'un entorn gràfic amb navegador, també es pot descarregar mirant l'adreça de l'enllaç adequat i utilitzant la comanda wget:

```
wget https://github.com/BeyondTrust/pbis-open/releases/download/8.5.2/pbis-open-8.5.2.265.linux.x86_64.deb.sh
```

### Instal·lar PBIS Open

Per instal·lar-lo, primer se li han de donar permisos d'execució a l'arxiu descarregat.

`chmod a+x pbis-open-8.5.2.265.linux.x86_64.deb.sh`

Després ja es pot executar amb la següent comanda (cal respondre sempre yes):

`sudo ./pbis-open-8.5.2.265.linux.x86_64.deb.sh`

>**ATENCIÓ**: encara que s'obri una finestra per connectar al domini, abans s'ha de comprovar que el servei **lwsmd** es reinicia correctament, i després reiniciar el sistema:

```
sudo service lwsmd restart
sudo reboot
```

### Comprovar el servei PBIS
Amb la comanda **pbis status** es pot comprovar l'estat del servei:

```bash+theme:dark
usuari@ucxxx:~$ pbis status
...
[Authentication provider: lsa-activedirectory-provider]
    Status:        Online
    Mode:          Un-provisioned
    Domain:        ADXXX.LOCAL
    Domain SID:    S-1-5-21-3903495518-2577291124-556879616
    Forest:        adxxx.local
...
    [Domain: ADXXX]
        DNS Domain:       adxxx.local
        Netbios name:     ADXXX
        Forest name:      adxxx.local
...
        [Domain Controller (DC) Information]
            DC Name:              wsxxx.adxxx.local
            DC Address:           172.30.0.10
...
```

## Unir el client Linux a un domini Windows

### Utilitzant la interfície gràfica

Per obrir la interfície gràfica cal executar la següent comanda:

`sudo /opt/pbis/bin/domainjoin-gui`

![](/assets/PBIS-domini.png)

* Nom del domini: `adxxx.local`
* Deshabilitar l'opció _**Enable default user name prefix**_

Quan es faci clic a l'opció **_Join Domain_** demanarà el nom d'un usuari que pugui unir màquines al domini (normalment l'administrador del domini) i la seva contrasenya.

> **ATENCIÓ**: si no es desmarca l'opció **_Enable default user name prefix_** es podran validar usuaris sense haver de posar el prefix **ADXXX\** o el sufix **@adxxx.local**, però pot portar a confusió si existeixen usuaris locals amb el mateix nom que usuaris del domini.

Ha de sortir el missatge **_SUCCESS_** si s'ha unit correctament al domini.

Cal **reiniciar** el sistema per poder validar usuaris de l'Active Directory.

### Utilitzant la consola

Al executar la següent comanda, demanarà la contrasenya de l'usuari **administrador** del domini.

`
sudo /opt/pbis/bin/domainjoin-cli join adxxx.local administrador
`

Ha de sortir el missatge **_SUCCESS_** si s'ha unit correctament al domini.

Cal **reiniciar el sistema** per poder validar usuaris de l'Active Directory.

## Comprovació i validació d'usuaris en el client Linux

Comprovar que el sistema pot mostrar els usuaris del domini
Amb les comandes **getent passwd** i **getent group** es poden veure els usuaris del sistema:

```bash+theme:dark
usuari@ucxxx:~$ getent passwd
root:x:0:0:root:/root:/bin/bash
usuari:x:1000:1000:usuari,,,:/home/usuari:/bin/bash
...
ADXXX\administrador:PBIS:2035286516:2035286529::/home/ADXXX/administrador:/bin/bash
ADXXX\usuari:PBIS:2035287018:2035286529:usuari:/home/ADXXX/usuari:/bin/bash
ADXXX\ppadilla:PBISX:2035287130:2035286529:Pau Padilla :/home/ADXXX/ppadilla:/bin/bash
ADXXX\aamat:PBISx:2035287137:2035286529:Albert Amat:/home/ADXXX/aamat:/bin/bash

usuari@ucxxx:~$ getent group
root:x:0:
usuari:x:1000:
...
ADXXX\admins.^del^dominio:PBIS:2035286528:
ADXXX\usuarios^del^dominio:PBIS:2035286529:ADXXX\ppadilla
ADXXX\profes:PBIS:2035287124:ADXXX\ppadilla
ADXXX\alumnes:PBIS:2035287125:ADXXX\aamat
```

Els usuaris i grups del domini apareixen amb el nom NetBIOS del domini al davant: `ADXXX\usuari` o  `ADXXX\grup`.

### Validar usuaris del domini Windows

Per poder validar usuaris des de l'entorn gràfic escrivint el seu identificador, cal [configurar **LightDM**](https://seicoll.gitbooks.io/sox/content/UF2/uf2-auteticacio-ldap.html#validar-usuaris-amb-entorn-gr%C3%A0fic).

Es poden utilitzar els mateixos formats que s'utilitzen en Windows:

* **ADXXX\usuari**
* **usuari@adxxx.local**

Si s'utilitza la primera forma quan es valida des de la consola, és possible que calgui posar **doble contrabarra** (\\) entre el nom del domini i el nom d'usuari: `ADXXX\\usuari`

## Desconnexió del domini i desinstal·lació de PBIS en el client Linux






