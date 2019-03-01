# Comptarció de carpetes 

## Servidor i client

Qualsevol ordinador pot actuar com a **servidor** i com a **client**.

* **Servidor**: ordinador que comparteix un recurs.
* **Client**: ordinador que accedeix a un recurs compartit.

Només cal que tingui instal·lats els **programes** adequats: 
  * Un programa per **gestionar el servei** (en aquest cas, compartir un recurs) 
  * Un programa per poder **accedir al servei** (accedir al recurs compartit).

**Exemple:**

![](/assets/uf3-ServidorClient.svg)

**PC1** comparteix la carpeta C1 i per tant actua com a servidor, però a la vegada accedeix a la carpeta C2 compartida en PC2, per tant també actua com a client.
En canvi, el **Windows Server** només actua com a client, i el **PC2** només actua com a servidor.

## Permisos d'accés a carpetes i arxius

Quan es comparteixen carpetes, cal distingir entre **permisos locals** i **permisos de compartició**:

* **Permisos locals**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta local:
  * En Windows: `C:\Usuari\Documents`
  * En Linux: `/home/usuari`
  
* **Permisos de compartició**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta remota:
  * En Windows: 
    * `\\Server\Compartida` 
    *  `X:` (suposant que `X:` és una unitat de xarxa connectada amb una carpeta remota)
  * En Linux: 
    * `smb://server/compartida` 
    * `/mnt/compartida` (suposant que  `/mnt/compartida` és una carpeta remota muntada per exemple amb NFS).

Quan es comparteix una carpeta, s'han de configurar els **permisos de compartició**.

Es poden assignar diferents **permisos de compartició** per usuaris i grups. Aquests permisos **poden ser diferents dels permisos locals**.

> Quan s'accedeix a un recurs **de forma local** només es tenen en compte els **permisos locals**.
> Però quan s'accedeix a un recurs compartit **de forma remota** s'apliquen els permisos **més restrictius** entre els permisos locals i els permisos de compartició.

### Taula de permisos efectius quan s'accedeix a un arxiu o carpeta de forma remota

![](/assets/uf3-taula-permisos-remots.PNG)

## Documentació i recursos

* **Font d'informació:** [Apunts SOX (Pere Sánchez)](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=183&ref=3021)





