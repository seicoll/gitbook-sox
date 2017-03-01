# Zentyal com a controlador de domini

## Introducció

**Zentyal** integra **Samba4** com a servei de directori, implementant la funcionalitat d'un controlador de domini Active Directory de Windows, a més de compartició de fitxers i impressores.

El domini en aquest context consisteix en una sèrie de serveis distribuïts al llarg de tots els controladors, sent els més importants directori **LDAP**, el **servidor DNS** i l'autenticació distribuïda mitjançant **Kerberos**.

Per la compartició d'arxius, **Zentyal** utilitza el protocol **SMB/CIFS** per mantenir la compatibilitat amb els clients Microsoft. 

## Documentació i recursos

[Zentyal Documentació](https://wiki.zentyal.org/wiki/Es/4.1/Usuarios,_Equipos_y_Comparticion_de_ficheros)