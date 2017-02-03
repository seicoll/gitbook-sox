# Usuaris, grups i unitats organitzatives

## Objectes que administra un domini

Els objectes d'un domini són aquelles **entitats susceptibles de ser administrades en una xarxa d'ordinadors**. 

El directori actiu no és més que una base de dades jerarquitzada d'objectes. 

Els **objectes **que administra un domini són: 

* **Usuaris globals** 
  * Són usuaris reconeguts per tots els equips que formen part del domini.
  * Són gestionats pel Directori Actiu de forma centralitzada.
  * Permet identificar i autenticar els usuaris que poden accedir al sistema.
  * Permet gestionar els permisos d'aquests usuaris als recursos compartits. 

* **Grups **

  * Els usuaris globals es poden assignar a grups.
  * Facilitar l'administració quan diversos usuaris tenen perfils de seguretat i accés comuns. 

* **Equips** 
  * La base de dades del Directori Actiu també guarda informació dels diferents equips que pertanyen al domini.
  * Com per exemple el nom del ordinador així com un identificador únic que permet assignar drets i permisos.


* **Unitats organitzatives (UO)** 
  * Són objectes de directori que contenen altres objectes com usuaris, grups, equips o altres unitats organitzatives.


## Eines per a l’administració del domini

Per accedir a les eines que permeten la gestió del Directori Actiu cal anar a _**Administrador del servidor > Herramientas > Usuarios y equipos de Active Directory**_

En aquesta pantalla podrem administrar els usuaris globals, grups i equips del domini.

![Usuarios y equipos de Active Directory](/assets/users_active_directori.png)

## Equips

La base de dades del Directori Actiu emmagatzema **un compte d'equip per cada un dels ordinadors** que formen part del domini. 

* Les comptes d'equip dels DCs s'ubiquen a la unitat organitzativa (UO) anomenada "_**DomainControllers**_". 
* Les comptes de la resta d'equips s'ubiquen per defecte al contenidor "_**Computers**_" 

Tots dos contenidors se situen just a sota del contenidor que representa el domini.

Entre altres dades, el compte d'equip que cada ordinador té al domini inclou els següents atributs: 
* **Nom de l'equip**. Coincideix amb el nom que l'equip té, sense comptar amb seu sufix DNS. 
* **Contrasenya**. Cada equip té una contrasenya que l'ordinador utilitza per acreditar-se en el domini, de forma anàloga als usuaris quan inicien sessió. 

Aquesta contrasenya es genera automàticament quan s'agrega l'equip al domini, i es canvia automàticament cada 30 dies.

## Comptes d'usuari

En un sistema en xarxa cada persona que tingui accés al sistema requereix d'un compte d'usuari que l'identifiqui amb **un nom únic de compte (login)** i una **contrasenya (password)**. 

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

Es poden **crear usuaris locals** en un equip anant a _**Inici > Eines Administratives > Administració del equip > Eines del sistema > Usuaris i grups locals**_.

> IMATGE

### Usuaris globals

Els comptes d'**usuari del domini o usuaris globals** s'emmagatzemen en el directori actiu i per tant són coneguts per tots els ordinadors del domini.

L’**inici de sessió** al domini utilitzant un usuari global por fer-se de dues formes:
* Nom NetBios del domini seguit del símbol “\” i nom d’usuari: 

`BOSCCOMA\sergi`

* Identificador d’usuari seguit del símbol “@” i el nom de domini:

`sergi@bosccoma.local`
        
A l'inici de sessió en qualsevol **equip del domini** utilitzant un compte d'usuari global, l'ordinador en qüestió realitzarà una **consulta al Directori Actiu** per validar les credencials de l'usuari.
El resultat de la validació és enviat a l'equip on s'està iniciant la sessió, concedint o rebutjant la connexió.

#### Creació d'usuaris globals

1. Ves a l’_**Administrador del Servidor > Usuaris i equips de Active Directory.**_
2. Situa't **sobre l'arrel del domini o una unitat organitzativa** on vulguis crear l'usuari i obre el menú contextual amb el botó dret del ratolí. 
3. Selecciona l'opció **Nou > Usuari**.

![Nou usuari](/assets/usuari_nou.png)

En aquesta pantalla introduirem: 
* **_Nombre de pila_** i **_Apellidos_**: No de l'usuari (que no és el login) i les inicials per identificar l’usuari. 
* _**Nombre completo**_: s’omplirà automàticament. 
* _**Nombre de inicio de sesión de usuario**_: El login de usuari que ens permetrà iniciar sessió al sistema (ja sigui des d’un client o des del propi servidor).
* _**Nombre de inicio anterior a Windows 2000**_: Aquesta opció serveix per tal que l’usuari pugui iniciar sessió en un domini Windows NT4.0 Server amb el que s’han establert relacions de confiança. 

Premem **_Siguiente_** i apareix una pantalla de **contrasenyes: **

![Nou usuari](/assets/usuari_contrassenyes.png)

Disposem de diverses opcions: 
* **L’usuari ha de canviar la contrasenya en el següent inici de sessió**. 
  * Si activem aquesta opció, quan l’usuari es connecti per primera vegada li exigirà un canvi obligatori de contrasenya. Li demanarà la contrasenya anterior (per tant l’haurà de conèixer i la nova.
* **L´usuari no pot canviar la contrassenya**.
  * Per poder activar aquest check-box haurem de desactivar l’anterior.
  * A diferència del cas anterior, ara l’administrador sí que coneix la clau d’accés del nou usuari. En el cas anterior, l’administrador coneixerà la primera clau (l’haurà donada ell) però quan el usuari la canviï no coneixerà el nou password. Aquest fet no afecta per res a la gestió que l’administrador faci de les contrasenyes, ja que, encara que no la conegui, la podrà modificar i fins i tot borrar. 
* **La contrasenya mai caduca**. 
  * Si no marquem aquesta casella, la contrasenya caducarà, per defecte, al cap de 42 dies. 
* **Compte deshabilitat**. 
  *Permet que un usuari no es pugui connectar sense haver d’esborrar el compte amb totes les dades que contenia. Això es fa quan volem denegar l’accés temporalment.

> Les **contrasenyes **en **Windows Server** han de tenir un mínim de 7 caràcters amb al menys una lletra majúscula, una minúscula i un número.

#### Modificació d'usuaris globals

Un cop creats els usuaris es poden fer moltes modificacions.
Seleccionem compte la que volem modificar i amb botó dret farem **propiedades**.

![Usuaris propietats](/assets/user_propietats.png)

Això és el que podem fer a les pestanyes més significatives:
* **_General_**: Dades identificatives del usuari.
* **_Cuenta_**: Nom d’inici de sessió, restricció d’inici de sessió, opcions de contrasenya, caducitat del compte i dies hores en què pot iniciar sessió.
  * Hores de inici de sessió, podem indicar a quines hores cada usuari podrà connectar-se.
* **_Miembro de_**: A quins grups pertany l'usuari.
* **_Perfil_**: permet configurar alguns paràmetres del perfil, com ara la carpeta on es guarden els perfils, una carpeta personal o un script d'inici de sessió.
* **_Control remoto_**: permet habilitar el control remot de la sessió del usuari.

### Creació de plantilles d'usuaris

Una de les tasques més repetitives en l’administració de Sistemes Operatius és la creació de comptes d’usuari que acostumen a tenir molts valors de configuració similars.

Les **plantilles de comptes d’usuaris** ens ajuden en aquesta tasca ja que són comptes d’usuari estàndard creades amb les propietats que s’apliquen a usuaris amb necessitats comunes.

**Com utilitzar plantilles**:

  1. En primer lloc es crea un compte d’usuari normal amb tots els valors de configuració, permisos, pertinences a grups, etc. corresponents a un tipus d’usuari en concret. Per exemple “professors” i guardem aquest compte amb un nom com **_Plantilla_Professor_**.
  
  2. Cada vegada que haguem de donar d’alta un comercial, **farem un còpia d’aquest usuari** i així el nou usuari hereda tota la configuració original de la plantilla.
  
  3. Finalment, **personalitzem el nou compte** amb el nom, cognoms, contrasenya, etc. particulars però la resta de treball de configuració ja estarà realitzat.

## Grups 

De forma similar als usuaris, hi ha **grups d’usuaris** que són emmagatzemats en el **Directori Actiu** i que per tant són visibles des de tots els ordinadors del domini.

Els **grups d’usuaris** s’utilitzen per simplificar la gestió de permisos sobre els recursos del domini.

Els **membres d’un grup d’usuaris** poden ser:
* Usuaris
* Equips 
* Altres grups d’usuaris

Windows Server té creats una sèrie de **grups d’usuaris predefenits** (_**Tots**_, **_Administradors_**, **_Equips del domini_**, etc.)

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

En dominis Windows Server els grups es poden definir en **tres àmbits** diferents: 
* **Grups d’àmbit local**: 
  * Només són visibles en el domini en què es creen. 
  * Només es poden assignar permisos sobre recursos del mateix domini en el que es crea el grup.
* **Grups d’àmbit global**: 
  * Són visibles en tots els dominis del bosc. 
  * Poden contenir usuaris del mateix domini i els permisos concedits a aquest grup tenen validesa en qualsevol domini.
* **Grups d’àmbit universal**: 
  * Són visibles a tot el bosc. 
  * Poden tenir membres procedents de qualsevol domini.
  
### Creació de grups

1. Ves al **_Administrador del Servidor > Usuaris i equips del Directori Actiu_**.
2. Situa't **sobre l'arrel del domini o una unitat organitzativa** on vulguis crear grup i obre el menú contextual amb el botó dret del ratolí. 
3. Selecciona l'opció **Nou > Unitat Organitzativa**. 
4. Ara has d'**introduir el nom del grup** i seleccionar l'**àmbit** i el **tipus **de grup.

## Unitats Organitzatives (UO)

Les **unitats organitzatives (OU)** són objectes contenidors del directori actiu que agrupen altres objectes com a usuaris, grups, equips i altres unitats organitzatives. 

El seu **objectiu** és permetre **ordenar el conjunt d'objectes del directori** agrupant-los de forma organitzada (per exemple per departaments, seus, delegacions , etc.).

> Els objectes d'una unitat organitzativa poden moure a una altra però **mai duplicar ja que cada objecte és únic al directori**. 

En una UO podem posar-hi:
* Equips
* Grups
* Impresores
* Usuaris
* Altres Unitats Organitzatives (UO)

Les seves principals **funcions** són : 
* Representar estructures jeràrquiques existents dins de la pròpia organització com alternativa als dominis. 
* Permetre l'**aplicació de directrius** per personalitzar el comportament d'usuaris i equips definint així polítiques de grup comuns a usuaris, grups i equips ubicats en una determinada unitat organitzativa. 
* **Delegar l'administració **dels seus objectes a altres usuaris diferents a l'administrador de domini. 
  * **Per exemple**: podem fer que un usuari no administrador pugui donar d’alta usuaris d’un determinat departament.

> En les organitzacions de mida reduïda , és preferible implementar un model de **domini únic amb diferents unitats organitzatives d'administració delegada** i comportament diferent, que utilitzar un model de múltiples dominis.

### Creació d'Unitats Organitzatives (UO)

La creació d'unitats organitzatives és molt senzilla: 

1. Ves al **_Administrador del Servidor > Usuaris i equips del Directori Actiu_**.
2. Situa't **sobre l'arrel del domini o una altra unitat organitzativa** on vulguis crear la unitat organitzativa i obre el menú contextual amb el botó dret del ratolí. 
3. Selecciona l'opció **Nou > Unitat Organitzativa**. 
4. Ara has d'**introduir el nom de la nova unitat organitzativa** i per defecte deixar marcada l'opció de _Protegir contenidor contra esborrat accidental_. Prem Acceptar. 
5. Apareix un nou contenidor al menú d'usuaris i equips de Directori Actiu. Ja pots **crear nous objectes** (usuaris, grups, equips, etc.) en aquesta nova unitat organitzativa **o bé moure objectes ja existents** senzillament arrossegant des d'altres contenidors.

> Per poder **esborrar l'Unitat Organitzativa** cal prémer sobre Ver i activar l’opció _Característiques avançades_. Després a les _Propietats_ de la UO apareix una pestanya _Objecte_ on es pot desactivar la casella _Protegir contenidor contra esborrat accidental_. I ara sí es pot eliminar la UO.
