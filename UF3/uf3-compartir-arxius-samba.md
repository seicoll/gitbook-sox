# Compatir arxius i carpetes amb SAMBA

## Introducció

En el tema anterior van compartir carpetes utilitzant el protocol **NFS**.

Amb **NFS**, no hi ha cap procés d’acreditació d’usuaris per accedir al recursos compartits.

L’administrador ha de decidir amb cautela a quins ordinadors exporta un determinat directori.

La **manca d’autenticació d’usuaris** és un dels majors inconvenients del protocol **NFS**.

Només podem **restringir els permisos dels usuaris** utilitzant mecanisme habitual de permisos en sistema de fitxer Linux.

Per aquesta raó cada vegada s’utilitzen més altres sistemes de compartició de fitxers com, per exemple, el **Samba**.

## Què és SAMBA?

El **Samba** és un paquet de programari per Linux que implementa el protocol de comunicació SMB (Server Message Block) utilitzat per sistemes operatius Windows per compartir carpetes i impressores. 

El protocol **SMB** permet que els equips d’una xarxa local comparteixin fitxers i impressores.

Gràcies al **Samba**, en una xarxa hi pot haver equips amb Windows i equips amb Linux de manera que puguin intercanviar informació en carpetes compartides i compartir impressores.
