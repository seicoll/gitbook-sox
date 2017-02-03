# Introducció als dominis

## Grup de treball

L’agrupació d'equips informàtics en xarxes té com a objectiu l'intercanvi d'informació i la compartició de recursos. 

Es pot gestionar de dues formes:
* **Grups de treball (Workgroup)**: En els grups de treball cada usuari administra els recursos del seu propi equip, decidint la política d'accessos, la seguretat i els recursos que vol compartir.
* **Dominis**: Permeten una organització més segura i d'administració centralitzada.

Els **grups de treball** són útils en xarxes petites per la seva senzillesa d'ús.

Amb un augment de la mida de la xarxa, la complexitat de l'administració es fa necessari la gestió centralitzada i l'administració basada en **dominis**.

> **Domini**: conjunt d’equips connectats entre ells que comparteixen informació administrativa (usuaris, grups, contrasenyes...) centralitzada, una política de seguretat i una base de dades comú.

## Directori Actiu [_Active Directory (AD)_] 

Els l'àmbit dels sistemes operatius en xarxa el concepte de **Directori **fa referència a un magatzem de dades estructurat que emmagatzema la informació sobre els diferents objectes de la xarxa.

El **Directori Actiu [_Active Directory (AD)_]** és el directori implementat en les xarxes de la família Microsoft Windows Server.

El **AD **emmagatzema la informació necessària de la xarxa: 
* comptes d'usuari, grups i perfils d’usuaris.
* equips i impressores
* directives de seguretat, recursos, aplicacions, etc.

El **AD **permet accés i autentificació dels usuaris i control d'accés als recursos compartits.

El **AD **és la eina que permet organitzar, controlar i administrar de forma centralitzada l’accés als recursos de la xarxa.

> El **Directori Actiu (AD)** és, per tant, una eina fonamental d’administració de tota la infraestructura informàtica d’una empresa o organització.

![Active Directory](/assets/ActiveDirectory.png)

## Controlador de domini i clients

Quan instal·lem el **Directori Actiu [_Active Directory_]** en un (o varis) equips de la nostra xarxa, convertim aquests equips en servidors de domini, els anomenats **controladors de domini [_Domain Controlers_]**.

Cada domini ha de tenir **com a mínim un controlador de domini principal**, però pot tenir més d'un per dues raons: 
* seguretat (les dades estan replicades)
* rendiment (es pot repartir la càrrega entre els diferents servidors)

La resta d’equips de la xarxa actuen com a **clients **d’aquest servei de directori i reben tota la informació guardada als controladors de domini (compte d’usuari, grups, etc).

Un **controlador de domini** és una part essencial dels sistemes operatius de Microsoft. 
* S’encarrega fonamentalment d’emmagatzemar les parelles usuari contrasenya dels comptes d’usuari que tenen accés al domini de xarxa. 
* Aquest controlador centralitza la funció d’autenticar l’accés al domini.

## Noms de domini

El** Active Diretory (AD)** es basa en en el servei de noms de domini (**DNS**).

**DNS **és un servei de xarxa que tradueix els noms dels dominis a direccions IP.

El **Active Diretory (AD)** utilitza el servei de noms de domini (**DNS**), que caldrà instal·lar en el servidor, per resoldre els nom de la màquina per la seva adreça IP. 

Mitjançant el DNS un equip que es connecta en xarxa pot trobar el **controlador de domini _[Domain Controller (DC)]_**.
* A les màquines client posarem la IP del servidor com a servidor DNS a la configuració de la xarxa.

Cada **domini **de Windows Server queda identificat únivocament per un nom DNS. Per exemple:

`bosccoma.local`

Cada **equip **que forma part d’un domini tindrà la categoria de subdomini i tindrà un nom DNS amb sufix el nom DNS del domini. Per exemple:

`equip1.bosccoma.local`

## Estructura lògica. Domini, Arbre, Bosc

L’estructura del servei de directori està constituïda per diferents elements: 
* **Objecte**: Entitats en el directori (usuaris, ordinadors, encaminadors, impressores, ...).
* **Domini (_Domain_)**: És l'element central i consisteix bàsicament en un conjunt d'objectes identificats per un nom de tipus DNS (Domain Name System).
* **Arbre**: És un conjunt de dominis que s’estructuren jeràrquicament i comparteixen recursos, clients i un sistema de resolució de noms. 
* **Bosc (_Forest_)**: Si el conjunt de dominis no comparteixen un nom d’arrel comú, s’anomen bosc. Per tant, un bosc és un conjunt d’arbres de domini.

Els boscos poden compartir informació mitjançant **relacions de confiança**. Aquestes relacions establertes entre dos dominis permeten als usuaris d'un domini ser reconeguts pels controladors de domini (DC) d'un altre domini.
Aquesta estructura facilita la cerca i l'accés als recursos dins de l'arbre formant un espai que compateix un nom d'arrel únic. 

Per exemple:
* cendrassos.local i aula1.cendrassos.local és un arbre AD amb 2 dominis.
* cendrassos.local i montsacopa.loca són dos arbres amb dos dominis 
* Tots 3 poden estar dins el mateix bosc.

> IMATGE