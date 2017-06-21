# Compartir impressores en Windows

El protocol que utilitza Windows (**SMB/CIFS**) ja ve implementat en el sistema, encara que no sigui un Windows Server, i per tant no cal instal·lar res per poder-lo utilitzar, però si es disposa d'un servidor, i sobre tot si es disposa d'un domini, el més recomanable és instal·lar el **Servei d'impressió (_Print Server_)**, que amplia les possibilitats d'administració de les impressores compartides.

Aquest servei s’encarregarà de compartir les impressores dins una xarxa i gestionar la cua d’impressió on es guaden de forma ordena els documents que rep per imprimir. Fins i tot, permet instal·lar impressores automàticament en els clients a través de directives.

Per instal·lar el **Servidor d'impressió** en el servidor, cal afegir la funció de **Serveis d’Impressió** seguint els següents passos:

1. Anem a l’**_Administrador del Servidor_**.
2. Afegir rols i característiques i afegim els rol **_Print and Document Services_**.
3. Seleccionem únicament **_Print Server_**.
4. I fem instal·lar.

Finalment, podem obrir l'administrador d'impressió anant a **_Eines > Administrador d'impressió_**.

![](/assets/win-print-management.png)