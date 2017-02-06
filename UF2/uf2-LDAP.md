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



