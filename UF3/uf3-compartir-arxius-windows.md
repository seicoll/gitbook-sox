# Compartir arxius i carpetes en Windows

## Introducció

### Conceptes bàsics

Windows utilitza el protocol **CIFS** \(antigament anomenat **SMB**\) per compartir arxius, carpetes i impressores en un entorn en xarxa. També se'l sol anomenar **SMB/CIFS**.

**Propietari d'un arxiu o carpeta**

En Windows, cada carpeta i arxiu pertany a un usuari o a un grup d'usuaris, que és qui l'ha creat, però es pot canviar sempre que es tinguin els permisos per fer-ho.  
L'usuari o grup propietari, per defecte té tots els permisos.

**Permisos per arxius i carpetes**  
A part del propietari, es poden afegir altres usuaris i grups, i assignar permisos diferents.

> Si un usuari pertany a dos grups, se sumen els permisos dels dos grups.

**Permisos locals \(de seguretat o NTFS\)**  
Són els permisos que tindran els usuaris quan accedeixin als recursos \(arxius, carpetes i impressores\) de forma local.

**Herència**  
Quan es crea una carpeta, aquesta hereta els permisos de la carpeta pare, però aquesta dependència es pot trencar per canviar i posar els permisos adequats a cada cas.

### Recursos compartits

Un recurs compartit és un objecte al qual es pot accedir de forma remota.  
El recursos que es poden compartir són:

* **Arxius i carpetes**
* **Impressores**

El nom del recurs compartit \(el que s'ha d'utilitzar quan s'accedeix de forma remota\) pot ser diferent del nom real.

Recursos compartits per defecte en un domini

* **NETLOGON**: Conté els scripts d'inici de sessió. C:\Windows\SYSVOL\sysvol\domini\SCRIPTS
* **SYSVOL**: Conté els fitxers públics del domini. C:\Windows\SYSVOL\sysvol

### Compartició de carpetes

Quan es comparteixen carpetes, cal distingir entre permisos locals i permisos de compartició:

* **Permisos locals**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta local:
  * En Windows: C:\Usuari\Documents
* **Permisos de compartició**: s'apliquen quan l'usuari accedeix a l'arxiu o carpeta utilitzant una ruta remota:
  * En Windows: \Server\Compartida o X: \(suposant que X: és una unitat de xarxa connectada amb una carpeta remota\)

Quan es comparteix una carpeta, s'han de configurar els **permisos de compartició**.

Es poden assignar diferents permisos de compartició per usuaris i grups. Aquests permisos poden ser diferents dels permisos locals.

> Quan s'accedeix a un recurs **de forma local** només es tenen en compte els permisos locals, però quan s'accedeix a un recurs compartit **de forma remota** s'apliquen els permisos **més restrictius** entre els permisos locals i els permisos de compartició.
>
> Una forma de simplificar la gestió dels permisos quan es comparteixen arxius i carpetes és posar **Control total** als permisos de compartició i gestionar els permisos locals més detalladament.  
> Això no sempre es pot fer \(depén dels requeriments de seguretat\) però en la majoria de casos, sí.

## Gestió de permisos locals

Per configurar els permisos locals cal anar a les **propietats de la carpeta** i entrar a la pestanya _**Seguridad**_.

![](/assets/win-permisos-locals.png)

### Gestionar els usuaris

Es poden afegir o eliminar usuaris i grups fent clic al botó _**Editar**_.

### Gestionar els permisos simples

Seleccionant l'usuari o grup es poden marcar o desmarcar les caselles _**Permitir o Denegar**_ en cada permís.

Per defecte, si no està marcada la casella _**Permitir**_, implica que no es té el permís corresponent.

### Opcions avançades

Amb el botó _**Opciones avanzadas**_ es poden canviar algunes propietats avançades:

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

Abans de configurar els permisos de compartició que assegurar-se que s'ha [activat l'_**Ús compartit d’arxius i impressores**_](#activar-la-compartició-de-recursos)_**.**_

A continuació, per configurar els permisos de compartició cal anar a les **propietats de la carpeta** i entrar a la pestanya _**Compartir**_.

![](/assets/win-permisos-compartits.png)

> Un cop s'hagi compartit la carpeta, la ruta que s'ha d'utilitzar per accedir de forma remota és la que apareix a _**Ruta de acceso de red:**_ `\\\WIN-SOX\Compartida`.

### Compartició senzilla

Amb el botó _**Compartir**_, s'accedeix a les opcions per compartir la carpeta de forma senzilla.  
Només es poden afegir o eliminar **usuaris i grups**, i assignar-los permisos de **Lectura **o de **Lectura i escriptura**.

![](/assets/win-permisos-compartits-simple.png)

### Compartició avançada

Amb el botó _**Uso compartido avanzado**_, s'accedeix a les opcions per compartir la carpeta de forma avançada.

![](/assets/win-permisos-compartits-avansats1.png)

En aquest cas es disposa de més opcions per configurar la compartició:

* Marcar o desmarcar la casella _**Compartir esta carpeta**_ per compartir-la o deixar-la de compartir.
* Posar-li un **nom de recurs** compartir diferent del nom original. Aquest nom és el què s'ha d'utilitzar quan es vol accedir a aquest recurs de forma remota.
* Es pot establir el **nombre màxim d'usuaris** que poden utilitzar la carpeta simultàniament.
* Els **permisos** que es poden assignar són diferents: _**Llegir, Canviar i Control total**_.

![](/assets/win-permisos-compartits-avansats2.png)

> Es pot simplificar la configuració de permisos de compartició posant **Control total** a _**Compartició**_ i gestionar els permisos més detalladament a _**Seguretat**_.  
> En alguns casos no es podrà fer així: per exemple, si es vol que els usuaris tinguin permís de lectura i escriptura quan accedeixin localment però només de lectura quan ho facin de forma remota.

### Carpetes compartides ocultes

* Si es vol compartir un recurs però que **no sigui visible** \(només es podrà connectar qui conegui la ruta a aquest recurs\) només cal afegir un **$** darrera del nom del recurs.

  * Per exemple: C$

* Amb **\ip\_equip** o **\nom\_equip** es pot veure els recursos compartits visibles.

* Es pot accedir a un recurs compartit ocult si es conneix tota la ruta.

  * Per exemple: \192.168.0.1\C$

### Veure els permisos efectius

És fàcil cometre errors al combinar permisos locals amb permisos compartits, i sol ser difícil descobrir quins són els permisos que estan mal configurats.  
Per ajudar en aquesta tasca, es pot anar a permisos locals \(pestanya _**Seguridad**_\), clicar el botó _**Opciones avanzadas**_ i entrar a la pestanya **Acceso efectivo**.

Aquesta finestra permet comprovar quins permisos té un usuari i, en cas que no tingui un permís, saber si el problema està en la configuració dels permisos locals o en els permisos de compartició.

Primer cal **triar l'usuari o grup** i després clicar el botó _**Ver acceso efectivo**_.

![](/assets/win-permisos-efectius.png)

En les dues primeres columnes se indica si l'usuari o grup té o no un permís determinat.  
En cas que no el tingui, en la tercera columna se indica el motiu:

* **Permisos de archivo**: no s'ha donat permís en la configuració de **permisos locals**.
* **Compartir**: no s'ha donat permís en la configuració de **permisos de compartició**.

## Veure i gestionar les carpetes compartides

### A través de l'Administrador d'equips

Es poden veure tot el relacionat amb els recursos que està compartint la màquina a _**Administración de equipos \[Computer Management\]**_, dins l'apartat _**Herramientas del sistema &gt; Carpetas compartidas**_.

![](/assets/win-recursos-compartits.png)

**Recursos compartits**

En aquest apartat es poden veure la següent informació sobre els recursos compartits:

* **Nom del recurs:** és el nom del recurs compartit.
* **Ruta de la carpeta:** és la ruta sencera en el sistema local.
* **Tipus:** és el tipus d’ordinador que pot utilitzar el recurs.
* **Num. de connexions de client:** és la quantitat de clients que estan accedint al recurs en aquell precís moment.
* **Descripció:** és la descripció del recurs.

I també podem:

* Deixar de compartir-los
* Veure els permisos de compartició
* Veure els permisos locals

**Sessions**

Aquí es pot veure qui està accedint als recursos \(usuari o màquina\) i, si cal, tancar-li la sessió.

**Arxius oberts**

Mostra els arxius compartits que s'estan utilitzant i, si cal, es poden tancar.

### A través del Administrador del servidor

En l'_**Administrador del servidor \[Server Manager\]**_, dins de l'apartat _** Servicios de archivos i de almacenamiento \[File and Storage Services &gt; Shares\]**_.

![](/assets/win-recursos-compartits2.png)

* **Nom del recurs compartit:** és el nom del recurs compartit.
* **Ruta local:** és la ruta completa de la carpeta en el sistema local.
* **Protocol:** és el nom del protocol utilitzat per compartir la carpeta.
* **Espai lliure:** és la quantitat d’espai lliure en el disc si no hi ha quotes establertes.
* **Quota:** és el resum de l’estat de les quotes de l’administrador de recursos sobre la carpeta compartida.

### A través de comandes

Executant la a comanda `net share` permet veure les unitats que tenim compartides en l’equip actual.

![](/assets/win-netshare.png)

## Accedir a carpetes compartides

Una forma fàcil d'accedir a les carpetes compartides en una màquina és a través de l'explorador d'arxius.

A l'apartat _**Red **_ es poden veure les màquines de la mateixa xarxa.

Seleccionant qualsevol d'elles es veuran les carpetes que comparteixen.

Si no apareix la màquina però es coneix la màquina i el nom del recurs compartit, es pot escriure en la barra d'adreces:

```
\\NOM_SERVIDOR\Compartida o \\IP_SERVIDOR\Compartida
```

### Validació d'usuaris per accedir a carpetes compartides

Quan s'intenta accedir a una carpeta compartida, el sistema comprova si l'usuari i contrasenya amb el que s'ha accedit al sistema està reconegut per la màquina servidor i té accés al recurs, aquest es podrà connectar.

Si no es reconeix l'identificador de l'usuari, demanarà un usuari i contrasenya.

Si reconeix l'usuari i contrasenya, podrà accedir si té els permisos adequats. Un cop a dins podrà realitzar diferents accions en funció dels permisos que tingui: veure continguts, crear, modificar, esborrar...

Si volem que es pugui connectar qualsevol usuari caldrà donar permisos a l'usuari convidat i, si cal, habilitar aquest usuari.

### Connectar una unitat de xarxa a una carpeta compartida

Es pot connectar la carpeta compartida a una unitat de xarxa assignant-li una lletra d'unitat que estigui disponible.  
D'aquesta forma serà més fàcil accedir-hi, doncs apareixerà com una unitat d'emmagatzematge local.

Per fer la connexió, clicar amb el botó dret sobre Este equipo i triar l'opció Conectar a unidad de red.

* **Unitat:** triar una lletra d'unitat que estigui lliure \(X:\).
* **Carpeta:** escriure la ruta o buscar-la \(\NOM\_EQUIP\Compartida\).
* **Conectar de nuevo al iniciar sesión:** connectar la unitat a la carpeta cada cop que l'usuari inicïï sessió.
* **Conectar con otras credenciales:** connectar amb un usuari diferent de l'actual.

### Connectar una unitat de xarxa a través de comandes

Per connectar-se a una unitat de xarxa i accedir als recursos que conté, només cal executar l’ordre:

`net use`

Per **exemple**, si es vol accedir a un recurs anomenat _Compartida_ que s'emmagatzema en una màquina anomenada _Servidor_ i la lletra de la unitat és la d, cal escriure el següent:

`net use d: \\IP_SERVIDOR\Compartida`

## Problemes i altres configuracions

### Activar la compartició de recursos

Per activar l´ús compartit d'arxius i impressores cal el següent:

1. Cal anar al _**Centro de redes y recursos compartidos &gt; Cambiar configuración de uso compartido avanzado.**_
2. Activar l'opció _**Activar la detecció de xarxes.**_
3. Activar l’_**Ús compartit d’arxius i impressores**_.

Quan s'activa l’opció _**Ús compartit d’arxius i impressores**_, els usuaris de la xarxa podran tenir accés als arxius i impressores compartits en aquest equip.

![](/assets/win-activar-us-compartit.PNG)

