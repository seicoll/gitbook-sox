<!-- notoc -->

# Activitat 1. Compartir recursos i seguretat en Windows Server

## Requisits

* Utilitzeu la màquina virtual amb **Windows Server 2012** com a servidor i **Windows 10** com a client. Utilitzeu una xarxa interna i assigneu les adreces IP manualment.

* Activeu la funció d'Active Directory en Windows i creeu un nou **domini** amb el nom **bosccoma.local**

* Creeu un Unitat Organitzativa **_Institut_**, dins d’aquesta un **usuari** amb el vostre nom i un grup **_Informàtics_**.

* Afegiu la màquina amb Windows 10 al domini bosccoma.local.

## Activitat

1. Entreu al servidor i creeu la carpeta `C:\Documents\Compartit`.

2. Compartiu la carpeta tenint en compte que dins d'aquest recurs ningú hi tindrà accés, ni a través de la xarxa ni localment, excepte el grup Informàtics, que tindrà accés de lectura i el grup d'administradors, que hi tindrà accés total. 

3. Des del **servidor**, feu ús de la comanda `net share` per veure els recursos compartits. Comprova que apareix el nou recurs compartit.

4. Des del **client** amb el vostre usuari comproveu que teniu accés al recurs compartit. Comproveu que teniu accés total.

5. Feu ús de la comanda `net use` per connectar al recurs publicat a la unitat Z:. 

6. Creeu una carpeta al servidor, `C:\Documents\InformaticaDocs`, i compartiu-la de forma **oculta**, amb permisos de control total per al grup Informàtics.

7. Expliqueu com faríeu servir la comanda `net use` per connectar-vos des de la màquina client a aquest recurs amb el vostre usuari.
