# Compartir impressores amb CUPS

## Servei d'impressió CUPS

**CUPS** _**\(common Unix printing system\)**_ eina que ens proporciona un sistema d’impressió que ens permet **centralitzar, compartir i gestionar impressores** instal·lades en una màquina que fa les tasques de servidor d’impressió.

Permet que un ordinador actuï com a **servidor d’impressió**.

Un ordinador que executa el **CUPS** actua com un servidor que pot acceptar tasques d’impressió des d’altres ordinadors clients, les processa i les envia a la impressora apropiada.

La gran majoria de distribucions GNU/Linux utilitzen el CUPS com a sistema d’impressió per defecte.

Quan el **CUPS** es fa servir amb el **Samba**, les impressores també es poden utilitzar en ordinadors **Windows** remots per imprimir per mitjà de la xarxa.

![](../../.gitbook/assets/cupslogo.png)

### Instal·lació del servei d'impressió CUPS

La instal·lació de **CUPS** en Ubuntu no és necessaria perquè ja ve instal·lat per defecte.

El paquet **cups** instal·la el servidor d'impressió CUPS que permet instal·lar, configurar i compartir impressores en xarxa.

Es podria instal·lar amb la comanda:

```text
sudo apt install cups
```

### Administrar el servidor d'impressió CUPS

Per poder configurar i administrar el servidor CUPS disposes de:

* **comandes** de l’intèrpret d’ordres
* **una interfície web** que funciona sobre el port 631.

La interfície web permet afegir, cercar i eliminar impressores i controlar els treballs en les cues d’impressió.

### Permetre la configuració remota a través de la interfície web

La interfície web per l'**administració remota** de CUPS està per defecte deshabilitada.

Per permetre l'accés remot utilitzarem la comanda `cupsctl`.  
amb el paràmebre `--remote-admin` que habilita l'accés remot però només des de la xarxa local

```text
sudo cupsctl --remote-admin
sudo service cups restart
```

### Configurar CUPS de forma remota a través d'una interfície web

Per accedir de forma remota a la web de configuració del servidor d'impressió, només cal obrir un navegador web i posar l'adreça:

> `https://172.30.A.20:631`

On `172.30.A.20` és la IP del servidor d'impressió.

Si demana un **usuari** i contrasenya per canviar alguna configuració, es pot utilitzar qualsevol usuari que pertanyi al grup _**lpadmin**_, per exemple l'usuari principal.

Si no hi ha cap usuari que pertanyi a aquest grup, es pot afegir un usuari a aquest grup amb les següents comandes:

```text
sudo adduser usuari lpadmin
sudo service cups restart
```

## Instal·lació de la impressora CUPS-PDF en xarxa

El paquet **cups-pdf** ens instal·la una impressora virtual que permet crear fitxers PDF. Quan s'envia un document a aquesta impressora, enlloc d'imprimir-se, es converteix a PDF i es guarda en una carpeta predeterminada.

És similar al PDFCreator de Windows.

`sudo apt install cups-pdf`

### Afegir la impressora CUPS-PDF en el servidor CUPS

Per instal·lar una impressora en el servidor CUPS hem de seleccionar l’opció **Add printer** de la pestanya **Administration**.

![](../../.gitbook/assets/cupsadministration.png)

1. Seleccionem la impressora a instal·lar. Per exemple l’impressora local **CUPS-PDF \(Virtual PDF Printer\)**.
2. Cal posar un nom a la impressora, i si es vol, una descripció i lloc on es troba la impressora. 
   * També cal marcar l’opció de **“Share This Printer”** per compartir-la.
3. Ens demanarà el **fabricant** de la impressora. Seleccionem la marca **Generic**.
4. Seguidament, ens demanarà pel **model d'impressora** per instal·lar els controladors més adequats. 
   * També, permet especificar aquests controladors mitjançant un fitxer de text en format PPD \(PostScript printer description\).
   * Seleccionem el model **Generic CUPS-PDF Printer \(en\)**.
5. Si s’instal·la correctament, apareixerà una pantalla que ens permetrà configurar les **opcions generals d’impressió** de la impressora.
6. Amb això ja tenim la impressora configurada.

### Configuració del directori on s'envien els documents PDF

La configuració es troba a l'arxiu `/etc/cups/cups-pdf.conf`, en el paràmetre **Out**.

En el cas d'Ubuntu, envia els documents a una carpeta anomenada **PDF**, dins del directori personal de l'usuari que ha imprès el document \(el valor **${HOME}** equival a `/home/usuari`\):

`Out ${HOME}/PDF`

Per motius de seguretat, el programa CUPS només pot escriure en algunes carpetes, i això ho determina la configuració del programa **apparmor**.

### Configuració d'un directori comú on s'envien els documents PDF

Si es vol que tots els document de la impressora **cups-pdf** vagin a una carpeta comuna, per exemple a `/svr/documents/pdf`, primer s'ha de crear la carpeta on s'han d'enviar els documents generats per la impressora **cups-pdf**, i donar-li permisos de lectura i escriptura per a tothom.

```text
sudo mkdir -p /srv/documents/pdf
sudo chmod 777 /srv/documents/pdf
```

Després, en l'arxiu `/etc/cups/cups-pdf.conf`, posar en el paràmetre **Out** el nou directori.

`Out /srv/documents/pdf`

I reiniciar el servei cups:

`sudo service cups reload`

Finalment s'ha d'afegir aquest directori a la llista de directoris on pot escriure el programa CUPS.  
Això es fa en l'arxiu `/etc/apparmor.d/usr.sbin.cupsd`.

Es pot afegir la línia a continuació de les que configuren els directoris personals.

```text
@{HOME}/PDF/ rw,
/srv/documents/pdf/* rw,
```

I reiniciar el servei **apparmor**:

`sudo service apparmor reload`

## Instal·lació en el client d'una impressora compartida

1. Per tal que el **client** utilitzi les impressores remotes instal·lades en el servidor CUPS, des de l’Ubuntu, anirem al menú **Sistema &gt; Administració &gt; Impressores**.
2. En aquesta pantalla haurem de seleccionar la icona **Afegeix &gt; Impressora** i començarà un procés de cerca de les impressores que detecti l’equip.
3. Al final d’aquest procés se’ns obrirà el quadre Impressora nova
   * Si ens ha detectat la impressora que volem instal·lar, només caldrà que premem el botó Endavant.
   * Si no ens ha detectat la impressora, despleguem l'opció **Impresora de red** i triem **Buscar impressora de red**. En el camp **Equip** posem la IP del servidor on està compartida i cliquem **Buscar**.
4. Ens demanarà el nom mitjançant el qual volem que es reconegui la impressora en el sistema i haurem de fer clic a **Aplica**.
   * De manera opcional, també ens demanarà una descripció d’aquesta impressora i lloc on es troba. 
5. Finalment, el sistema ens proposarà **imprimir una pàgina de prova** perquè puguem estar segurs que la instal·lació s’ha fet correctament.

