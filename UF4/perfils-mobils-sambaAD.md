# Perfils mòbils en un domini Samba AD

## Creació de perfils mòbils

En general, la creació de **perfils mòbils** en un domini Samba és molt similar a la creació de perfils mòbils amb Active Directory si es fa des d'un client Windows unit al domini amb les eines d'administració remota (RSAT) que permeten configurar un domini (usuaris, grups, recursos compartits...).

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