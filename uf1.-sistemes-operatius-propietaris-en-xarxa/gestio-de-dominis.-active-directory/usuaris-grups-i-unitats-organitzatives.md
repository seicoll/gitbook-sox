# Usuaris, grups i unitats organitzatives

## Objectes que administra un domini

Els objectes d'un domini són aquelles **entitats susceptibles de ser administrades en una xarxa d'ordinadors**.

El directori actiu no és més que una base de dades jerarquitzada d'objectes.

Els **objectes** que administra un domini són:

* **Usuaris globals**
  * Són usuaris reconeguts per tots els equips que formen part del domini.
  * Són gestionats pel Directori Actiu de forma centralitzada.
  * Permet identificar i autenticar els usuaris que poden accedir al sistema.
  * Permet gestionar els permisos d'aquests usuaris als recursos compartits. 
* **Grups** 
  * Els usuaris globals es poden assignar a grups.
  * Facilitar l'administració quan diversos usuaris tenen perfils de seguretat i accés comuns. 
* **Equips**
  * La base de dades del Directori Actiu també guarda informació dels diferents equips que pertanyen al domini.
  * Com per exemple el nom del ordinador així com un identificador únic que permet assignar drets i permisos.
* **Unitats organitzatives \(UO\)** 
  * Són objectes de directori que contenen altres objectes com usuaris, grups, equips o altres unitats organitzatives.

## Centre d'administració de Active Directory

El **centre d'administració de Active Directory** permet administrar els objectes de Active Directory de forma gràfica.

Per accedir-hi cal anar a _**Administrador del servidor &gt; Herramientas &gt; Centro de administración de Active Directory**_

En aquesta pantalla podrem administrar els usuaris globals, grups i equips del domini.

![](../../.gitbook/assets/ad_centre_administracio.png)

## Equips

La base de dades del Directori Actiu emmagatzema **un compte d'equip per cada un dels ordinadors** que formen part del domini.

* Les comptes d'equip dels DCs s'ubiquen a la unitat organitzativa \(UO\) anomenada "_**DomainControllers**_". 
* Les comptes de la resta d'equips s'ubiquen per defecte al contenidor "_**Computers**_" 

Tots dos contenidors se situen just a sota del contenidor que representa el domini.

Entre altres dades, el compte d'equip que cada ordinador té al domini inclou els següents atributs:

* **Nom de l'equip**. Coincideix amb el nom que l'equip té, sense comptar amb seu sufix DNS. 
* **Contrasenya**. Cada equip té una contrasenya que l'ordinador utilitza per acreditar-se en el domini, de forma anàloga als usuaris quan inicien sessió. 

Aquesta contrasenya es genera automàticament quan s'agrega l'equip al domini, i es canvia automàticament cada 30 dies.

## Usuaris

En un sistema en xarxa cada persona que tingui accés al sistema requereix d'un compte d'usuari que l'identifiqui amb **un nom únic de compte \(login\)** i una **contrasenya \(password\)**.

Un compte d'usuari fa possible:

* Autenticar la identitat de la persona que es connecta al sistema. 
* Controlar i validar l'accés als recursos mitjançant permisos.
* Auditar les accions efectuades per l'usuari.

Al Windows Server els usuaris poden ser de dos tipus:

* **Usuaris locals:** Són comptes d'usuari definides només per accedir a un equip determinat. No poden accedir al domini i per tant només concedeixen drets i permisos sobre l'equip on es crea i utilitza.

> Amb **usuaris locals**, si una persona ha de treballar en diversos ordinadors de l’organització, necessita posseir un compte d’usuari en cada un d’ells.

* **Usuaris globals o usuaris de domini:** Comptes d'usuari creades mitjançant el Directori Actiu. 
  * Les dades d’una compte d’usuari global, es guarden en el Directori Actiu i, per tant, són coneguts per tots els equips del domini.
  * Qualsevol ordinador de fa de DC - Domain Controller, pot crear comptes d’usuari de domini.

> Amb **usuaris de domini**, una persona pot validar-se amb el mateix compte d’usuari des de qualsevol ordinador integrat al domini i accedir als recursos de tot el domini.

### Usuaris locals

No és incompatible que els equips **clients d’un domini**, a més de conèixer els usuaris globals, tinguin també **els seus propis usuaris locals** que només són visibles en l’ordinador que han estat creats.

Els **usuaris locals** poden crear-se en qualsevol equip Windows Server **excepte en els equips controladors de domini** que gestionen els usuaris com globals a través del Directori Actiu.

Es poden **crear usuaris locals** en un equip anant a _**Inici &gt; Eines Administratives &gt; Administració del equip &gt; Eines del sistema &gt; Usuaris i grups locals**_.

### Usuaris globals

Els comptes d'**usuari del domini o usuaris globals** s'emmagatzemen en el directori actiu i per tant són coneguts per tots els ordinadors del domini.

#### Inici de sessió

L’**inici de sessió** al domini utilitzant un usuari global por fer-se de dues formes:

* Nom NetBios del domini seguit del símbol “\” i nom d’usuari: 

`BOSCCOMA\sergi`

* Identificador d’usuari seguit del símbol “@” i el nom de domini:

`sergi@bosccoma.local`

A l'inici de sessió en qualsevol **equip del domini** utilitzant un compte d'usuari global, l'ordinador en qüestió realitzarà una **consulta al Directori Actiu** per validar les credencials de l'usuari. El resultat de la validació és enviat a l'equip on s'està iniciant la sessió, concedint o rebutjant la connexió.

#### Creació d'usuaris globals

1. Ves a l’_**Administrador del servidor &gt; Herramientas &gt; Centro de administración de Active Directory**_
2. Situa't **sobre l'arrel del domini o una unitat organitzativa** on vulguis crear l'usuari i en el menú de la dreta selecciona l'opció **Nou &gt; Usuari**.

![](../../.gitbook/assets/ad_usuri_nou.png)

Les dades d'un usuari es divideixen en diferents seccions:

* _**Cuenta**_: Nom d’inici de sessió, restricció d’inici de sessió, opcions de contrasenya, caducitat del compte i dies hores en què pot iniciar sessió.
* Hores de inici de sessió, podem indicar a quines hores cada usuari podrà connectar-se.
* _**Miembro de**_: A quins grups pertany l'usuari.
* _**Perfil**_: permet configurar alguns paràmetres del perfil, com ara la carpeta on es guarden els perfils, una carpeta personal o un script d'inici de sessió.
* _**Control remoto**_: permet habilitar el control remot de la sessió del usuari.

En la secció _**Cuenta**_ introduirem:

* _**Nombre**_ i _**Apellidos**_: Nom de l'usuari \(que no és el login\) i les inicials per identificar l’usuari. 
* _**Nombre completo**_: s’omplirà automàticament. 
* _**Inicio de sesión UPN de usuario**_: El login de usuari que ens permetrà iniciar sessió al sistema \(ja sigui des d’un client o des del propi servidor\).

Altres opcions de la compte d'usuari:

* **L’usuari ha de canviar la contrasenya en el següent inici de sessió**. 
  * Si activem aquesta opció, quan l’usuari es connecti per primera vegada li exigirà un canvi obligatori de contrasenya. Li demanarà la contrasenya anterior \(per tant l’haurà de conèixer i la nova.
* **L'usuari no pot canviar la contrassenya**.
  * A diferència del cas anterior, ara l’administrador sí que coneix la clau d’accés del nou usuari. En el cas anterior, l’administrador coneixerà la primera clau \(l’haurà donada ell\) però quan el usuari la canviï no coneixerà el nou password. Aquest fet no afecta per res a la gestió que l’administrador faci de les contrasenyes, ja que, encara que no la conegui, la podrà modificar i fins i tot borrar. 
* **La contrasenya mai caduca**.
  * Si no marquem aquesta casella, la contrasenya caducarà, per defecte, al cap de 42 dies.
* **Hores d'inici de sessió**

  * Permet definir els dies i hores en els que pot iniciar sessió.  

  ![](../../.gitbook/assets/ad_usuari_hores.png)

També podem realitzar **tasques** en un compte, com eliminar-lo, deshabilitar-lo, restablir contrassenya, etc.

* **Tasques &gt; Deshabilitar**. 
  * Serveix per deshabilitar una compte temporalment. Permet que un usuari no es pugui connectar sense haver d’esborrar el compte amb totes les dades que contenia. 
* **Tasques &gt; Restablir contrassenya**
  * Serveix per canviar la contrasenya a un usuari. Es sol utilitzar quan un usuari no recorda la seva contrasenya. 

> Les **contrasenyes** en **Windows Server** han de tenir un mínim de 7 caràcters amb al menys una lletra majúscula, una minúscula i un número.

#### Creació de plantilles d'usuaris

Una de les tasques més repetitives en l’administració de Sistemes Operatius és la creació de comptes d’usuari que acostumen a tenir molts valors de configuració similars.

Les **plantilles de comptes d’usuaris** ens ajuden en aquesta tasca ja que són comptes d’usuari estàndard creades amb les propietats que s’apliquen a usuaris amb necessitats comunes.

**Com utilitzar plantilles**:

1. En primer lloc es crea un compte d’usuari normal amb tots els valors de configuració, permisos, pertinences a grups, etc. corresponents a un tipus d’usuari en concret. Per exemple “professors” i guardem aquest compte amb un nom com _**Plantilla\_Professor**_.
2. Cada vegada que haguem de donar d’alta un professor, **farem un còpia d’aquest usuari** i així el nou usuari agafa tota la configuració original de la plantilla excepte el nom, l'identificador i la contrasenya.
3. Finalment, **personalitzem el nou compte** amb el nom, cognoms, contrasenya, etc. particulars però la resta de treball de configuració ja estarà realitzat.

#### Configurar varis usuaris simultàniament

Algunes opcions de les propietats d'un usuari es poden modificar en diversos usuaris simultàniament. Per fer-ho només cal seleccionar tots els usuaris en els que es vulgui canviar algun paràmetre, i amb el botó secundari triar l'opció _**Propiedades**_.

Només es veuen algunes seccions de la compte d'ususari perquè no es poden canviar totes les propietats per diversos usuaris simultàniament \(algunes propietats, com per exemple el nom, identificador... no es poden repetir en més d'un usuari\).

Per poder canviar una propietat, abans cal seleccionar la casella que hi ha al davant. Després, els canvis que es facin en aquesta propietat s'aplicaran a tots els usuaris seleccionats, mentre que les que no s'hagin marcat quedaran sense modificar \(cada usuari mantindrà les que tenia\).

![](../../.gitbook/assets/ad_usuaris_varis.png)

## Grups

De forma similar als usuaris, hi ha **grups d’usuaris** que són emmagatzemats en el **Directori Actiu** i que per tant són visibles des de tots els ordinadors del domini.

Els **grups d’usuaris** s’utilitzen per simplificar la gestió de permisos sobre els recursos del domini.

Els **membres d’un grup d’usuaris** poden ser:

* Usuaris
* Equips 
* Altres grups d’usuaris

Windows Server té creats una sèrie de **grups d’usuaris predefenits** \(_**Tots**_, _**Administradors**_, _**Equips del domini**_, etc.\)

> Un usuari ha de pertànyer com a mínim a un grup, però pot pertànyer a més d'un.

### Tipus de grups

Al directori actiu es poden crear **dos tipus de grups**:

* **Grups de seguretat**
  * Aquests tipus de grups s'utilitzen per assignar permisos d’utilització de recursos del domini i així no cal fer-ho usuari per usuari.
  * És l'opció per defecte.
* **Grups de distribució**:
  * Aquets tipus de grups s'utilitzen per realitzar instal·lacions remotes de software en els equips client on es validin els usuaris del grup.

> Nosaltres utilitzarem, únicament, els grups de seguretat.

### Àmbit del grup

Quan es crea un grup se li assigna un **àmbit** que determini la visibilitat dins del domini.

En dominis Windows Server els grups es poden definir en tres àmbits diferents:

* **Grups d'àmbit local**: 
  * Només són visibles en el domini en què es creen. 
  * Només es poden assignar permisos sobre **recursos del mateix domini** en el que es crea el grup.
* **Grups d'àmbit global**: 
  * Són visibles en tots els dominis del bosc. Els permisos concedits a aquest grup tenen validesa en qualsevol domini.
  * Només se li poden assignar permisos sobre **recursos que pertanyin a dominis del bosc**.
* **Grups d'àmbit universal**: 
  * Són visibles a tot el bosc. 
  * Poden tenir membres procedents de qualsevol domini.
  * Se li poden assignar permisos sobre **recursos de qualsevol domini o bosc.**

### Creació de grups

1. Ves a l’_**Administrador del servidor &gt; Herramientas &gt; Centro de administración de Active Directory**_.
2. Situa't **sobre l'arrel del domini o una unitat organitzativa** on vulguis crear grup i al menú de la dreta selecciona l'opció **Nou &gt; Grup**. 
3. Ara has d'**introduir el nom del grup** i seleccionar l'**àmbit** i el **tipus** de grup.

![](../../.gitbook/assets/adnewgroup.png)

### Gestió de grups

Les opcions més importatns que podem fer amb un grup, a part de poder esborrar o moure un grup, es troben a **Propiedades**:

* **Miembros:** en aquesta secció es poden veure els membres que pertanyen a aquest grup i també es poden afegir altres membres o treure'ls del grup.
* **Miembro de:** serveix per veure a quins grups pertany aquest grup i afegir-lo a altres grups o treure'l.

![](../../.gitbook/assets/adnewgroupmember.png)

## Unitats Organitzatives \(UO\)

Les **unitats organitzatives \(OU\)** són objectes contenidors del directori actiu que agrupen altres objectes com a usuaris, grups, equips i altres unitats organitzatives.

El seu **objectiu** és permetre **ordenar el conjunt d'objectes del directori** agrupant-los de forma organitzada \(per exemple per departaments, seus, delegacions , etc.\).

> Els objectes d'una unitat organitzativa poden moure a una altra però **mai duplicar ja que cada objecte és únic al directori**.

En una UO podem posar-hi:

* Equips
* Grups
* Impresores
* Usuaris
* Altres Unitats Organitzatives \(UO\)

Les seves principals **funcions** són :

* Representar estructures jeràrquiques existents dins de la pròpia organització com alternativa als dominis. 
* Permetre l'**aplicació de directrius** per personalitzar el comportament d'usuaris i equips definint així polítiques de grup comuns a usuaris, grups i equips ubicats en una determinada unitat organitzativa. 
* **Delegar l'administració** dels seus objectes a altres usuaris diferents a l'administrador de domini. 
  * **Per exemple**: podem fer que un usuari no administrador pugui donar d’alta usuaris d’un determinat departament.

> En les organitzacions de mida reduïda , és preferible implementar un model de **domini únic amb diferents unitats organitzatives d'administració delegada** i comportament diferent, que utilitzar un model de múltiples dominis.

### Unitats organitzatives predeterminades

Les principals unitats organitzatives que ja estan creades són:

* **Builtin:** conté els grups locals
* **Computers:** les màquines unides al domini
* **Domain Controllers:** els controladors de domini
* **Users:** usuaris i grups per defecte del domini

Per evitar barrejar els usuaris i grups de l'empresa amb els que ja té Windows per defecte, pot ser convenient crear una unitat organitzativa en el primer nivell \(just per sota de l'arrel del domini\) i crear a dins les nostres pròpies unitats organitzatives \(Grups i Usuaris\).

### Creació d'Unitats Organitzatives \(UO\)

La creació d'unitats organitzatives és molt senzilla:

1. Ves a l’_**Administrador del servidor &gt; Herramientas &gt; Centro de administración de Active Directory**_.
2. Situa't **sobre l'arrel del domini o una unitat organitzativa** on vulguis crear grup i al menú de la dreta selecciona l'opció **Nou &gt; Unitat Organitzativa**. 
3. Ara has d'**introduir el nom de la nova unitat organitzativa** i per defecte deixar marcada l'opció de _Protegir contenidor contra esborrat accidental_. 
4. Apareixerà un nou contenidor al menú i ara ja pots **crear nous objectes** \(usuaris, grups, equips, etc.\) en aquesta nova unitat organitzativa **o bé moure objectes ja existents** senzillament arrossegant des d'altres contenidors.

> Per poder **esborrar o moure la Unitat Organitzativa** cal prémer sobre Ver i activar l’opció _Característiques avançades_. Després a les _Propietats_ de la UO apareix una pestanya _Objecte_ on es pot desactivar la casella _Protegir contenidor contra esborrat accidental_. I ara sí es pot eliminar la UO.

## Documentació i recursos

* **MSDN: Ámbito de grupo.**  [https://msdn.microsoft.com/es-es/library/cc755692.aspx](https://msdn.microsoft.com/es-es/library/cc755692.aspx)

