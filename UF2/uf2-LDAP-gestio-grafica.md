# Gestionar LDAP amb interfície gràfica

## Instal·lació phpLDAPAdmin

Per instal·lar una interfície web de gestió del directori LDAP, instal·la al servidor el **phpLDAPadmin** amb la comanda:

  `apt-get install phpldapadmin`

Edita el fitxer `/etc/phpldapadmin/config.php`

  `sudo nano /etc/phpldapadmin/config.php`

I modifiqueu `dc=example,dc=com` per `dc=bosccoma,dc=local`

> Amb l'editor nano, es pot buscar text amb la combinació de tecles **Ctrl + W**

Des de l’ubuntu desktop, aneu a un navegador web i connecteu-vos al phpldapadmin.

  `http://IP/phpldapadmin`
