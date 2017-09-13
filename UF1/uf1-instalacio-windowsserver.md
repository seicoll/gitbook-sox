# Instal·lació Windows Server 2016

## Planificació de la instal·lació

### Comprovar els requeriments de maquinari

  Cal assegurar-nos que el nostre maquinari compleix els requisits mínims tan del sistema operatiu com de les aplicacions que s'han d'instal·lar.

### Preparar el programari a instal·lar i les dades a configurar
  
  Cal tenir preparat tot el programari i les dades necessàries: Sistema Operatiu, controladors, claus d'activació, etc.

> **Nota:** Si no disposes d'una **llicència** de Windows Server, pots obtenir, de forma gratuita, un versió d'evaluació durant un període de 180 dies a la següent direcció:
[https://www.microsoft.com/es-es/evalcenter/evaluate-windows-server-2016](https://www.microsoft.com/es-es/evalcenter/evaluate-windows-server-2016)

### Crear la màquina virtual

  Cal crear una màquina virtual amb les característiques recomanades per instal·lar **_Windows Server 2016 64 bits Standard Edition_**.
  * El nom de la màquina pot ser **_SOX Windows Server_**.
  * Es recomana que l'espai del disc es reservi de forma dinàmica.
  * Es recomana posar 2 CPU com a mínim.
  * Si és possible, habilitar l'acceleració gràfica 2D i 3D.
  * [Crea i i configura la** xarxa NAT SOX**](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf0/A012-VBoxPlus.html#config_nat_network) amb l'adreça **172.30.0.0/16** i suport per DHCP.

* **Planificar el disc**

  Cal planficar la utilització del disc, decidir les particions necessàries i el sistema de fitxers a utilitzar.

## Opcions d'instal·lació

Windows Server permet instal·lar-se en dues versions diferents:

* **Opció Instal·lació Servidor amb GUI _[Grafic User Interface]_**

  * S’instal·la la interfície gràfica d'usuari estàndard amb totes les eines d'administració del servidor.
  
  
* **Opció Instal·lació Server Core. **

  * No s’instal·la la interfície gràfica d’usuari estàndard i el servidor s’administra amb la línia de comandes (Windows PowerShell) o bé remotament.
  * És l’opció predeterminada i recomanada per Microsoft. 
  * **Avantatges**: requereix menys espai de disc (uns 4GB menys), és més eficient i augmenta la seguretat.

> A partir de la versió Windows Server 2012, **es pot passar d’una opció a l’altra** en qualsevol moment.

Podem instal·lar l’opció _**Servidor amb GUI**_ al principi, utilitzar les eines gràfiques per configurar el servidor, i després, canviar a l’opció instal·lació _**Server Core**_.

## Minimal Server Interface

La possibilitat de passar d’una instal·lació a una altra, crea una instal·lació intermitja anomenda **Mininal Server Interface**.

Aquesta interface és el resultat d’iniciar amb una instal·lació** Servidor amb GUI** i després canviar a una instal·lació **Server Core**. 

Amb **Minimal Server Interface**, continuen instal·lats els següents components:
  * La Consola d’Administració Microsoft _[Microsoft Management Console (MMC)]_
  * L’Administrador del Servidor 
  * Una part del Tauler de Control

Però no hi trobarem intal·lats ni l'Exporador d'arxius ni el Navegador web entre d'altres components.

![Minimal Server Interface](/assets/WindowsServerMinimal.png)

## Tipus d’instal·lació

Una vegada escollit l’opció d’instal·lació, cal que decidiu si fareu una instal·lació des de zero o bé optareu per actualitzar el vostre sistema.

* **Instal·lació des de zero (personalitzada): **El sistema operatiu que hi hagi a l’equip se substituirà completament, de manera que les configuracions i les aplicacions es perdran.
* **Actualització:** el sistema operatiu s’instal·la i es fa una migració de les configuracions, els documents i les aplicacions.

> Si durant el procés d’instal·lació en falta alguna informació que necessitem per continuar. En el moment que es demana On es vol instal·lar Windows? es pot accedir a la línia de comandes prement Majúscules i F10.

## Particionar el disc

> Com a norma general crearem una **partició pel sistema operatiu** i una altra per les **dades**.

D'aquesta forma els possibles errors del sistemes operatiu no afectaran tant directament a les dades.

* Amb el botó **_Nuevo_**,  crear una partició d'uns 20 GB.
* Utilitzar l'espai restant per crear una altra partició.
* Seleccionar la partició de 20 GB per instal·lar el sistema i continuar endavant.

![](/assets/WSInst07-Particionat.png)

## Post-instal·lació

Una vegada s’ha instal·lat el sistema operatiu caldrà proporcionar la informació següent a l’equip:

### Establir zona horària

Per canviar l'hora del sistema es pot fer fent clic amb el botó secundari sobre la bara de tasques on hi ha la data i hora. I després seleccionar l'opció **_Ajustar data i hora_**.

### Canviar el nom de l’equip

Durant la instal·lació es genera de forma automàtica un nom pel servidor poc descriptiu i difícil de recordar com _WIN-BOGEMFKQDSH_. És recomenable canviar-lo i posar a la màquina un nom que sigui fàcil de recordar.

Fer clic amb el botó secundari del ratolí sobre la icona d'inici de Windows i seleccionar l'opció **Sistema**. Després anar a _**Cambiar configuración > Cambiar... > Nombre de equipo**_.

### Contrasenya de l'usuari Administrador

> S'ha de posar una contrasenya que compleixi els requisits de complexitat de Windows (mínim 8 caràcters, minúscules, majúscules, números i símbols).

És recomanable que trieu bé aquesta contrasenya i la poseu a tot arreu, tant per Windows com per Linux (evidentment, en un cas real s'han de posar contrasenyes diferents).
  
### Configuració de la xarxa.

Un servidor ha de tenir una **adreça estàtica** ja que els clients l'han de conèixer per poder accedir-hi i utilitzar els seus serveis. 

L'adreça ha de pertànyer a la xarxa on està connectada la màquina:
* **Adreça IP**: `172.21.A.10` (**_A_** és el teu número d'alumne)
* **Màscara**: `255.255.0.0` (de 16 bits, com la de la xarxa)
* **Porta d'enllaç (GW)**: `172.21.0.1` (l'adreça del router de l'aula)
* **Servidors DNS**: `192.168.0.30` i `8.8.8.8`

### Iniciar sessió
Demana que es premin les tecles _**Ctrl+Alt+Supr**_, però en VirtualBox s'ha de fer amb **_Ctrl dreta + Supr_**.
Un cop es posi la contrasenya de l'administrador, s'accedirà al sistema.
  
### Actualització del sistema operatiu 

### Instal·lar _Guest Additions_

En el cas de **màquines virtuals**, pot ser molt útil instal·lar les eines addicionals del gestor de màquines virtuals (en el cas de VirtualBox, les **_Guest Additions_**). 

Aquestes eines permeten disposar de més opcions per configurar el monitor, realitzar accions de "copiar i enganxar" entre la màquina real i la virtual, o accedir des de la màquina virtual a una carpeta de la màquina real per poder passar arxius fàcilment.

Per instal·lar les **_Guest Additions_** cal tenir la màquina virtual engegada i, en el menú de la mateixa finestra de la màquina virtual, seleccionar l'opció **_Dispositivos → Insertar imagen del CD de las Guest Additions_**. Això és equivalent a posar el CD d'instal·lació en la màquina virtual. 
 
En la majoria de sistemes amb entorn gràfic, s'obrirà automàticament una finestra per instal·lar el contingut. Si no, cal obrir el CD i executar el programa **_VBoxWindowsAdditions_**.

### Clau d'activació de Windows i període de proves

Si no s'ha introduït la clau d'activació durant la instal·lació, es disposa de 180 dies per provar-lo.

A la finestra d'inici ens avisa dels dies què queden.
Un cop acabat aquest període, es pot allargar 180 dies més obrint un terminal i posant la següent comanda:

`slmgr.vbs /rearm`

Després cal reiniciar la màquina.

Per **Introduir o canviar la clau d'activació** cal anar a _**Sistema**_ i a la part inferior hi ha un enllaç amb l'opció **_Introducir o cambiar la clave de producto_**.

### Fer una còpia de seguretat

En una màquina real, només faltaria realitzar una còpia de seguretat completa i configurar les copies de seguretat periòdiques.

En el cas de les màquines virtuals, es pot fer un snapshot o copiar el disc virtual.

Els snapshots es fan i es poden recuperar més ràpidament, però poden fer què la màquina funcioni una mica més lenta, sobre tot si el disc no és SSD. També fan què el disc virtual ocupi més espai.

> **ATENCIÓ**: un cop feta la instal·lació, configuració i comprovacions, feu una còpia del disc virtual de la màquina i guardeu-la bé. Us pot estalviar molta feina si en algun moment se us fa malbé la màquina.

### Instal·lació noves funcionalitats i característiques

Instal·lar noves funcionalitats o noves característiques: 
* **Funcions de servidor o rols:** Conjunt de programes que fan una funció específica per diferents usuaris o altres equips d'una xarxa. Un servidor pot realitzar més d'una funció o rol.
  * Servidor de fitxers. 
  * Servidor d'aplicacions. 
  * Servidor de correu. 
  * Terminal server: permet l’administració remota del servidor des d’un altre equip de la xarxa. 
 * Control de domini. 
  * Servidor DNS: realitza la resolució de noms del domini. 
  * Servidor DHCP: realitza l’assignació direccions IP automàtiques.
  * etc.
* **Serveis de funcions** (serveis de rol): afegeixen més funcionalitat a un servidor. 
  * Alguns rols, com per exemple el de servidor de DNS, només tenen una funcionalitat, i per tant no tenen serveis de rol disponibles. 
  * Altres, com per exemple el de servidor d'escriptori remot, tenen diferents serveis de rol que es poden afegir en funció de les necessitats de l'empresa.
* **Característiques:** són programes per complementar o augmentar la funcionalitat del servidor però no tenen cap relació amb els rols que desenvolupa. 
  * Client TFTP
  * Client Telnet

> Un servidor es pot especialitzar en una única funció o en diverses.

**Font d'informació:**  [Apunts SOX de Pere Sánchez](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf1/nf1/1202-WSInstalar.html)
# Documentació i recursos

  * **SomeBooks.es**: Instalación de Winsdows Server 2012 R2
[http://somebooks.es/capitulo-2-instalacion-de-windows-server-2012-r2/4/] (http://somebooks.es/capitulo-2-instalacion-de-windows-server-2012-r2/4/)

---

**Font d'informació:**  [Apunts SOX de Pere Sánchez](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf1/nf1/1202-WSInstalar.html)


