# Usuaris, grups i unitats organitzatives

## Objectes que administra un domini

Els objectes d'un domini són aquelles **entitats susceptibles de ser administrades en una xarxa d'ordinadors**. 

El directori actiu no és més que una base de dades jerarquitzada d'objectes. 

Els **objectes **que administra un domini són: 

* **Usuaris globals** 
  * Són usuaris reconeguts per tots els equips que formen part del domini.
  * Són gestionats pel Directori Actiu de forma centralizada.
Permet identificar i autenticar els usuaris que poden accedir al sistema.
Permet gestionar els permisos d'aquests usuaris als recursos compartits. 


* **Grups **

  * Els usuaris globals es poden assignar a grups.
  * Facilitar l'administració quan diversos usuaris tenen perfils de seguretat i accés comuns. 


* **Equips** 
  * La base de dades del Directori Actiu també guarda informació dels diferents equips que pertanyen al domini.
  * Com per exemple el nom del ordinador així com un identificador únic que permet assignar drets i permisos.


* **Unitats organitzatives (UO)** 
  * Són objectes de directori que contenen altres objectes com usuaris, grups, equips o altres unitats organitzatives.
