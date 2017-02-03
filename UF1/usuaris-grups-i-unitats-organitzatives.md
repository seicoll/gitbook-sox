# Usuaris, grups i unitats organitzatives

## Objectes que administra un domini

Els objectes d'un domini són aquelles **entitats susceptibles de ser administrades en una xarxa d'ordinadors**. 

El directori actiu no és més que una base de dades jerarquitzada d'objectes. 

Els **objectes **que administra un domini són: 

* **Usuaris globals** 
  * Són usuaris reconeguts per tots els equips que formen part del domini.
  * Són gestionats pel Directori Actiu de forma centralizada.
Permet identificar i autenticar els usuaris que poden accedir al sistema.
Permet gestionar els permisos d'aquests usuaris als recursos compartits. 


* **Grups **

  * Els usuaris globals es poden assignar a grups.
  * Facilitar l'administració quan diversos usuaris tenen perfils de seguretat i accés comuns. 


* **Equips** 
  * La base de dades del Directori Actiu també guarda informació dels diferents equips que pertanyen al domini.
  * Com per exemple el nom del ordinador així com un identificador únic que permet assignar drets i permisos.


* **Unitats organitzatives (UO)** 
  * Són objectes de directori que contenen altres objectes com usuaris, grups, equips o altres unitats organitzatives.


## Eines per a l’administració del domini

Per accedir a les eines que permeten la gestió del Directori Actiu cal anar a _**Inici > Eines administratives**_

Aquí trobarem l’opció _**Usuaris i equips de Active Directory**_ on podrem administrar els usuaris globals, grups i equips del domini.

> Imatge

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


## Grups 

De forma similar als usuaris, hi ha **grups d’usuaris** que són emmagatzemats en el **Directori Actiu** i que per tant són visibles des de tots els ordinadors del domini.

Els **grups d’usuaris** s’utilitzen per simplificar la gestió de permisos sobre els recursos del domini.

Els **membres d’un grup d’usuaris** poden ser usuaris, equips o altres grups d’usuaris.

Windows Server té creats una sèrie de grups d’usuaris predefenits (“Tots”, “Administradors”, ”Equips del domini”, etc.)

### Tipus de grups

Al directori actiu es poden crear **dos tipus de grups**: 

* **Grups de seguretat**: s'utilitzen per assignar permisos d’utilització de recursos del domini.
* **Grups de distribució**: s'utilitzen per realitzar instal·lacions remotes de software en els equips client on es validin els usuaris del grup.
Nosaltres veurem únicament els primers.

### Àmbit del grup

Quan es crea un grup se li assigna un **àmbit** que determini al visibilitat dins del domini.
En dominis Windows Server els grups es poden definir en tres àmbits diferents: 
* **Grups d’àmbit local**: 
  * Només són visibles en el domini en què es creen. 
  * Els permisos concedits només són efectius per recursos del domini en el que es crea el grup.
* **Grups d’àmbit global**: 
  * Són visibles en tots els dominis del bosc. 
  * Poden contenir usuaris del mateix domini i els permisos concedits a aquest grup tenen validesa en qualsevol domini.
* **Grups d’àmbit universal**: 
  * Són visibles a tot el bosc. 
  * Poden tenir membres procedents de qualsevol domini.

## Unitats Organitzatives (UO)

Les **unitats organitzatives (OU)** són objectes contenidors del directori actiu que agrupen altres objectes com a usuaris, grups, equips i altres unitats organitzatives. 

El seu **objectiu **és permetre **ordenar el conjunt d'objectes del directori** agrupant-los de forma organitzada (per exemple per departaments, seus, delegacions , etc.).

Els objectes d'una unitat organitzativa poden moure a una altra però **mai duplicar doncs cada objecte és únic al directori** i independent de la unitat organitzativa a la qual pertanyi. 

En una UO podem posar-hi:
* Equips
* Contactes
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