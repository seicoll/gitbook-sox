# Sistemes de fitxers

## Introducció

> Per poder utilitzar una partició, cal donar-li format per gestionar els arxius que s'hi guardaran.

Els sistemes de fitxers divideixen l'espai de la partició en diferents zones. Per exemple, en el cas del sistema **FAT** hi ha les següents (els altres sistemes solen ser semblants):

Sector d'arrencada (BOOT): conté informació del sistema de fitxers i l'arrencada del sistema.
Regió FAT: gestiona l'espai lliure de la partició i normalment està duplicada ja que la informació que conté és molt important.
Directori arrel: conté la informació dels fitxers i les subcarpetes que es troben en el directori principal (nom, mida, on està guardat, permisos...).
Àrea de fitxers: és on es guarden els propis fitxers i carpetes.


**Característiques importants que han de tenir**
* Han de permetre la gestió de permisos per diferents usuaris i grups.
* Han de ser transaccionals (en anglès, **_journaling_**): aquesta característica disminueix molt el perill de perdre arxius o de que el sistema de fitxers quedi danyat en cas que falli una operació d'escriptura.

## Sistemes de fitxers Windows

### FAT32
Particions de fins a 2 TiB.
Arxius de fins a 4 GiB.
No permeten gestionar permisos per diferents usuaris.
No és transaccional.

### exFAT
Particions de fins a 512 TiB (màxim recomanat).
Arxius de fins a 16 EiB (límit teòric).
No permeten gestionar permisos per diferents usuaris.
Per defecte, no és transaccional, però se li pot afegir suport per ser-ho.

### NTFS
Particions de fins a 16 TiB (màxim 256 TiB).
Arxius tan grans com la partició.
És més eficient que FAT32.
Permet gestionar permisos per diferents usuaris.
Sistema de fitxers transaccional.

## Sistemes de fitxers Linux

### Ext4
Particions de fins a **1 EiB** (1 exbibyte = 260 Bytes = 1.152.921.504.606.846.976 Bytes).
Arxius de fins a 16 TiB.
És compatible amb **ext3**, i **ext3 **també ho és amb **ext4**.
Permet gestionar permisos per diferents usuaris.
Sistema de fitxers transaccional.

### Reiser4
Característiques similars a **ext4**, excepte amb la compatibilitat amb **ext3**

### Swap (o memòria d'intercanvi)
És un sistema de fitxers especial que s'utilitza quan es necessita més memòria RAM de la que té el maquinari.

## Documentació i recursos

* **Font d'informació: ** Apunts SOX Pere Sánchez ([http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=9&ref=1014](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=9&ref=1014))



