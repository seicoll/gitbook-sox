# Instal·lació d'un controlador de domini LDAP

## Instal·lació OpenLDAP

El programa OpenLDAP s'instal·la com a servei amb el paquet _**slapd**_.

```text
  sudo apt update
  sudo apt install slapd
```

**Slapd** \(_Independent LDAP Daemon_\) és un programa que s'executa en segon pla, atenent les sol·licituds d'autenticació LDAP que es rebin al servidor.

Durant l’instal·lació, només us demana que introduïu una **contrasenya de l’administrador** del servei LDAP.

![](../../.gitbook/assets/slapd_instalacio.png)

## Configuració servidor LDAP

Un cop instal·lat **OpenLADP** cal configurar-lo amb la comanda:

`sudo dpkg-reconfigure slapd`

1. La primera pantalla que es mostra, actua com a mesura de seguretat, per assegurar-se que no fem canvis per error. Cal anar amb compte perquè la pregunta es fa a l'inrevés, és a dir , ens pregunta si volem **ometre la configuració del servidor** haurem de triar la opció **NO**.
2. El directori LDAP ha de tenir una arrel de la qual penja la resta d'elements. Com a **nom de l'arrel de domini** s'utilitza un nom DNS. En el nostre cas utilitzarem el domini _**ldapxxx.local**_ \(xxx són les teves inicials en minúscules\).
3. **Nom de l'entitat** en la qual estem instal·lant el directori LDAP: _**ldapxxx.local**_
4. Se us informarà sobre els possibles gestors de bases de dades per emmagatzemar el directori. Es recomana **HDB** perquè ens permetrà canviar els noms dels subarbres si fos necessari.
5. **Esborrar la base de dades anterior** del directori quan acabem la configuració de slapd: **SI**.
6. Com s’ha decidit esborrar la base de dades antiga, l'assistent ens pregunta si volem **canviar-la de lloc la base de dades antiga**: **NO**.
7. En algunes xarxes pot ser necessari mantenir la versió 2 del protocol LDAP. Pregunta si volem **permetre el protocol LDAPv2**. En el nostre cas **NO**.
8. La configuració s'ha realitzat amb èxit.

**Més informació**: [Instalación y configuración de OpenLDAP](http://www.ite.educacion.es/formacion/materiales/85/cd/linux/m6/instalacin_y_configuracin_de_openldap.html)

## Comprovar el servei LDAP

Una vegada configurat el servei, **ens assegurem que funciona** amb l’ordre següent:

`sudo nmap localhost`

* El servei ha d’escoltar en el port 389.

Verifica el seu funcionament amb la comanda `slapcat` que permet veure la base de dades de l’OpenLDAP en format LDIF.

Per tal d’**arrencar o reiniciar el servidor LDAP**, executeu l’ordre següent:

`sudo /etc/init.d/slapd restart`

## Reconfigurar el servidor LDAP

Si no hem configurat correctament el servei LDAP o volem canviar el nom del domini, es pot tornar a configurar el servei amb la comanda:

`sudo dpkg-reconfigure slapd`

## Instal·lació d'utilitzats d'administració de LDAP

També instal·larem el paquet _**ldap-utils**_ que proporciona algunes comandes per realitzar consultes i modificacions a la base de dades del servei LDAP.

Com que aquest paquet es troba en els repositoris oficials d'Ubuntu, cal escriure la següent comanda:

`sudo apt install ldap-utils`

Per no haver d'indicar la base del domini i el servidor en cada comanda, es pot configurar l'arxiu `/etc/ldap/ldap.conf` :

* Descomentant les línies amb els paràmetres **BASE** i **URI**
* I posant la base del domini i la IP del servidor LDAP \(si hi hagués un servidor de DNS, també es podria utilitzar el nom DNS del servidor de LDAP, per exemple _**usxxx.ldapxxx.local**_\):

  ```text
  BASE   dc=ldapxxx,dc=local
  URI    ldap://172.30.A.20
  ```

Per **comprovar amb ldap-utils que la configuració** del servei LDAP és correcta i veure els elements que hi ha a la base de dades LDAP es pot utilitzar la següent comanda que mostra tots els dn dels objectes del domini \(de moment només el del domini i el de l'usuari admin\):

```text
usuari@usxxx:~$ ldapsearch -x -LLL dn
dn: dc=ldapxxx,dc=local

dn: cn=admin,dc=ldapxxx,dc=local
```

Sense la configuració prèvia de l'arxiu `/etc/ldap/ldap.conf`, la comanda hauria de ser:

```text
usuari@usxxx:~$ ldapsearch -x -LLL -H ldap://172.30.0.20 -b dc=ldapxxx,dc=local dn
dn: dc=ldapxxx,dc=local

dn: cn=admin,dc=ldapxxx,dc=local
```

