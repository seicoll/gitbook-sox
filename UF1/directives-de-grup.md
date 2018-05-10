# Directrius de grup [_Group Policy Object (GPO)_]

## Què és una directriu de grup (GPO)?

Una **directriu de grup (GPO)** és un component a on **es defineixen les regles** o polítiques que compatiran tot un grup de comptes d'usuari o equips en un domini.

> Una **directriu de grup** és un conjunt d'una o més polítiques que defineixen el què els usuaris poden o no poden fer en un sistema informàtic (drets i privilegis).

* **Per exemple**: bloquejar l’accés a l’administrador de tasques, restringir l’accés a determinades carpetes, deshabilitar la descàrrega d’arxius executables, etc.

Les directrius de grup **simplifiquen molt l’administració i configuració dels ordinadors** de la nostra empresa.

Les directrius de grup sovint s’**utilitzen per restringir certes accions** que poden presentar riscos de seguretat. 

Algunes configuracions que permeten les directrius de grup són: 
  * Polítiques de seguretat 
  * Instal·lació automàtica de programari
  * Execució de scripts

## Tipus de directrius de grup

* **Directrius de grup local**

  * Són aquelles que només s'apliquen **a la màquina on s'han definit**.

  * Normalment, es configuren directament en els clients, o bé, quan es treballa en una xarxa sense domini (grup de treball).

* **Directrius de grup d'Active Directory**

  * Són aquelles que s'apliquen **a un conjunt d'usuaris o equips del domini**.

## Principals polítiques incloses en un directriu de grup (GPO)

Cada directriu de grup (**GPO**) conté la configuració del **equip **i d'**usuari**. 

* **Configuració de l’equip**: permet establir les directrius que s’aplicaran als equips amb independència de qui inicia la sessió.

* **Configuració d’usuari**: permet establir les directrius que s’aplicaran als usuaris, independentment de l’equip en què hagin iniciat la sessió.

Cadascuna d’aquestes es divideix en arbres iguals.

![](/assets/directrius_edicio.png)

Hi ha polítiques que estan als dos subarbres però amb significats i/o paràmetres diferents.
Per exemple:

* **Configuración del Equipo** > Directivas > config Windows > script: Scripts que s'executen **quan es tanca o inicia equip**.
* **Configuración de usuario** > Directivas > config Windows > script: Scripts que s'executen **quan un usuari tanca o inicia sessió local**.

Dins cada configuració d’equip o d’usuari, hi trobem directives i preferències:

* **Directives**: 
  
  * **Configuració de software**: instal·lació automàtica de programari. 
  
  * **Configuració de Windows**: entre altres, aspectes de configuració de seguretat i execució de scripts.

  * **Plantilles administratives**: inclouen aquelles polítiques basades en la configuració de l'equip, com els següents: Tauler de control, escriptori, impressores, xarxa, carpetes compartides, etc. 

* **Preferències**: aspectes de configuració que típicament es feien amb scripts en versions anteriors de Windows. 

  * **Configuració de Windows**: Opcions de configuració com variables entorn, accessos directes, unitats xarxa 

  * **Configuració del panell de control**: Instal·lació dispositius, impressores, opcions d'energia, tasques programades, serveis, etc.


## Creació de directrius de Grup (GPO)

Per introduir-nos a les directives de grup el millor és començar amb un exemple.

**Exemple: Canviar el fons de pantalla**

1. Primerament, comprovem que tenim instal·lat la característica del servidor** Administració de directrius de grup** [_Group Policy Management_] per poder utilitzar la Consola d’administració de directrius de grup.

2. **Creem una carpeta** en el servidor. La anomenarem **_wallpaper_** i fiquem una imatge.

3. **Compartim la carpeta** a tots els usuaris del domini. Fem botó dret sobre la carpeta i escollim "compartir".

4. Obrim la Consola d’administració de directrius de grup a través de l’**_Administrador del Servidor > Eines > Administració de directrius de grup_**.

5. Fem botó dret sobre el nostre domini i **creem la nostra directriu de grup (GPO) **i l’anomanem "Directriu Fons Pantalla".
  * Es crea una plantilla amb totes les possibles polítiques sense configurar. Si volem s'apliquin s'han de configurar. 
  * Al fer botó dret sobre el nostre domini es vincula la directriu aquest contenidor (a tot el domini).
  * Els contenidors on es poden vincular GPOs són: sites, dominis, i OUs.
  * Els comptes i equips que estan dins del contenidor reben automàticament les polítiques que estiguin configurades en el GPO.

6. Fem botó dret sobre de la política que acabem de crear i escollim **_Editar..._**.

7. S’obrirà l’**Editor de directrius** de la GPO.

8. Anem a **_Configuració d'usuari > Directives > Plantilles administratives > Active Desktop > Active Desktop > Tapiz del escritorio_**.

![](/assets/directriu_escriptori.png)

9. **Habilitem la directriu**, posem el camí de la imatge `\\NomServidor\wallpaper\imatge.jpg` 

10. Tornem a la finestra de **_Administració de directives de grup_** i fem clic a la nostra directiva i anem a la pestanya "Detalles" aquí escollim en _**Estado de GPO**_ l'opció **_Configuració d'equip deshabilitada_** ja que ens interessa que estigui habilitat per usuari, no per equip.

11. Per **actualitzar les directrius**, anem a la línia de comandes i executem:  

  `gpupdate /force`

12. I per últim, podem **mostrar les directrius** aplicades executant:

  `gpresult /r`

13. Ara ja podem **comprovar **que funciona, aneu al vostre equip del domini Windows 7 i comprova que s'ha canviat el fons de pantalla.

## Aplicació de directrius

En funció d’on s’apliquin les directrius de grup, es poden crear dos grans conjunts de directrius:

* **Directrius que s’apliquen a equips**: normalment s’apliquen durant l’arrencada de l’equip.

* **Directrius que s’apliquen a usuaris**: s’apliquen quan els usuaris inicien les sessions.

Administrador les pot forçar l’actualització de les directrius amb la comanda:

`gpupdate /force`

> No funciona amb totes les polítiques. Sempre hi ha algunes que necessiten tancar sessió o reinicia equip. 

## Herència de directrius

Les directrius són **heretables **i **acumulatives**:
  * Els **GPO **vinculats a un site són heretats pel domini
  * Aquests, més el vinculats al domini són heretats per les OU de primer nivell.
  * Tots els anteriors més les GPO de les OU primer nivell són heretats per les OU de segon nivell, etc. 

![](/assets/directrius_herencia.png)

Pot ser que hi hagi comptes usuari o equip, amb **duplicitat de polítiques**. 

Per evitar conflictes, s’utilitza el següent **ordre d'aplicació**: 
1. Directrius de **grup local** del equip. 
2. GPOs viculades a **sites**.
3. GPOs vinculats a **dominis**.
4. GPOs vinculats a **Unitats Organitzatives de primer nivell**.
5. GPOs vinculats a **Unitats Organitzatives de segon nivell**. 

## Delegació del control del GPO

Qualsevol usuari o grup que tingui aplicat el **control total** sobre un GPO pot administrar-lo. 

Per defecte, poden **administrar GPOs**: 
* Grup administradors d'empresa 
* Grup adminstradors del domini 
* Creador del GPO 
* El propi SYSTEM 

Per defecte, només poden **crear GPOs**: 
* Administradors d'empresa i domini 
* Usuaris o grups membres del grup Group Policy Creator Owners 

> Es pot **delegar el control** a altres usuaris i grups posant els usuaris que han de fer aquesta tasca al grup **_Group Policy Creator Owners_**.

## Directrius d'instal·lació de programari

Permet instal·lar programes als ordinadors clients des del servidor.

Serveix tant per instal·lar com per desinstal·lar de forma centralitzada.

Hi ha dues formes desplegar una aplicació:

* **Assignar**: 
  * Permet que l’aplicació s’instal·li o bé quan l’usuari intenti accedir per primera vegada o bé automàticament. 
* **Publicar**: 
  * Dóna la oportunitat a l'usuari d'instal·lar l'aplicació si li interessa, però sense cap acció automàtica. 
  * La llista aplicacions publicades i instal·lar-les, apareix al **_Panel de control > Añadir / eliminar programas_**.

> La publicació sempre es fa sobre els usuaris, mentre que l’assignació es pot fer sobre el usuaris o sobre els equips.

## Consells d'utilització de polítiques de grup

* **Separar Equips i  Usuaris en OUs** diferenciades: 
  Facilita tasca d'administració d'usuaris/equips i podem assignar a administradors diferents. 

* **Minimitzar els GPOs **associades a usuaris o equips:
  Els temps que triga a iniciar equip o usuari depèn del número de polítiques a aplicar. 

