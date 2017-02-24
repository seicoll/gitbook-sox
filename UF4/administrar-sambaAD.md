# Administrar el directori actiu de Samba 4

## Instal·lació de les eines per administrar el domini (RSAT)

Per administrar el domini Samba, utilitzarem un conjunt d’eines d’administració gratuïtes que ofereix Microsoft anomenades **_RSAT_** (_Remote Server Administration Tool_).

Aquestes eines s'instal·len en un **client Windows** i ens permetran gestionar el domini de forma idèntica a un domini amb Windows Server.

**_RSAT_** està disponible per diferents versions de Windows:

* Windows 10: https://www.microsoft.com/en-us/download/details.aspx?id=45520
* Windows 8.1: http://www.microsoft.com/en-us/download/details.aspx?id=39296
* Windows 8: http://www.microsoft.com/en-us/download/details.aspx?id=28972
* Windows 7: http://www.microsoft.com/en-us/download/details.aspx?id=7887

Un cop instal·lades, activarem a **_Características de Windows_** les eines d’administració necessàries (Remote Server Administration Tools)

![](/assets/RSAT1.jpg)

Un cop activades les eines, **iniciem sessió amb l'usuari administrador** del domini i obrim **_Administrador del servidor > Herramientas administrativas > Usuarios y equipos de Active Directory_** i podrem **gestionar el domini** tal i com realitzaven amb Windows Server.

> Per poder administrar el domini (afegir usuaris, grups...) cal iniciar sessió amb el **compte** d'administrador de Samba (**_Administrator_**).

## Documentació i recursos

* [Somebooks: Usar Windows 8.1 para administrar el directorio activo de Samba 4](http://somebooks.es/capitulo-12-integracion-de-redes-mixtas-con-windows-y-linux/8/)
