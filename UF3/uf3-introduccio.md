<!-- notoc -->

# Introducció

La compartició de recursos en xarxa és una de les utilitats o raons principals perquè els sistemes operatius es connectin en xarxa.

En un entorn on es comparteixen recursos, és molt important controlar qui pot accedir a la xarxa i l'ús que pot fer de les màquines i dels recursos compartits per evitar situacions com les següents:
* **Accés a ordinadors i recursos de la xarxa**: que una persona no autoritzada pugui utilitzar les màquines i recursos de l'empresa.
* **Modificació del funcionament del sistema i dels recursos**: que qualsevol pugui modificar la configuració del sistema o canviar els permisos d'accés a carpetes i impressores.
* **Accés a recursos restringits**: que un usuari pugui veure documents amb informació a la qual no ha de tenir accés o que pugui imprimir sense necessitat en una impressora en color.
* **Utilització de recursos**: que un usuari pugui omplir un disc o acaparar l'ús d'una impressora impedint l'ús a altres usuaris o, fins i tot, impedint el correcte funcionament del sistema.

Es poden compartir tot tipus de recursos, encara que els més habituals són **directoris** i **impressores**. 

En els **sistemes operatius lliures** hi ha diversos protocols i aplicacions que ens permeten compartir recursos en xarxa, com el **protocol NFS** i el paquet de programari **Samba**.

En aquesta mòdul no es parlarà dels sistemes de protecció activa i passiva que es veuen en altres mòduls (antivirus, còpies de seguretat...) sinó d'altres aspectes gestionats directament pel sistema operatiu: els drets, privilegis i permisos.

## Drets d'inici de sessió o drets d'accés

Aquests **drets** determinen qui pot accedir al nostre sistema i de quina forma:
* **Formes d'accés**
  * Accés local o remot a una màquina
  * Accés al domini
* **Limitacions d'accés**
  * En quines màquines es pot accedir
  * Durant quins períodes de temps es pot accedir

## Privilegis

Els **privilegis** determinen quins usuaris poden realitzar determinades accions que afecten a la màquina, al sistema operatiu o al domini.
Els següents són aluns exemples:
* Aturar el sistema o apagar la màquina
* Canviar la data i hora
* Instal·lar programes i controladors de dispositius
* Crear, modificar i eliminar usuaris i grups
* Configurar i compartir els recursos
* Afegir equips al domini o treure'ls
* Fer auditories i configurar la seguretat

## Permisos

Els **permisos** determinen què poden fer els diferents usuaris amb els recursos, siguin locals o compartits.

Els principals recursos que es comparteixen en una xarxa son els arxius, les carpetes i les impressores.

De forma molt general i simplificada, tenim els següents permisos:
* **Permisos per arxius i carpetes**
  * Lectura
  * Modificació (o escriptura)
  * Execució (en els arxius) o navegació (en les carpetes)
* **Permisos per impressores**
  * Imprimir
  * Gestionar la llista de documents pendents d'imprimir (canviar prioritats, eliminar...)
  * Administrar les impressores (afegir, eliminar, configurar, posar en pausa...)

**Assignació de permisos**

Els permisos es poden assignar a usuaris individuals o a grups.
Quan els permisos s'assignen a un grup, aquests permisos s'aplicaran també als subgrups i usuaris que pertanyin a aquest grup.
> Si els permisos del grup entren en contradicció amb altres permisos assignats als subgrups o usuaris, s'aplicaran els més específics (els de subgrup o els d'usuari).

## Compartició de recursos

Quan es disposa d'ordinadors connectats en xarxa, és molt convenient compartir recursos.

Alguns dels **principals avantatges** són els següents:

* **Reduir costos**: normalment no fa falta tenir una impressora per cada usuari, ni discos de gran capacitat en tots els ordinadors; es pot compartir una impressora entre vàries màquines o guardar els arxius en un sistema d'emmagatzematge centralitzat.

* **Facilitar la feina dels usuaris**: es pot fer que un usuari pugui treballar en qualsevol ordinador sense haver de reconfigurar cada vegada el seu entorn de treball, i poder accedir fàcilment als seus documents, a documents que comparteixen altres usuaris o a una impressora encara que aquests recursos no estigui en el seu ordinador.

Els **principals recursos** que es poden compartir en xarxa són:
* **Arxius i carpetes**
* **Impressores**

