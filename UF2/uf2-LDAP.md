# Instal·lació d'un controlador de domini LDAP

## Instal·lació OpenLDAP

La instal·lació consisteix en instal·lar el paquet **_slapd_**.

  `sudo apt-get update`

  `sudo apt-get install slapd`

* **Slapd **(_Independent LDAP Daemon_) és un programa multiplataforma, que s'executa en segon pla, atenent les sol·licituds d'autenticació LDAP que es rebin al servidor.

Durant l’instal·lació, us demana que introduïu una contrasenya de l’administrador del servei LDAP.

![](/assets/slapd_instalacio.png)

## Instal·lació d'utilitzats d'administració de LDAP

També instal·larem el paquet **_ldap-utils_** que conté les utilitats d'administració de LDAP.
* Conté comandes per realitzar consultes i modificacions a la base de dades del servei LDAP.

Com que aquest paquet es troba en els repositoris oficials d'Ubuntu, cal escriure la següent comanda:

  `sudo apt-get install ldap-utils`

## Configuració servidor LDAP

Un cop instal·lat **OpenLADP **cal configurar-lo amb la comanda:
  
  `sudo dpkg-reconfigure slapd`

1. La primera pantalla que es mostra, actua com a mesura de seguretat, per assegurar-se que no fem canvis per error.
Cal anar amb compte perquè la pregunta es fa a l'inrevés, és a dir , ens pregunta si volem ometre la configuració del servidor haurem de triar la opció **NO**. 

2. El directori OpenLDAP ha de tenir una arrel de la qual penja la resta d’elements. Com a nom de l’arrel s’utilitza un nom DNS. En el nostre cas utilitzarem el domini **_bosccoma.local_**

3. Nom de l'entitat en la qual estem instal·lant el directori LDAP: **_bosccoma.local_**

4. Se us informarà sobre els possibles gestors de bases de dades per emmagatzemar el directori. Es recomana **HDB** perquè ens permetrà canviar els noms dels subarbres si fos necessari.

5. Esborrar la base de dades anterior del directori quan acabem la configuració de slapd: **SI**.

6. Com s’ha decidit esborrar la base de dades antiga, l'assistent ens pregunta si volem canviar-la de lloc: **NO**.

7. En algunes xarxes pot ser necessari mantenir la versió 2 del protocol LDAP. Pregunta si volem permetre el protocol LDAPv2. En el nostre cas **NO**.

8. La configuració s'ha realitzat amb èxit.

Una vegada configurat el servei, **ens assegurem que funciona** amb l’ordre següent:

  `sudo nmap localhost`
  
* El servei ha d’escoltar en el port 389.

Verifica el seu funcionament amb la comanda `slapcat` que permet veure la base de dades de l’OpenLDAP en format LDIF. 

Per tal d’arrencar o reiniciar el servidor LDAP, executeu l’ordre següent:

   `sudo /etc/init.d/slapd restart`
   
**Més informació**: [Instalación y configuración de OpenLDAP](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m6/instalacin_y_configuracin_de_openldap.html)


## Autentificació LDAP

Com ja hem comentat anteriorment, una de les utilitats més importants d'un servidor LDAP és com a servidor d'**autenticació**. 

**Autentificar **és necessari per entrar en un sistema linux . 

També per accedir a alguns serveis com un **servidor FTP** o a **pàgines privades** en un servidor web. 

En aquest tema veurem les modificacions que cal realitzar en un sistema Linux perquè autentifiqui als usuaris en un **servidor LDAP** en lloc d'utilitzar els clàssics arxius `/etc/passwd`, `/etc/group` i `/etc/shadow`.

### PAM (_pluggable autentication module_)

El **PAM **és un mecanisme que les aplicacions fan servir per a l’autenticació d’usuaris.

El **PAM **està compost per un paquet de llibreries compartides que permeten especificar la manera com les diverses aplicacions autenticaran els usuaris.

**Avantatges**:
* Permet utilitzar sistemes d’autenticació diferents del mecanisme tradicional d’autenticació dels sistemes GNU/Linux.
* Permet desenvolupar programes amb independència de l’esquema d’autenticació.
* La gran majoria de les aplicacions dels sistemes GNU/Linux estan preparades per utilitzar el Linux PAM.

### Configurar el client LDAP

A continuació configurarem un ubuntu desktop per tal que s’autentifiqui amb un domini ja creat en un servidor LDAP.

Per tal que en nostre ubuntu desktop client s'autentiqui per LDAP, instal·larem els paquets i eines necessàries per configurar el client. 

  `sudo apt-get install libnss-ldap`

* Et genera un fitxer a `/etc/ldap.conf`

> **ATENCIÓ**: Si la següent configuració no es fa correctament, el més probable és que la màquina no s'engegui o trigui molt en fer-ho!!!

Els paràmetres de configuració que demana són els següents:
* Servidor LDAP: **ldap://_IP_SERVIDOR_**
* Base del domini (DN): **dc=bosccoma,dc=local**
* Versió de LDAP: **3**
* Crear una base de dades local: **Sí**
* Determinar si es requereix login per accedir a la base de dades: **No**
* CN (common name) de l'usuari administrador del directori LDAP: **cn=admin,dc=bosccoma,dc=local**
* Contrasenya per accedir a LDAP com a root: No posar contrasenya (Intro)

La comprovació es farà validant usuaris un cop s'hagin creat alguns.

### Configurar l’autenticació d’usuaris (NSS i PAM)

Les següents comandes serveixen per indicar al sistema que es puguin autenticar usuaris utilitzant tant base de dades d'usuaris locals (arxius `/etc/password`, `/etc/shadow` i `/etc/group`) com la base de dades del servei LDAP.

La configuració es modifica en el fitxer `/etc/nsswitch.conf`.

`sudo auth-client-config -t nss -p lac_ldap`

`sudo pam-auth-update`

En la segona comanda cal deixar les opcions per defecte.

> A partir ara, quan s'engegui la màquina, buscarà el servidor LDAP per validar els usuaris.
Per tant, cal tenir engegat el servidor abans d'engegar el client, apagar el client abans que el servidor, i no s'hauria de canviar l'adreça del servidor.

### Més configuracions necessàries

> Pag 39 pressentació


### Reconfigurar el client LDAP

Es pot reconfigurar el client LDAP amb la comanda 

`sudo dpkg-reconfigure ldap-auth-config`

