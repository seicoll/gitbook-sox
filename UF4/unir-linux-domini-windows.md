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


