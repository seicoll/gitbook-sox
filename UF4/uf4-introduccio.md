<!-- notoc -->
# UF4. Integració de sistemes operatius

## Introducció

### Compartició de recursos entre diferents sistemes operatius

**Windows** utilitza el protocol **SMB/CIFS** tant per compartir com per accedir a recursos compartits (arxius, carpetes i impressores).

**Linux** necessita els següents programes o serveis:

* **smbclient**: és un programa que serveix per accedir a recursos compartits en Windows (SMB/CIFS).

* **smbfs**: per muntar carpetes compartides en Windows.

* **Samba**: servei compatible amb SMB/CIFS per compartir recursos de forma que s'hi pugui accedir des de Windows.

### Dominis entre diferents sistemes operatius

**Windows** utilitza **Active Directory** per gestionar els usuaris i recursos d'un domini.

Es pot connectar un client **Linux** a un domini gestionat amb Active Directory fent una configuració manual bastant laboriosa o utilitzant un programa com **PBIS Open** que s'encarrega de realitzar la major part de la configuració amb unes poques comandes.

Per crear en **Linux** un domini similar a Active Directory, per connectar-hi tant clients Windows com clients Linux, es pot utilitzar **Samba AD DC**.















