# Compartir impressores amb CUPS

## Servei d'impressió CUPS

**CUPS _(common Unix printing system)_** eina que ens proporciona un sistema d’impressió que ens permet **centralitzar, compartir i gestionar impressores** instal·lades en una màquina que fa les tasques de servidor d’impressió.

Permet que un ordinador actuï com a servidor d’impressió.

Un ordinador que executa el **CUPS **actua com un servidor que pot acceptar tasques d’impressió des d’altres ordinadors clients, les processa i les envia a la impressora apropiada.
La gran majoria de distribucions GNU/Linux utilitzen el CUPS com a sistema d’impressió per defecte.

Quan el **CUPS **es fa servir amb el **Samba**, les impressores també es poden utilitzar en ordinadors **Windows **remots per imprimir per mitjà de la xarxa.


### Instal·lació i configuració del CUPS

La instal·lació de CUPS en Ubuntu no és necessaria perquè ja ve instal·lat per defecte. 

El paquet **cups **instal·la el servidor d'impressió CUPS que permet instal·lar, configurar i compartir impressores. 

Es podria instal·lar amb la comanda:

`sudo apt-get install cups`

### Administrar el servidor d'impressió CUPS

Per poder-lo configurar i administrar el servidor CUPS disposes de:
* **comandes **de l’intèrpret d’ordres
* **interfície web** que funciona sobre el port 631.
  
La interfície web permet afegir, cercar i eliminar impressores i controlar els treballs en les cues d’impressió.

S'hi pot accedir des de:
> http://IP_servidor:631

### Permetre la configuració remota a través de la interfície web

La interfície web per l'administració remote de CUPS està per defecte deshabilitada. 

Per permetre l'accés remot utilitzarem la comanda `cupsctl`.
amb el paràmebre `--remote-admin` que habilita l'accés remot però només des de la xarxa local

`sudo cupsctl --remote-admin`

## Instal·lació d'una impressora en xarxa

## Instal·lació de la impressora CUPS-PDF en xarxa

El que sí instal·larem és el paquet cups-pdf que ens instal·la una eina que ens permet crear fitxers PDF a partir del CUPS, com si fos una impressora. 
És similar al PDFCreator del Windows.
sudo apt-get install cups-pdf


## Instal·lació en el client d'una impressora compartida



