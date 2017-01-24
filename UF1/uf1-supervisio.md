# Supervisió de sistemes operatius propietaris

## Tasques de l’administrador de sistemes

Algunes de **tasques d'un administrador de sistemes **d'informació:

* Instal·lació, configuració i reconfiguració del Sistema Operatiu 
* Instal·lació, actualització dels drivers i firmwares.
* Instal·lació de les **actualitzacions **crítiques i/o recomenables del sistema operatiu. 
  * Crítiques és important instal·lar-les, sempre que no afecti al funcionament del sistema d'informació. 
  * Recomanables depen de si ens soluciona un problema o no. 
* Gestió i comprovació de les** còpies de seguretat**. 
* **Monitorització i vigilar:**
  * l’estat del sistema
  * l’estat de la xarxa
  * l’estat dels serveis
  * l’espai físic d’emmagatzematge
  * els possibles problemes generats pel programari
  * etc

## Eines de supervisió

El sistema operatiu Microsoft Windows Server 2012 us proporciona una sèrie d’**eines** i facilitats perquè pugueu **administrar el sistema** de manera efectiva i ràpida:

* **Administrador del servidor**
* **Administració de tasques**
* **Administració de serveis**
* **Registre d’esdeveniments**

### Administrador del servidor _\[Server Manager\]_

L'**Administrador del servidor** permet veure, en una única pantalla, la informació del sistema, opcions de configuració de seguretat i  les rols i caracterísiques intal·lats i els seus possibles problemes de configuració.

![](/assets/ServerManager.png)

L'**Administrador del servidor**,  amb una única eina, permet als administradors:

* Veure i modificar els** rols i característiques instal·lats** al servidor.
* Realitzar tasques d'administració com **iniciar o aturar serveis** i administrar comptes d'usuari locals.
* Determinar l'**estat del servidor**.
* Identificar **esdeveniments crítics**. 
* Analitzar i solucionar **problemes o errors de configuració**.

### Administrador de tasques _\[Task Manager\]_

L’**administrador de tasques** és l’eina principal per administrar processos i aplicacions del sistema.  
Disposa de cinc pestanyes. Aquestes pestanyes us ajudaran a administrar **processos, rendiment, usuaris i serveis**.

![](/assets/TaskManager.png)

Teniu **quatre vies per accedir** a l’administrador de tasques:

* Combinar les tecles _**Control, Majúscules i Esc**_.
* Combinar les tecles **Control, Alt i Supr** i escollir l’opció Iniciar l’administrador de tasques.
* Clicar a Inicio, escriure _**taskmgr**_ en el quadre de text, clicar a Iniciar la cerca i prémer Enter.
* Clicar amb el botó dret del ratolí a la barra d’eines i seleccionar l’opció _**Administrador de tasques**_.

### Administrador de serveis

Els **serveis** són programes que funcionen sense interactuar directament amb l'usuari.

Normalment són programes que s'arranquen amb el sistema operatiu.

Cada servei el podem configurar: Ens posem a sobre &gt; boto dret ratolí &gt; propietats:

![](/assets/services.png)

#### Configuració d'inici d'un servei

És important que feu la **configuració d’inici** dels serveis més escaient.  
Que un servei estigui instal·lat no vol dir que s'estigui executant.

![](/assets/SevicesStart.png)

Existeixen quatre **tipus d’arrencada d’un servei**:

* **Automàtic:** El servei que s’iniciarà quan l’equip s’engegui.
* **Automàtic \(inici retardat\):** el servei s’inicia quan l’equip està en marxa i tots els serveis automàtics \(marcats amb l’opció anterior\) estan funcionant. 
* **Manual:** el servei s’haurà d’iniciar manualment.
* **Deshabilitat:** el servei estarà desactivat.

> Tenir executant-se serveis que no fem servir consumirà recursos innecessaris.

#### Configuració de la recuperació d'un servei

El sistema Microsoft Windows Server permet fer accions si detecta que un servei específic falla. 

![](/assets/ServeisRecuperacio.png)

Existeixen tres opcions de **recuperació d’un servei**:

* **No fer cap acció:** el sistema no intentarà recuperar-se d’aquest error, però sí de la resta.
* **Reiniciar el servei:** atura el servei, fa una pausa i el torna a iniciar.
* **Executar un programa:** si es produeix un error en aquest servei, es llançarà un script o un programa.

### Registre d’esdeveniments _[Event Viewer]_

El **registre d’esdeveniments** posa a disposició de l’administrador informació historial, amb la qual pot localitzar problemes de seguretat i del sistema.

![](/assets/EventViewer.png)

## Actualitzacions

Tant important és la monitorització com **l’actualització **dels components del Sistema Operatiu.

**Tipus d'actualitzacions:** 

  * **Pedaç, “Parches” (Hot fixes)**: Un fitxer que modifica el codi de programes intentant solucionar problemes de seguretat trobats en el programa fins el moment, intenta no modificar el funcionament del programa. 
  * **Services pack (SP)**: Consteix en un conjunt de pedaços que actualitzen, corregeixen i milloren aplicacions i sistemes operatius.
  
Des de **Windows Update** existeixen **quatre configuracions** possibles: 

![](/assets/WindowsUpdate.png)

* **Instal·lar actualitzacions automàticament (recomenat)**.
  * Les actualitacions requereix reiniciar, per aquesta, raó si triem l'opció automàtica, **configurarem el dia i la hora** que no afecti al funcionanament de l'empresa o als processos del servidor o sistema informàtic. 
* **Descarregar actualitzacions, però deixar-me triar quan instal·lar-les**.
* **Buscar actualitzacions, però deixar triar si vull descarregar-es i intalar-les**.
  * Quan volem controlar quines actualitzacions s’instal·len.
* **No buscar actualitzacions (no recomenat)**
  * Podem instal·lar manualment les actualitzacions des de la web oficial de Windows.

