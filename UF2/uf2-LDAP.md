# Instal·lació d'un controlador de domini LDAP

## Instal·lació OpenLDAP

La instal·lació consisteix en instal·lar el paquet **_slapd_**.

  `sudo apt-get update`

  `sudo apt-get install slapd`

* **Slapd **(_Independent LDAP Daemon_) és un programa multiplataforma, que s'executa en segon pla, atenent les sol·licituds d'autenticació LDAP que es rebin al servidor.

Durant l’instal·lació, us demana que introduïu una contrasenya de l’administrador del servei LDAP.

IMATGE

## Instal·lació ldap-utils

També instal·larem el paquet **_ldap-utils_** que conté les utilitats d'administració de LDAP.
* Conté comandes per realitzar consultes i modificacions a la base de dades del servei LDAP.

Com que aquest paquet es troba en els repositoris oficials d'Ubuntu, cal escriure la següent comanda:

  `apt-get install ldap-utils`

## Configuració servidor LDAP

  `dpkg-reconfigure slapd`

1. La primera pantalla que es mostra, actua com a mesura de seguretat, per assegurar-se que no fem canvis per error.
Cal anar amb compte perquè la pregunta es fa a l'inrevés, és a dir , ens pregunta si volem ometre la configuració del servidor haurem de triar la opció **NO**. 

2. El directori OpenLDAP ha de tenir una arrel de la qual penja la resta d’element. Com a nom de l’arrel s’utilitza un nom DNS que servirà per crear el DN base (Distinguished Name) del directori LDAP. En el nostre cas utilitzarem del domini **_bosccoma.local_**

3. Nom de l'entitat en la qual estem instal·lant el directori LDAP: **_bosccoma.local_**

4. Se us informarà sobre els possibles gestors de bases de dades per emmagatzemar el directori. Es recomana **HDB** perquè ens permetrà canviar els noms dels subarbres si fos necessari.

5. Esborrar la base de dades anterior del directori quan acabem la configuració de slapd: **SI**.

6. Com s’ha decidit no esborrar la base de dades antiga, l'assistent ens pregunta si volem canviar-la de lloc: **SI**.

7. En algunes xarxes pot ser necessari mantenir la versió 2 del protocol LDAP. Pregunta si volem permetre el protocol LDAPv2. En el nostre cas **NO**.
La base de dades antiga s'ha guardat a /var/backups.

8. La configuració s'ha realitzat amb èxit.

