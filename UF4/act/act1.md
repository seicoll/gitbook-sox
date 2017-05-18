<!-- notoc -->

# Activitat 1. Compartir recursos amb Samba

En aquesta activitat configurarem el servidor de fitxers del **Samba **per a accedir-hi mitjançant l'autenticació.

## Requisits

Treballarem amb dues màquines virtuals amb Ubuntu. Una d'elles farà de client i l'altra de servidor. 
Configurar-les perquè estiguin connectades a una xarxa interna i tinguin una IP privada.

Configura el samba en un entorn de treball **_BOSCCOMA _**editant el fitxer `/etc/samba/smb.conf` el paràmetre:
  
  ```
  workgroup = BOSCCOMA
  ```
  
Estableix els mode de seguretat del Samba a **security = user** que obliga els clients a proporcionar un nom d'usuari i una contrasenya per accedir als recursos compartits.

  ```
  security = user
  ```  
  
No permetis l’accés als recursos compartits als usuaris convidats. Canvia en l'apartat [global]:

```
guest ok = no
```

Ara si us connecteu als directoris compartits, el sistema us demanarà el nom d'usuari i la contrasenya.

## Activitat

1. Dins del servidor crea els següents directoris:

  * /srv/samba/profes
  * /srv/samba/alumnes
  * /srv/samba/compartit 

  Crea un fitxer de text anomenat document.txt en cadascuna de les tres carpetes i posa-li qualsevol text.

2. En el servidor defineix els grups d’usuaris **profes **i **alumnes **i afegeix a cada grup els usuaris indicats a continuació

  |Grup     | Usuaris|
  | ------------- |:-------------:| 
  |profes   | prof1, prof2 |
  |alumnes  | alum1, alum2 |

  > Captura de pantalla del fitxer /etc/passwd i /etc/group.

3. Utilitza la comanda **smbpasswd **per afegir els nous usuaris a la llista d'usuaris samba. Com pots llistar els usuaris samba?

  > Captura de pantalla de la llista d’usuaris samba.

4. Fes que el directori `/srv/samba/profes` tingui permisos locals de lectura, escriptura i execució pels membres del **grup profes** i només de lectura i execució per la resta d'usuaris.

5. Modifica el fitxer de configuració samba perquè es permeti l'accés a `/srv/samba/profes` a través de la xarxa. Anomena el recurs compartit com **public_profes**.

6. Fes la prova des del client i connecta't com **prof1 **al recurs **public_profes**.  Pots utilitzar la interfície gràfica d'ubuntu. Tens permís per llegir i per escriure? 
Fes la prova també amb l'usuari **alum1**. Tens permís per llegir i per escriure?

7. Fes que els **professors **puguin llegir i escriure a **public_profes**. Connecta't com prof1 i crea un fitxer dins de la carpeta. Des del servidor fixa't amb els atributs del fitxer creat (ls -l /samba/profes). Amb quins permisos s'ha creat el fitxer? Qui és el propietari?

8. Fes que el grup **alumnes **no tingui accés al recurs **public_profes**.

9. Comparteix la carpeta **/srv/samba/alumnes** amb permisos de lectura i escriptura pels **alumnes **i restringiu l'accés als **profes**. 

  El nom del recurs serà **public_alumnes**. 

  Fes la prova des del client i comprova tens permís per llegir i escriure amb l’usuari **alum1**.

10. Fes el necessari per tal de que el directori **/srv/samba/compartit** s'ofereixi a la xarxa com un recurs pels membres dels grups **profes **i **alumnes **i ningú més. 
El nom del recurs serà **public**.

11. Fes servir la comanda `smbclient` per obtenir una llista dels recursos compartits del servidor. 

12. Des del **client **utilitza la comanda `mount` per muntar les unitats de xarxa segons la taula següent:

  |recurs	 | punt de muntatge | usuari   |
  | ------------- |:-------------:| 
  |public_profes | /mnt/profes | profe1   |
  |public_alumnes| /mnt/alumnes | alum1 |
  |public| /mnt/public | profe2|



