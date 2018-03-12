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

