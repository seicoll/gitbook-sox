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

* Controladors
* Formularis
* Ports
* Impressores

### Controladors

> Si la impressora està correctament instal·lada i configurada de forma local en el servidor, ja disposarem dels controladors necessaris per imprimir localment.

Tot i així, és interessant **guardar controlador pels diferents sistemes operatius** que utilitzen els equips clients del nostre domini. Així quan s'instal·li la impressora en el client ja tindrà disponible els controladors necessaris i no ens sol·licitarà el disc de la impressora. 

## Gestió de permisos de compartició

## Configuració de la impressora compartida en el client

## Documentació i recursos

* **Somebooks**: Compartir una impresora del controlador de dominio con Windows Server 2016 (http://somebooks.es/compartir-una-impresora-del-controlador-dominio-windows-server-2016/)