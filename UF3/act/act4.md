<!-- notoc -->

# Activitat 4. Compartir impressores en GNU/Linux amb CUPS

![](/assets/CUPSlogo.png)

## Requisits

* Utilitzeu dues màquines virtuals amb Ubuntu (Client i Servidor).

* Configureu-les per tal de que estiguin connectades a una **xarxa interna** i tinguin una IP privada.

* Fareu servir una impressora virtual que imprimeixi els treballs en documents pdf.

## Activitat

1. En la màquina que farà de **servidor d’impressió**, instal·leu el paquet cups-pdf i comproveu que teniu una nova impressora anomenada CUPS-PDF. 

  **Nota**: Per tal que un client pugui administrar CUPS remotament, executeu la següent comanda i reinicieu el servei:

  ```
  cupsctl --remote-admin
  service cups restart
  ```

  a. Configureu la impressora amb CUPS.

  b. Imprimiu una pàgina de prova i comproveu que es visualitza correctament al directori {HOME}\PDF.

  c. Comparteix la impressora PDF.

2. Des de la **màquina client** instal·la la impressora compartida del servidor (no una de local) i imprimeix una pàgina de prova.

  Comprova que s’ha creat el fitxer PDF al servidor.
  
3. Fes el necessari per tal de que els clients puguin **accedir a la carpeta d’impressions** {HOME}\PDF i recollir el seu treball en pdf. 

  Cal que els clients només puguin accedir en mode lectura utilitzant NFS.
