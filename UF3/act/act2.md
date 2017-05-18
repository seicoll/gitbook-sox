<!-- notoc -->

# Activitat 2. Compartir impressores en Windows Server

![](/assets/windowsServer.png)

## Requisits

* Utilitzeu la màquina virtual amb **Windows Server 2012** com a servidor i **Windows 10** com a client. Utilitzeu una xarxa interna i assigneu les adreces IP manualment.

* Activeu la funció d'Active Directory en Windows i creeu un nou **domini** amb el nom **bosccoma.local**

* Creeu un Unitat Organitzativa **_Institut_**, dins d’aquesta un **usuari** amb el vostre nom i un grup **_Informàtics_**.

* Afegiu la màquina amb Windows 10 al domini bosccoma.local.

## Activitat

Donat que no disposem d’un dispositiu d’impressió, instal·larem el PDF Creator al servidor i el farem compartit.

1. Configureu el servidor com a **_Servidor d’Impressió_**.

2. Instal·leu el **PDF Creator** (http://www.pdfforge.org/pdfcreator) al servidor.

3. Comproveu que s'ha instal·lat correctament la impressora PDF Creator fent clic a Inicio\Panel de Control\Impresoras.

4. Obriu el programa PDF Creator, aneu a **_Ajustes del perfil_** activeu la opció **auto-guardado**. Aquesta opció permet que els documents que enviem a imprimir es guardin directament a un arxiu pdf dins de la carpeta indicada. Cal guardar els documents a la carpeta C:\Documents\Impressora

  > No tanqueu el programa mentre feu la pràctica.

6. Imprimiu una pàgina de prova i comproveu que s'ha guardat a la carpeta corresponen.
Compartiu la impressora.

7. Assigneu els permisos necessaris per tal de que els usuaris del grup **_Informàtics_** puguin accedir a la carpeta del servidor C:\Documents\Impressora

8. Inicieu la sessió des de la **màquina client** i instal·leu la impressora del servidor en el client.

9. Feu una impressió de prova des del client per comprovar que funciona.

