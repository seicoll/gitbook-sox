# Perfils mòbils en un domini Samba AD

## Creació de perfils mòbils

En general, la creació de **[perfils mòbils](//UF1/perfils-usuari.html#què-és-el-perfil-dun-usuari)** en un domini Samba és molt similar a la creació de perfils mòbils amb Active Directory si es fa des d'un client Windows unit al domini amb les eines d'administració remota (RSAT) que permeten configurar un domini (usuaris, grups, recursos compartits...).

## Configuració del servidor

### Crear i compartir les carpetes necessàries

Primer es creen les carpetes on es guardaran les carpetes de perfils, les carpetes privades i una o més carpetes que es compartiran amb diversos usuaris o grups.

Es poden crear a `/srv/samba` (no cal preocupar-se pels permisos locals; la configuració es farà modificant els permisos de seguretat des del client Windows):

```bash
sudo mkdir /srv/samba
sudo mkdir /srv/samba/perfils
sudo mkdir /srv/samba/privades
sudo mkdir /srv/samba/publica
```

Després, per compartir-les, afegim les següents línies a l'arxiu `/etc/samba/smb.conf` (aquí es pot donar permís de lectura i escriptura a tothom, `read only = no`; la limitació es farà modificant els permisos de seguretat des del client Windows):

```
[perfils]
    path = /srv/samba/perfils
    read only = no

[privades]
    path = /srv/samba/privades
    read only = no

[compartida]
    path = /srv/samba/publica
    read only = no
```

Si no es vol esperar a què Samba actualitzi aquesta informació (normalment no triga més d'un minut), es pot reiniciar el servei:

```bash
sudo service smbd restart
sudo service nmbd restart
```

## Configuració del client

### Configurar els permisos de la carpeta de perfils

Iniciant sessió amb l'administrador del domini Samba (**administrator**), buscar la carpeta compartida en el servidor i obrir els permisos de seguretat.
En el mode avançat, **deshabilitar l'herència de permisos** i configurar només els següents:
* Per a l'administrador (**Administrator**): control total sobre aquest directori, els subdirectoris i els fitxers
* Per al **propietari** (**_CREATOR OWNER_**): control total sobre els subdirectoris i els fitxers
* Per als usuaris del domini (**Domain users**) o altres grups: els següents permisos avançats només sobre aquest directori
  * Permís per travessar aquest directori / executar arxius
  * Permís per mostrar carpeta / llegir dades
  * Permís per crear carpetes / adjuntar dades
  
### Configurar els permisos de la carpeta per les carpetes privades

Es configura amb els mateixos permisos que l'anterior

### Configurar els permisos de la carpeta compartida per diversos usuaris

Es configura amb els permisos desitjats per a cada usuari i grup.

### Crear els scripts d'inici de sessió

Els scripts s'han de crear a la carpeta `netlogon` que es troba compartida en el servidor. Cal anar a _**Red > Servidor > netlogon**_ (també es pot accedir posant l'adreça del servidor i el nom de la carpeta compartida: \\USXXX\netlogon) i crear l'script.

> **ATENCIÓ**: els scripts han de ser arxius de text pla (sense format) i amb l'extensió `.bat` 

Si en el perfil d'un usuari es configura un dels scripts creats en aquesta carpeta, les comandes de l'script s'executaran en la màquina client cada cop que l'usuari iniciï la sessió.

Algunes de les accions que es poden posar en aquests arxius són:
* Sincronitzar la data i hora amb el servidor
* Connectar una unitat de xarxa amb una carpeta compartida en el servidor
* Connectar una impressora compartida en el servidor

### Configurar els perfils

Iniciant sessió amb l'administrador del domini Samba (**_administrator_**), obrir les eines d'administració remota del servidor o directament l'administració d'usuaris i equips del domini.

Seleccionant un usuari (o uns quants a la vegada), obrir la configuració del perfil i introduir les següents dades:
* **Ruta del perfil**: `\\USXXX\perfils\%username%`
* **Script d'inici de sessió**: `script.bat` (no cal posar la ruta)
* **Carpeta privada**:   Unitat de xarxa X:  Ruta \\USXXX\privades\%username%

## Comprovació dels perfils mòbils

### Comprovació dels permisos locals en el servidor

...

### Comprovació pràctica accedint i creant arxius des d'un client

**En un client Windows unit al domini Samba, realitza les següents accions:**

* Inicia sessió amb un usuari del domini.
* Assegura't que no surt el missatge de què ha hagut de crear un perfil temporal.
* Guarda un document amb el seu nom a l'escriptori.
* Accedeix a la seva carpeta privada a través de la unitat de xarxa on es troba i guarda un arxiu amb el seu nom.
* Accedeix a la carpeta compartida amb altres usuaris a través de la unitat de xarxa on es troba i guarda un arxiu amb el seu nom si té permisos per llegir i escriure, o comprova si pot veure els arxius que han creat altres usuaris.
* Tanca la sessió.
* Iniciant sessió amb l'administrador del domini, comprova que s'ha creat un perfil mòbil per l'usuari anterior

**En el servidor del domini Samba, fes les següents comprovacions:**

* Comprova que s'ha creat la carpeta del perfil d'aquest usuari i que dins de la carpeta **Escritorio** hi ha l'arxiu que ha creat.
* Comprova que s'ha creat la seva carpeta privada i que dins d'aquesta carpeta hi ha l'arxiu que ha creat.
* Comprova que dins de la carpeta compartida amb altres usuaris hi ha l'arxiu que ha creat (si tenia permisos per fer-ho).

