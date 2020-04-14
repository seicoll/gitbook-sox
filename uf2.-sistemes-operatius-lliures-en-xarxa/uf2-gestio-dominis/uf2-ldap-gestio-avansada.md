# Gestió avançada de LDAP

## Instal·lació LDAPscripts

Primer de tot, en el servidor cal instal·lar el paquet ldapscripts:

`sudo apt install ldapscripts`

Configurar els paràmetres del fitxer `/etc/ldapscripts/ldapscripts.conf` \(se suposa que ja s'han creat les unitats organitzatives **usuaris**, **grups** i **maquines**\):

```text
SERVER="ldap://localhost"
SUFFIX="dc=ldapxxx,dc=local"
USUFFIX="ou=usuaris"
GSUFFIX="ou=grups"
MSUFFIX="ou=maquines"
BINDDN="cn=admin,dc=ldapxxx,dc=local"
BINDPWDFILE="/etc/ldapscripts/ldapscripts.passwd"
UIDSTART=10000
GIDSTART=10000
MIDSTART=20000
GCLASS="posixGroup"
USHELL="/bin/bash"
UHOMES="/home/ldapxxx/%u"
```

Guardar la contrasenya en un arxiu per permetre l'accés :

```text
sudo sh -c "echo -n 'contrasenyaLDAP' > /etc/ldapscripts/ldapscripts.passwd"
sudo chmod 400 /etc/ldapscripts/ldapscripts.passwd
```

## Comandes per gestionar usuaris

Algunes comandes que es poden utilitzar \(sempre amb `sudo`\):

* `ldapadduser usuari grup`
* `ldapsetpasswd usuari`
* `ldapdeleteuser usuari`
* `ldapaddgroup grup`
* `ldapdeletegroup grup`
* `ldapsetprimarygroup usuari grup`
* `ldapaddusertogroup usuari grup`
* `ldapdeleteuserfromgroup usuari grup`

> Els usuaris es creen amb una plantilla diferent que la que utilitza **phpldapadmin**, per tant poden haver-hi camps diferents.

Es pot fer la prova creant un usuari amb aquests scripts i observar la diferència amb **phpldapadmin** o amb **ldapsearch**.

### Inconvenients d'aquest mètode

* No hi ha comandes per crear, modificar o eliminar unitats organitzatives.
* Tots els usuaris es creen en la unitat organitzativa configurada en l'arxiu `/etc/ldapscripts/ldapscripts.conf`.
  * Si es volen crear en altres unitats organitzatives, s'ha d'anar canviant la configuració en aquest arxiu.

## Altres comandes per gestionar LDAP

### Exemples de comandes per obtenir dades dels objectes

**Obtenir tots els objectes amb tots els atributs**

`ldapsearch -x -LLL -b dc=ldapxxx,dc=local '(&)'`

**Obtenir les classes d'un objecte**

`ldapsearch -x -b "cn=Director XXX,ou=gestio,ou=usuaris,ou=xxx,dc=ldapxxx,dc=local" objectclass`

**Esborrar una entrada** L'entrada no ha de contenir subelements

`dapdelete -D "cn=admin,dc=ldapxxx,dc=local" -W -x "cn=Director XXX,ou=gestio,ou=usuaris,ou=xxx,dc=ldapxxx,dc=local"`

### Exemples de comandes per obtenir diferents dades de l'esquema

**Obtenir totes les classes de l'esquema**

`ldapsearch -x -s base -b "cn=subschema" objectclasses`

**Obtenir tots els tipus d'atributs**

`ldapsearch -x -s base -b "cn=subschema" attributeTypes`

**Obtenir totes les regles aplicables als atributs**

`ldapsearch -x -s base -b "cn=subschema" matchingrules`

## Documentació i recursos

* **Apunts SOX Pere Sánchez:** [Gestió d'usuaris i grups LDAP amb scripts](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.9.19)
* **Apunts SOX Pere Sánchez:** [Altres comandes per gestionar LDAP](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.9.21)

