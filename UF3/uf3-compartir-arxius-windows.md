# Compartir recursos i seguretat en Windows

## Introducció 

### Conceptes bàsics

Windows utilitza el protocol **CIFS** (antigament anomenat **SMB**) per compartir arxius, carpetes i impressores en un entorn en xarxa. També se'l sol anomenar **SMB/CIFS**.

**Propietari d'un arxiu o carpeta**

En Windows, cada carpeta i arxiu pertany a un usuari o a un grup d'usuaris, que és qui l'ha creat, però es pot canviar sempre que es tinguin els permisos per fer-ho.
L'usuari o grup propietari, per defecte té tots els permisos.

**Permisos per arxius i carpetes**
A part del propietari, es poden afegir altres usuaris i grups, i assignar permisos diferents.
> Si un usuari pertany a dos grups, se sumen els permisos dels dos grups.

**Permisos locals (de seguretat o NTFS)**
Són els permisos que tindran els usuaris quan accedeixin als recursos (arxius, carpetes i impressores) de forma local.

**Herència**
Quan es crea una carpeta, aquesta hereta els permisos de la carpeta pare, però aquesta dependència es pot trencar per canviar i posar els permisos adequats a cada cas.

### Recursos compartits

Un recurs compartit és un objecte al qual es pot accedir de forma remota.
El recursos que es poden compartir són:
* **Arxius i carpetes**
* **Impressores**

El nom del recurs compartit (el que s'ha d'utilitzar quan s'accedeix de forma remota) pot ser diferent del nom real.

Recursos compartits per defecte en un domini

* **NETLOGON**: Conté els scripts d'inici de sessió. C:\Windows\SYSVOL\sysvol\domini\SCRIPTS
* ****SYSVOL****: Conté els fitxers públics del domini. C:\Windows\SYSVOL\sysvol

### Compartició de carpetes

Quan es comparteixen carpetes, cal distingir entre permisos locals i permisos de compartició:

* **Permisos locals**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta local:
  * En Windows: C:\Usuari\Documents
* **Permisos de compartició**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta remota:
  * En Windows: \\Server\Compartida o X: (suposant que X: és una unitat de xarxa connectada amb una carpeta remota)

Quan es comparteix una carpeta, s'han de configurar els **permisos de compartició**.

Es poden assignar diferents permisos de compartició per usuaris i grups. Aquests permisos poden ser diferents dels permisos locals.

> Quan s'accedeix a un recurs **de forma local** només es tenen en compte els permisos locals, però quan s'accedeix a un recurs compartit **de forma remota** s'apliquen els permisos **més restrictius** entre els permisos locals i els permisos de compartició.

> Una forma de simplificar la gestió dels permisos quan es comparteixen arxius i carpetes és posar **Control total** als permisos de compartició i gestionar els permisos locals més detalladament.
> Això no sempre es pot fer (depén dels requeriments de seguretat) però en la majoria de casos, sí.

## Gestió de permisos locals

Per configurar els permisos locals cal anar a les **propietats de la carpeta** i entrar a la pestanya **_Seguridad_**.

![](/assets/win-permisos-locals.png)

### Gestionar els usuaris

Es poden afegir o eliminar usuaris i grups fent clic al botó **_Editar_**.

### Gestionar els permisos simples

Seleccionant l'usuari o grup es poden marcar o desmarcar les caselles **_Permitir o Denegar_** en cada permís.

Per defecte, si no està marcada la casella **_Permitir_**, implica que no es té el permís corresponent.

### Opcions avançades

Amb el botó **_Opciones avanzadas_** es poden canviar algunes propietats avançades:

![](/assets/win-pemisos-avansats.png)

#### Canviar el propietari

A més de canviar el propietari de la carpeta, també es pot canviar en els arxius i subcarpetes.

#### Habilitar / Deshabilitar la herència

En el cas de deshabilitar l'herència es pot triar entre dues opcions:
* **Mantenir els permisos actuals**: es fa una còpia dels permisos actuals però ara es podran modificar.
* **Esborrar tots els permisos**: s'hauran de crear de nou tots els permisos.

#### Gestionar els permisos avançats
Seleccionant un usuari o grup, es poden afegir, eliminar o editar els permisos avançats:

![](/assets/win-permisos-avansats-afegir.png)

## Gestió de permisos de compartició

Per configurar els permisos de compartició cal anar a les **propietats de la carpeta** i entrar a la pestanya **_Compartir_**.

![](/assets/win-permisos-compartits.png)

> Un cop s'hagi compartit la carpeta, la ruta que s'ha d'utilitzar per accedir de forma remota és la que apareix a **_Ruta de acceso de red:_** ```\\\WIN-SOX\Compartida```.

### Compartició senzilla

Amb el botó **_Compartir_**, s'accedeix a les opcions per compartir la carpeta de forma senzilla.
Només es poden afegir o eliminar **usuaris i grups**, i assignar-los permisos de **Lectura **o de **Lectura i escriptura**.

![](/assets/win-permisos-compartits-simple.png)

### Compartició avançada

Amb el botó **_Uso compartido avanzado_**, s'accedeix a les opcions per compartir la carpeta de forma avançada.

![](/assets/win-permisos-compartits-avansats1.png)

En aquest cas es disposa de més opcions per configurar la compartició:

* Marcar o desmarcar la casella **_Compartir esta carpeta_** per compartir-la o deixar-la de compartir.
* Posar-li un **nom de recurs** compartir diferent del nom original. Aquest nom és el què s'ha d'utilitzar quan es vol accedir a aquest recurs de forma remota.
* Es pot establir el **nombre màxim d'usuaris** que poden utilitzar la carpeta simultàniament.
* Els **permisos** que es poden assignar són diferents: **_Llegir, Canviar i Control total_**.

![](/assets/win-permisos-compartits-avansats2.png)

> Es pot simplificar la configuració de permisos de compartició posant **Control total** a **_Compartició_** i gestionar els permisos més detalladament a **_Seguretat_**.
> En alguns casos no es podrà fer així: per exemple, si es vol que els usuaris tinguin permís de lectura i escriptura quan accedeixin localment però només de lectura quan ho facin de forma remota.

### Carpetes compartides ocultes

* Si es vol compartir un recurs però que **no sigui visible** (només es podrà connectar qui conegui la ruta a aquest recurs) només cal afegir un **$** darrera del nom del recurs.
  * Per exemple: C$
  
* Amb **\\\ip_equip** o **\\\nom_equip** es pot veure els recursos compartits visibles.

* Es pot accedir a un recurs compartit ocult si es conneix tota la ruta.
  * Per exemple: \\\192.168.0.1\C$
  
### Veure els permisos efectius

És fàcil cometre errors al combinar permisos locals amb permisos compartits, i sol ser difícil descobrir quins són els permisos que estan mal configurats.
Per ajudar en aquesta tasca, es pot anar a permisos locals (pestanya **_Seguridad_**), clicar el botó **_Opciones avanzadas_** i entrar a la pestanya **Acceso efectivo**.

Aquesta finestra permet comprovar quins permisos té un usuari i, en cas que no tingui un permís, saber si el problema està en la configuració dels permisos locals o en els permisos de compartició.

Primer cal **triar l'usuari o grup** i després clicar el botó **_Ver acceso efectivo_**.

![](/assets/win-permisos-efectius.png)

En les dues primeres columnes se indica si l'usuari o grup té o no un permís determinat.
En cas que no el tingui, en la tercera columna se indica el motiu:
* **Permisos de archivo**: no s'ha donat permís en la configuració de **permisos locals**.
* **Compartir**: no s'ha donat permís en la configuració de **permisos de compartició**.

## Activar unitats compartides

Per activar les unitats compartides has de fer el següent:

1. Fer clic a **_Inici > Xarxa_** per accedir al centre de Xarxes i recursos compartits.
2. Activar l’**_Ús compartit d’arxius i impressores_**.

![](/assets/win-activar-us-compartit.PNG)

* L’opció **_Ús compartit d’arxius i impressores_** controla l’accés als recursos compartits per mitjà de la xarxa i a les impressores connectades a l’equip.

* L’opció **_Ús compartit de la carpeta públic_** controla l’accés a les carpetes públiques de l’equip.  

## Veure els recursos compartits

### A través de l'interfície gràfica

Per **conèixer els permisos** que té un recurs, es poden seguir els passos que es mostren a continuació:

1. Connecteu-vos al recurs dins de l’administració d’equips.
2. Expandiu Eines de sistema, Carpetes compartides i cliqueu a Recursos compartits.
3. Cliqueu amb el botó dret al recurs que vulgueu examinar i cliqueu a Propietats.
4. La fitxa Permisos dels recursos compartits us mostrarà l’usuari o grups d’usuaris que tenen accés al recurs i com és aquest accés. Aquesta fitxa permet modificar els permisos existents.

**IMATGE**

### A través de comandes

Executant la a comanda ```net share``` permet veure les unitats que tenim compartides en l’equip actual.
  
![](/assets/win-netshare.png)






## Accedir a carpetes compartides

* Si l'**usuari** autentificat a la màquina client està **reconegut** per la màquina servidor i té accés al recurs, aquest es podrà connectar.

* Sinó és possible que demani un usuari i contrasenya que sigui reconegut pel servidor.

* Si volem que es pugui connectar qualsevol usuari caldrà donar permisos a l'usuari convidat i, si cal, habilitar aquest usuari.






Per compartir recursos de l’equip podem fer servir:

1. L’explorador de Windows i fent botó dret del ratolí > **_Compartir amb_**

2. L’administració d’equips [_Computer Management_]

![](/assets/win-shares.png)

  Des de l’administració d’equips veiem això:
    
  * **Nom del recurs:** és el nom del recurs compartit.
  * **Ruta de la carpeta:** és la ruta sencera en el sistema local.
  * **Tipus:** és el tipus d’ordinador que pot utilitzar el recurs.
  * **Num. de connexions de client:** és la quantitat de clients que estan accedint al recurs en aquell precís moment.
  * **Descripció:** és la descripció del recurs.

3. El **Server Manager**, dins **_File and Storage Services > Shares_**

> IMATGE

  * **Nom del recurs compartit:** és el nom del recurs compartit.
  * **Ruta local:** és la ruta completa de la carpeta en el sistema local.
  * **Protocol:** és el nom del protocol utilitzat per compartir la carpeta.
  * **Espai lliure:** és la quantitat d’espai lliure en el disc si no hi ha quotes establertes.
  * **Quota:** és el resum de l’estat de les quotes de l’administrador de recursos sobre la carpeta compartida.

### Connexió a unitats de xarxa

Per connectar-se a una unitat de xarxa i accedir als recursos que conté, només cal executar l’ordre: 

  ```net use```

* Per exemple, si es vol accedir a un recurs amb l'etiqueta Imatges que s'emmagatzema en una màquina anomenada Multimedia i la lletra de la unitat és la d, cal escriure el següent:

  ```net use d: \\Multimedia\Imatges```

  







