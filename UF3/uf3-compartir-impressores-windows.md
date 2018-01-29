# Compartir impressores en Windows

## Instal·lar el rol Servei d'impressió 

> El protocol que utilitza Windows (**SMB/CIFS**) ja ve implementat en el sistema, encara que no sigui un Windows Server, i per tant no cal instal·lar res per poder-lo utilitzar. 

Si es disposa d'un servidor, i sobre tot si es disposa d'un domini, el més recomanable és instal·lar el **Servei d'impressió (_Print Server_)**, que amplia les possibilitats d'administració de les impressores compartides.

Aquest servei s’encarregarà de compartir les impressores dins una xarxa i **gestionar la cua d’impressió** on es guaden de forma ordena els documents que rep per imprimir. Fins i tot, permet **instal·lar impressores automàticament** en els clients a través de directives.

Per instal·lar el **Servidor d'impressió** en el servidor, cal afegir el rol de **Serveis d’Impressió** seguint els següents passos:

1. Anem a l’**_Administrador del Servidor_**.
2. Afegir rols i característiques i afegim el rol **_Serveis d'impressió i documents (Print and Document Services)_**.
3. Seleccionem únicament el servei de rol **_Servidor de impressió (Print Server)_**.
4. I fem instal·lar.

## Compartir la impressora

Un cop instal·lat l’**_Administrador del Servidor_**, podem obrir l'administrador d'impressió anant a **_Eines > Administrador d'impressió_**.

![](/assets/uf3-win-print-management.png)

En el panell esquerra, dins la categoria de **_Serveis d'impressió_** trobem:

* Controladors [_Drivers_]
* Formularis [_Forms_]
* Ports [_Ports_]
* Impressores [_Printers_]

### Controladors

> Si la impressora està correctament instal·lada i configurada de forma local en el servidor, ja disposarem dels controladors necessaris per imprimir localment.

Tot i així, és interessant **guardar controlador pels diferents sistemes operatius** que utilitzen els equips clients del nostre domini. Així quan s'instal·li la impressora en el client ja tindrà disponible els controladors necessaris i no ens sol·licitarà el disc de la impressora. 

Podem afegir un nou controlador fent **_Botó dret de ratolí > Afegir controlador..._**

### Impressores

Per compartir una impressora cal anar l'**_Administració d'impressió_**, seleccionar una impressora i  anar a **_Administrar ús compartit_** o bé a les **_propietats de la impressora_** i entrar a la pestanya **_Compartir_**.

![](/assets/uf3-compartir-impressora-general.png)

* Marquem l'opció **_Compartir aquesta impressora_**
* **Nom del recurs compartit**: nom amb què es veurà la impressora a la xarxa.
* Marquem l'opció **_Presentar treballs d'impressió en els equips clients_**.
* Marquem l'opció **_Mostrar llista en el directori_**.

Si compartim aquesta impressora amb usuaris que tinguin altres versions de Windows, cal fer ús del botó **_Controladors addicionals..._** que ens permet instal·lar controladors per altres versions de Windows i així no l'hauran de buscar al instal·lar la impressora.


## Gestió de permisos de compartició

La pestanya **_Seguretat_** s'accedeix a les opcions per configurar els permisos de compartició de la impressora.

![](/assets/uf3-compartir-impressora.png)

> Cal treure el grup **_Tots [Everyone]_** per tal que només puguin utilitzar la impressora els usuaris que indiquem a continuació.

### Gestionar els usuaris

  Es poden afegir o eliminar usuaris i grups fent clic al botó **_Agregar..._**.

### Gestionar els permisos simples

  Seleccionant l'usuari o grup es poden marcar o desmarcar les caselles **_Permitir_** o **_Denegar_** en cada permís.

  Per defecte, si no està marcada la casella **_Permitir_**, implica que no es té el permís corresponent.

  Els **permisos** que es poden assignar són: 
 * _Imprimir_
 * _Administrar aquesta impressora_
 * _Administrar documents_ 
 * _Permisos especials_

### Opcions avançades

Amb el botó **_Opciones avanzadas_** es poden canviar algunes propietats avançades com:

* Canviar el propietari.
* Assignar **_Permisos especials_** com: 
    * _Permisos de lectura_ 
    * _Canviar permisos_  
    * _Prendre possessió_
* Veure els permisos efectius.

## Instal·lar la impressora compartida en el client


## Implementar impressora compartida amb directiva de grup


## Instal·lar impressora de xarxa

Obrir l'**_Administrador d'impressió_** anant a **_Eines > Administrador d'impressió_**, fer botó dret del ratolí i escollir **_Afegir impressora..._** >


![](/assets/uf3-afegir-impressora-buscar.png)


Podem instal·lar una impressora de xarxa varies formes en funció de si coneixem la IP o nom de la impressora o sinó tenim cap informació.

* Opció **_Buscar impressores a la xarxa:_** Si no sabem la IP o nom de la impressora.

  A continuació ens ha de detectar la impressora compartida i la seleccionem de la llista.


* Opció  **_Afegir impressora TCP/IP escrivint la direcció IP o nom de host_**

  A continuació caldrà posar la IP o nom de la impressora

  ![](/assets/uf3-afegir-impressora-IP.png)

### Instal·lar controlador


## Documentació i recursos

* **Somebooks**: Compartir una impresora del controlador de dominio con Windows Server 2016 (http://somebooks.es/compartir-una-impresora-del-controlador-dominio-windows-server-2016/)