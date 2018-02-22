<!-- notoc -->
# UF4. Integració de sistemes operatius

## Introducció

Actualment, en la majoria d'empreses existents, fan servir gran quantitat de **sistemes i dispositius diferents (maquinari i programari diferents)** dels que s'espera que interaccionin entre ells. 

Aquest conjunt de maquinari i programari diferents forma un sistema anomenat **sistema heterogeni**.

En aquesta unitat formativa ens ocuparem d'**integrar els diferents sistemes operatius** perquè siguin capaços de funcionar conjuntament i intercanviar informació.

### Compartició de recursos entre diferents sistemes operatius

**Windows** utilitza el protocol **SMB/CIFS** tant per compartir com per accedir a recursos compartits (arxius, carpetes i impressores).

* El protocol **SMB ** creat per IBM va ser adaptat per Microsoft i se li va canviar el nom per **CIFS (_Common Internent File System_)**.

**Linux** per compartir o accedir a recursos compartits necessita els següents programes:

* **smbclient**: és un programa que serveix per accedir a recursos compartits en Windows (SMB/CIFS).

* **Samba**: és un programa que permet compartir recursos utilitzant el protocol SMB/CIFS de forma que s'hi pugui accedir des de Windows.

### Dominis entre diferents sistemes operatius

**Windows** utilitza **Active Directory** per gestionar els usuaris i recursos d'un domini.

Es pot connectar un client **Linux** a un domini gestionat amb Active Directory fent una configuració manual bastant laboriosa o utilitzant un programa com **PBIS Open** que s'encarrega de realitzar la major part de la configuració amb unes poques comandes.

També es pot crear en **Linux** un domini similar a Active Directory, per connectar-hi tant clients Windows com clients Linux, utilitzant **Samba AD DC**.















