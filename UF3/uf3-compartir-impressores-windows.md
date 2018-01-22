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

![](/assets/win-print-management.png)

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

Per compartir una impressora cal anar, per configurar els permisos de compartició cal anar a **_Administrar ús compartit_** o bé a les **_propietats de la impressora_** i entrar a la pestanya **_Compartir_**.

> Imatge



## Gestió de permisos de compartició

La pestanya **_Seguretat_** s'accedeix a les opcions per compartir la impressora de forma avançada.

![](/assets/uf3-compartir-impressora.png)

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



## Configuració de la impressora compartida en el client

## Implementar impressora compartida amb directiva de grup



## Instal·lar impressora de xarxa

Opció 1: Si no sabem la IP de la impressora
Afegir impressora... > Busca impressores de xarxa
Seleccionar impressora de la llista


Opció 2: Si sabem la IP de la impressora
Afegir impressora TCP/IP escrivint la direcció IP o nom de host.
Posar la IP de la impressora


Instal·lar controlador


## Documentació i recursos

* **Somebooks**: Compartir una impresora del controlador de dominio con Windows Server 2016 (http://somebooks.es/compartir-una-impresora-del-controlador-dominio-windows-server-2016/)