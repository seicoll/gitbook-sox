# Perfils d'usuari

## Què és el perfil d'un usuari?

> El **perfil d'un usuari** és un conjunt de dades que serveixen per personalitzar l'entorn de treball d'aquest usuari.

Aquestes dades inclouen:

* En **quina carpeta es guarda la configuració** que l'usuari fa del seu entorn de treball (fons de l'escriptori, mida de les icones, la lletra del sistema, configuració del teclat i ratoli...).
* En **quina carpeta es guardaran els seus arxius** personals. Només ell hi podrà accedir.
* **Quin script s'executarà cada cop que l'usuari iniciï sessió**. Pot servir entre altres coses per què l'usuari pugui accedir a impressores i carpetes compartides

Si es fa què la carpeta del seu perfil es guardi en un servidor, l'usuari tindrà la seva configuració en qualsevol màquina del domini, i en aquest cas es diu que té un **perfil mòbil**.

Si no es configura la carpeta de perfil, en cada màquina se li crearà un **perfil local**.

## Tipus de perfils

**Perfil local**: quan s'accedeix amb un usuari local, el perfil d'usuari què s'utilitzarà és el què hi a la mateixa màquina. Si encara no té cap perfil guardat, se li crea un per defecte. Quan l'usuari tanca sessió, es guarden els canvis què ha fet (el seu perfil) en la mateixa màquina

**Perfil temporal**: es crea un perfil temporal quan no es pot carregar el perfil. Els canvis que faci l'usuari s'esborren quan es tanca la sessió

**Perfils de xarxa**: quan s'accedeix amb un usuari del domini, es carrega el perfil guardat en el servidor. D'aquesta forma, l'usuari tindrà la seva configuració en qualsevol ordinador. Els canvis què faci (si és un perfil mòbil) també es guardaran al servidor quan tanqui la sessió
* **Perfil Mòbil**: l'usuari pot fer canvis en el seu perfil.
* **Perfil Obligatori**: l'usuari pot fer canvis però s'esborren al tancar la sessió.
* **Perfil Súper-obligatori**: si no es pot carregar el perfil, no es pot iniciar sessió.

> Els perfils mòbils són molt útils però també tenen inconvenients: augmenten molt el tràfic de xarxa i, si falla la xarxa o el servidor, els usuaris no podran accedir als seus arxius.

## Configuració de perfils d'usuaris

### Creació de la carpeta per guardar els perfils

Si es vol configurar els **perfils mòbils**, primer de tot cal crear en el **servidor** la carpeta on es guardaran les carpetes de perfil de cada usuari i posar els permisos adequats:

> En el **nom carpeta** dels perfils, és convenient no posar espais, accents, ñ, ç o altres símbols prohibits (*, ?) o que puguin dificultar l'accés a aquestes carpetes des d'altres sistemes operatius. 
El millor és utilitzar exclusivament lletres, números i/o guió baix (_).

> A més, **si es canvia el nom de la carpeta**, caldrà tornar-la a compartir, i si canvia el nom de recurs compartit s'hauran de tornar a configurar els perfils!

Un cop creada la carpeta cal posar els **permisos** adequats:

1. Clicar amb el botó dret sobre la carpeta determinada i seleccionar **_Propiedades_**

2. Entrar a la pestanya **_Seguridad _**i clicar el botó **_Opciones avanzadas_**

3. Si cal, canviar el propietari pel grup **_Administradores_**

4. Clicar el botó Deshabilitar herencia i seleccionar **_Quitar todos los permisos heredados..._**

5. A cada un dels següents usuaris, se li han de donar els permisos necessaris clicant el botó     
**_Agregar > Seleccionar una entidad de seguridad_**:
  * **Administador**: aplicar permisos sobre aquest directori, els subdirectoris i els fitxers i marcar la casella **control total**.
  * **Propietari (CREATOR OWNER)**: aplicar permisos sobre els subdirectoris i els fitxers i marcar la casella **control total**.
  * **Usuaris del domini**: aplicar els següents permisos però només sobre aquest directori (clicar **_Mostrar permisos avanzados_**):
    * Permís per travessar aquest directori / executar arxius
    * Permís per mostrar carpeta / llegir dades
    * Permís per crear carpetes / adjuntar dades
    
  ![](/assets/perfilmobils_permisos.png)
  
### Creació de la carpeta per posar les carpetes privades

Si es vol què els usuaris tinguin una **carpeta privada** en el servidor, cal crear una carpeta on es posaran les seves carpetes privades.

Aquesta carpeta ha de tenir els mateixos permisos que la de **_perfils_**.
  
### Compartició de les carpetes

Les carpetes anteriors (**_perfils_** i **_privades_**) **s'han de compartir** de forma que tothom tingui control total (els permisos necessaris per cada usuari concret s'han d'haver configurat en els permisos de seguretat):

* Clicar amb el botó dret sobre la carpeta determinada i seleccionar **_Propiedades_**
* Entrar a la pestanya **_Compartir _**i clicar el botó **_Uso compartido avanzado_**
* Marcar la casella **_Compartir _**esta carpeta i clicar el botó **_Permisos_**
* Seleccionar l'usuari **_Todos_** i marcar l'opció **_Control Total_**

La ruta per accedir de forma remota a una carpeta compartida es pot veure a l'apartat **_Propiedades > Compartir_**.

### Configuració del perfil d'usuari

Seleccionar l'usuari i amb el botó secundari, es tria l'opció **_Propiedades _**i s'entra a la pestanya **_Perfil_**.

* **_Ruta de acceso al perfil_**: ha de ser la carpeta que s'ha compartit per guardar els perfils més l'identificador de l'usuari o `%username%`.
  * Per exemple: `\\WSXXX\Perfils\%username%` o bé `\\IP_SERVIDOR\Perfils\%username%`

* **_Carpeta particular_**: ha de ser la carpeta que s'ha compartit per guardar les carpetes particulars més l'identificador del l'usuari o `%username%`. També s'ha indicar la lletra de la unitat se xarxa a la què es connectarà aquesta carpeta en la màquina client.
* **_Script de inicio de sessión_**: no s'ha de posar la ruta. Les màquines unides al domini ja saben on trobar-lo: `\\WSXXX\netlogon`.

> La **carpeta de perfil** per cada usuari no es crearà fins què l'usuari es validi per primera vegada.
> La **carpeta privada** de cada usuari es crearà en quant es faci clic a **_Aceptar_**.

### Comprovació de la carpeta de perfil mòbil

En el **client**, iniciar sessió amb un usuari del domini a qui se li ha configurat el perfil mòbil.
Si surt un error indicant que s'ha creat un perfil temporal, dos possibles errors són:
* No s'ha trobat la ruta cap a la carpeta del perfil de l'usuari en el servidor
* Els permisos de la carpeta de perfil de l'usuari no són correctes.

Si no surt cap error, en la carpeta de perfils del servidor apareixerà una carpeta per l'usuari. Aquesta carpeta pot tenir la extensió **_.V2_** depenent de la versió de sistema operatiu que tingui la màquina client (Windows XP, Windows 8.1...).

Si s'han fet canvis en el perfil, es guarden al tancar la sessió. Al tornar a entrar des de qualsevol màquina del domini, els canvis s'han de mantenir.

### Comprovació de la carpeta privada

Un cop iniciada la sessió en el **client**, l'usuari ha de veure una unitat de xarxa (la que s'hagi configurat en el perfil) i ha de poder entrar, crear, esborrar i modificar arxius i carpetes.

Si no apareix la unitat de xarxa, segurament és per què no s'ha trobat la ruta. Cal revisar la ruta de la carpeta privada que s'ha configurat en el perfil.

Si no es poden crear arxius, carpetes... s'han de revisar els permisos de la carpeta privada, tant els de seguretat com els de compartició.

## Documentació i recursos

* **Font d'informació: ** Apunts SOX Pere Sánchez ([http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?tema=17](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?tema=17))