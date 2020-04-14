# Perfils d'usuaris

## Què és el perfil d'un usuari?

> El **perfil d'un usuari** és un conjunt de dades que serveixen per personalitzar l'entorn de treball d'aquest usuari.

Aquestes dades inclouen:

* En quina **carpeta on es guarda el perfil d'usuari** on es guarda la configuració que l'usuari fa del seu entorn de treball
  * Fons de l'escriptori, mida de les icones, la lletra del sistema, configuració del teclat i ratoli...
  * **Accés ràpid**: arxius que l'usuari guarda a l'escriptori, arxius descarregats d'Internet, música, fotos i vídeos.

    ![](../../.gitbook/assets/adperfil_accesrapid.png)
* En quina **carpeta privada** on es guarden els seus arxius personals. Només ell hi podrà accedir.
* Quin **script s'executarà cada cop que l'usuari iniciï sessió**. Algunes de les coses que es poden programar son:
  * Sincronitzar la data i hora del client amb el servidor.
  * Configurar les impressores a les que pot accedir l'usuari.
  * Connectar una unitat de xarxa a una carpeta compartida en el servidor. 

Els diferents arxius que formen el perfil s'estructuren en carpetes com per exemples _**Dades de programes**_, _**Escriptori**_, _**Favorits**_, _**Els meus documents**_, _**Impressores**_, etc.

> Si es fa què la carpeta del seu perfil d'usuari es guardi en un servidor, l'usuari tindrà la seva configuració en qualsevol màquina del domini, i en aquest cas es diu que té un **perfil mòbil \(**_**roaming profile**_**\)**.

Si no es configura un perfil mòbil, en cada màquina on es validi l'usuari se li crearà un **perfil local**.

## Tipus de perfils

**Perfil local**:

* Quan s'accedeix amb un usuari local, el perfil d'usuari que s'utilitzarà és el què hi a la mateixa màquina. 
* Si encara no té cap perfil guardat, se li crea un per defecte. 
* Quan l'usuari tanca sessió, es guarden els canvis què ha fet \(el seu perfil\) en la mateixa màquina.

**Perfil temporal**:

* Es crea un perfil temporal quan no es pot carregar el perfil. 
* Els canvis que faci l'usuari s'esborren quan es tanca la sessió.

**Perfils de xarxa**:

* Quan s'accedeix amb un usuari del domini, es carrega el perfil guardat en el servidor. D'aquesta forma, l'usuari tindrà la seva configuració en qualsevol ordinador. 
* Els canvis que faci \(si és un perfil mòbil\) també es guardaran al servidor quan tanqui la sessió.
  * **Perfil Mòbil**: l'usuari pot fer canvis en el seu perfil.
  * **Perfil Obligatori**: l'usuari pot fer canvis però s'esborren al tancar la sessió.
  * **Perfil Súper-obligatori**: si no es pot carregar el perfil, no es pot iniciar sessió.

> Els **perfils mòbils** són molt útils però també tenen **inconvenients**:
>
> * Si l'usuari té molts arxius o arxius molt grans, l'inici i tancament de sessió es ralentitza molt. 
> * Pot augmentar molt el tràfic de xarxa. 
> * Si falla la xarxa o el servidor, els usuaris no podran accedir als seus arxius.

## Configuració de perfils d'usuaris

### Creació de la carpeta per guardar els perfils

Si es vol configurar els **perfils mòbils**, primer de tot cal crear en el **servidor** la carpeta on es guardaran les carpetes de perfil de cada usuari i posar els permisos adequats:

> En el **nom carpeta** dels perfils, és convenient no posar espais, accents, ñ, ç o altres símbols prohibits \(\*, ?\) o que puguin dificultar l'accés a aquestes carpetes des d'altres sistemes operatius. El millor és utilitzar exclusivament lletres, números i/o guió baix \(\_\).
>
> A més, **si es canvia el nom de la carpeta**, caldrà tornar-la a compartir, i si canvia el nom de recurs compartit s'hauran de tornar a configurar els perfils!

Un cop creada la carpeta cal posar els **permisos** adequats:

1. Clicar amb el botó dret sobre la carpeta determinada i seleccionar _**Propiedades**_
2. Entrar a la pestanya _**Seguridad**_ i clicar el botó _**Opciones avanzadas**_
3. Si cal, canviar el propietari pel grup _**Administradores**_
4. Clicar el botó Deshabilitar herencia i seleccionar _**Quitar todos los permisos heredados...**_
5. Afegir els següents usuaris i donar-los els permisos necessaris clicant el botó _**Agregar &gt; Seleccionar una entidad de seguridad**_:
   * **Administadors \(Administrators\)** 
     * Aplicar permisos sobre _**"Esta carpeta, subcarpetas y archivos"**_.
     * Marcar la casella **control total**.

       ![](../../.gitbook/assets/adpermisosadmin.png)

* **Propietari \(CREATOR OWNER\)**: 
  * Aplicar permisos sobre _**"Solo subcarpetas y archivos"**_ .
  * Marcar la casella **control total**.

    ![](../../.gitbook/assets/adpermisoscreator.png)
* **Usuaris del domini \(Domain Users\)**:

  * Aplicar permisos a _**"Solo esta carpeta"**_.
  * Clicar _**Mostrar permisos avanzados**_:
    * Permís per _**Travessar aquest directori/executar arxius**_.
    * Permís per _**Mostrar carpeta / llegir dades**_.
    * Permís per _**Crear carpetes / adjuntar dades**_.
    * _**Permisos de lectura**_.

  ![](../../.gitbook/assets/adpermisosusuaris.png)

### Creació de la carpeta per posar les carpetes privades

Si es vol què els usuaris tinguin una **carpeta privada** en el servidor per poder-hi accedir des de qualsevol màquina unida al domini, cal crear una carpeta on es posaran les seves carpetes privades de cada usuari.

Aquesta carpeta ha de tenir els mateixos permisos que la de _**perfils**_.

### Compartició de les carpetes

Per poder accedir des de les màquines clients a les carpetes dels perfils en el servidor, **cal compartir** la carpeta dels perfils i la carpeta privada i configurar els permisos de compartició adequats.

Les carpetes anteriors \(_**perfils**_ i _**privades**_\) s'han de compartir de forma que tothom tingui **control total** \(els permisos necessaris per cada usuari concret ja s'han d'haver configurat en els permisos de seguretat\).

* Clicar amb el botó dret sobre la carpeta determinada i seleccionar _**Propiedades**_
* Entrar a la pestanya _**Compartir**_ i clicar el botó _**Uso compartido avanzado**_
* Marcar la casella _**Compartir esta carpeta**_ i clicar el botó _**Permisos**_
* Seleccionar l'usuari _**Todos \(Everyone\)**_ i marcar l'opció _**Control Total**_

![](../../.gitbook/assets/adperfilspermisoscomparticio.png)

La ruta per accedir de forma remota a una carpeta compartida es pot veure a l'apartat _**Propiedades &gt; Compartir &gt; Ruta de acceso a la red**_.

![](../../.gitbook/assets/adperfilsrutacompartida.png)

El nom de la ruta només hauria de contenir el nom del servidor \(`\\WSXXX`\) i el nom de la carpeta compartida \(`\Perfils`\). Si surt una ruta més llarga, segurament és perquè s'ha utilitzat el botó _**Compartir...**_ en lloc de _**Uso compartido avanzado...**_.

### Configuració del perfil d'usuari

Per configurar el perfil mòbil d'un usuari cal seleccionar l'usuari i amb el botó secundari, es tria l'opció _**Propiedades**_  i anar a la secció _**Perfil**_.

* _**Ruta de acceso al perfil**_: ha de ser la carpeta que s'ha compartit per guardar els perfils més l'identificador de l'usuari o `%username%`.

  * Per exemple: 

    `\\WSXXX\Perfils\%username%` o bé 

    `\\IP_SERVIDOR\Perfils\%username%`

  > La ruta de la carpeta **Perfils** es pot trobar dins de les seves propietats, a la pestanya _**Compartir &gt; Ruta de acceso a la red**_.
  >
  > **MAI** s'ha de posar la ruta local \(`C:\...`\).

  ![](../../.gitbook/assets/adperfilsperfilruta.png)

  > La **carpeta de perfil mòbil** de l'usuari no es crearà fins que l'usuari es validi per primera vegada.

* _**Carpeta particular**_: ha de ser la carpeta que s'ha compartit per guardar les carpetes privades més l'identificador del l'usuari o `%username%`.

  * Per exemple: `\\WSXXX\Privades\%username%`

    També s'ha indicar la lletra de la unitat se xarxa a la què es connectarà aquesta carpeta en la màquina client.

    ![](../../.gitbook/assets/adperfilprivada.png)

  > La **carpeta privada** de cada usuari es crearà dins de `Privades`en quant es faci clic a _**Aceptar**_.

* _**Script de inicio de sessión**_: no s'ha de posar la ruta. Les màquines unides al domini ja saben on trobar-lo: `\\WSXXX\netlogon`.

### Comprovació de la carpeta de perfil mòbil

En el **client**, iniciar sessió amb un usuari del domini a qui se li ha configurat el perfil mòbil.

Podria ser que surtís un error indicant que s'ha creat un perfil temporal.

![](../../.gitbook/assets/adperfiltemporal.png)

Els possibles motius són:

* No s'ha pogut contactar amb el servidor: s'ha de provar a fer **ping** al servidor. Si no funciona:
  * Comprovar si el servidor i el client estan connectats en la mateixa xarxa.
  * Comprovar que les seves adreces IP i les màscares siguin correctes.
  * Comprovar la configuració del tallafocs.
* No s'ha trobat la carpeta del perfil de l'usuari en el servidor o els permisos no són els adequats:
  * Comprovar en el servidor els permisos locals: **creació de la carpeta de perfils mòbils**.
  * Comprovar en el servidor que la carpeta estigui compartida i tingui els permisos adequats: **compartició de la carpeta de perfils mòbils**.
  * Comprovar en el servidor que la ruta configurada en el perfil inclogui el nom d'usuari \(`\\WSXXX\Perfils\usuari`\) i coincideixi amb la ruta de la carpeta compartida: **configuració del perfil mòbil**.

Quan es tanca la sessió, si s'han fet canvis en el perfil es guarden al servidor.

Al tornar a entrar des de **qualsevol màquina del domini**, els canvis s'han de mantenir.

#### Comprovació del tipus de perfil creat en la màquina client

Des del **client** es poden veure els perfils i modificar algun paràmetre a _**Sistema &gt; Configuración avanzada**_.

Per poder-ho fer, cal validar-se amb l'**administrador del domini** o amb l'**administrador local**.

#### Comprovació de la carpeta del perfil en el servidor

Si no surtit cap error al iniciar sessió en l'equip client, en la carpeta de perfils del servidor apareixerà una carpeta per l'usuari.

Aquesta carpeta pot tenir la extensió _**.V6**_ depenent de la versió de sistema operatiu que tingui la màquina client \(Windows XP, Windows 8.1, Windows 10, etc\).

> Si les màquines clients no tenen la mateixa versió de sistema operatiu, per exemple Windows 10 en unes i Windows 7 en altres, els canvis que es facin en unes, no quedaran reflectits en les altres.

### Comprovació de la carpeta privada des del client

Un cop iniciada la sessió en el **client**, l'usuari ha de veure una unitat de xarxa \(la que s'hagi configurat en el perfil\) i ha de poder entrar, crear, esborrar i modificar arxius i carpetes.

![](../../.gitbook/assets/adcarpetaprivada.png)

Alguns errors que es poden produir són:

* **No apareix la unitat de xarxa** degut a que no s'ha trobat la ruta a la carpeta privada: cal assegurar-se que la carpeta `Privades` està compartida en el servidor i que la ruta configurada en el perfil \(`\\WSXXX\Privades\usuari`\) és correcta.
* **L'usuari no pot entrar o no pot modificar el contingut** degut a la configuració incorrecta dels permisos de la carpeta `Privada`: cal esborrar les carpetes privades dels usuaris, revisar els permisos de la carpeta `Privades`, tant els de seguretat com els de compartició, i tornar a configurar el perfil dels usuaris per a què es tornin a crear les carpetes de cada usuari amb els permisos adequats.

## Documentació i recursos

* **Font d'informació:**  Apunts SOX Pere Sánchez \([http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?tema=17](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?tema=17)\)
* **Somebooks:** Crear un perfil móvil \([http://somebooks.es/5-7-crear-un-perfil-movil/](http://somebooks.es/5-7-crear-un-perfil-movil/)\)

