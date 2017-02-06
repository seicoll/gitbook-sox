# Gestionar LDAP amb interfície gràfica

## Instal·lació phpLDAPAdmin

Per instal·lar una interfície web de gestió del directori LDAP, instal·la al servidor el **phpLDAPadmin** amb la comanda:

  `apt-get install phpldapadmin`

Per configurar el **phpLDAPadmin** per tal que accedeixi al nostre domini, edita el fitxer `/etc/phpldapadmin/config.php`.

  `sudo nano /etc/phpldapadmin/config.php`

I modifiqueu `dc=example,dc=com` per `dc=bosccoma,dc=local`

> Amb l'editor nano, es pot buscar text amb la combinació de tecles **Ctrl + W**
> Les línies comentades comencen amb # o // són comentaris i no cal modificar-les.

## Accedir a phpLDAPadmin

Des de l’ubuntu desktop o qualsevol altre clien, aneu a un navegador web i connecteu-vos al phpldapadmin posant l'adreça.

  `http://IP_SERVIDOR/phpldapadmin`
  
> Cal substituir _**IP_SERVIDOR**_ per la IP del vostre servidor LDAP.

Us demanarà l'usuari (hauria de ser cn=admin,dc=bosccoma,dc=local) i la seva contrasenya.

Si l'identificador no és correcte, cal revisar els canvis fets a l'arxiu `/etc/phpldapadmin/config.php`
