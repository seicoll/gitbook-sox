# Gestió LDAP amb interfície gràfica

## phpLDAPadmin

![phpLDAPadmin](/assets/phpLDAPadmin.jpg)

### Instal·lació phpLDAPAdmin

Per instal·lar una interfície web de gestió del directori LDAP, instal·la al servidor el **phpLDAPadmin** amb la comanda:

  `apt install phpldapadmin`

Per configurar el **phpLDAPadmin** s'han de fer els següents canvis al fitxer `/etc/phpldapadmin/config.php`.

  `sudo nano /etc/phpldapadmin/config.php`

  1. Per tal que phpLDAPadmin accedeixi al nostre domini, cal **canviar la base del domini a dos llocs** `dc=example,dc=com` per `dc=ldapxxx,dc=local`

  > **Important**: Només s'ha de canviar en un lloc (la resta són línies que estan comentades).
  >Les línies que comencen amb **#** o **//** són comentaris i no cal modificar-les.

  ```
  /* Array of base DNs of your LDAP server. Leave this blank to have phpLDAPadmin auto-detect it for you. */
  $servers->setValue('server','base',array('dc=ldapxxx,dc=local'));
  ```

  > Amb l'editor _**nano**_, es pot buscar text amb la combinació de tecles **Ctrl + W**.
  2. **Canviar el DN de l'usuari amb qui s'ha de fer el _login_** a phpldapadmin per administrar LDAP.
  > **Important**: Només s'ha de canviar en un lloc (la resta són línies que estan comentades).

  ```
  /* The DN of the user for phpLDAPadmin to bind with. For anonymous binds or
  'cookie','session' or 'sasl' auth_types, LEAVE THE LOGIN_DN AND LOGIN_PASS
  BLANK. If you specify a login_attr in conjunction with a cookie or session
  auth_type, then you can also specify the bind_id/bind_pass here for searching
  the directory for users (ie, if your LDAP server does not allow anonymous
  binds. */
  $servers->setValue('login','bind_id','cn=admin,dc=ldapxxx,dc=local');
  ```
  
  3. **Canviar el valor inicial dels identificadors d'usuaris i grups** per tal que no coincideixin amb els valors dels usuaris i grups locals.
  Convé canviar-los, per exemple, a **10000 i 10000**.
  Aquests paràmetres es troben en una **línia que cal descomentar i modificar**:
  
  ```
  $servers->setValue('auto_number','min',array('uidNumber'=>10000,'gidNumber'=>10000));
  ```
  
  4. També es poden **evitar avisos innecessaris** descomentant i modificant la següent línia:
  
  ```
  $config->custom->appearance['hide_template_warning'] = true;
  ```
  
### Accedir a phpLDAPadmin

Des de l’ubuntu desktop o qualsevol altre client, aneu a un navegador web i connecteu-vos al phpLDAPadmin posant l'adreça.

  `http://172.30.A.20/phpldapadmin`
  
> Cal substituir _**IP_SERVIDOR**_ per la IP del vostre servidor LDAP.

Us demanarà l'usuari (hauria de ser `cn=admin,dc=ldapxxx,dc=local`) i la seva contrasenya.

![](/assets/uf2-phpldapadmin-login.png)

> Si les dades que apareixen al _login_ no són correctes, cal revisar els canvis fets a l'arxiu `/etc/phpldapadmin/config.php`

### Gestionar usuaris, grups i unitats organitzatives

Per crear usuaris, grups i unitats organitzatives heu d'escollir una d'aquestes opcions:

* **Unitats organitzatives**: _Generico: Unidad organizacional_
* **Grups**: _Generico: Grupo Posix_
* **Usuaris**: _Generico: Cuenta usuario_

![](/assets/uf2-CrearObjectesLDAP.png)

**Dades de l'usuari**:

* **_Número UID_**: (automàtic)
* **_Nom comú (cn):_** el sol posar el nom i cognom de l’usuari.
* **_ID del usuario_**: identificador del compte de l'usuari (login)
* **_Directorio personal_**: /home/**ldapxxx**/usuari

    És preferible posar els usuaris de LDAP en un directori diferent dels usuaris locals (`/home/ldapxxx/...`)
* **_Número GID_**: grup principal al què pertany l'usuari
* **_Contraseña_**: \*\*\*\*\*\* (md5)
* **_Consola de login_**: cap (per defecte agafa `/bin/bash`)


## LAT (_LDAP Administration Tool_)

### Instal·lació LAT

També hi ha programes per entorn gràfic que permeten gestionar LDAP de forma remota com per exemple **LAT (_LDAP Administration Tool_) **o **JXplorer**.

Es pot instal·lar **LAT **des del Centre de Software d'Ubuntu o per comandes:

`sudo apt install lat`

Per posar-lo en marxa és preferible fer-ho des de la consola:

`sudo lat`

Al posar-lo en marxa demanarà amb quin servidor LDAP es vol connectar:

![LAT](/assets/LAT.png)

# Documentació i recursos

* **Apunts SOX Pere Sánchez: [Instal·lació JXplorer](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.8.5) i [Gestió d’usuaris amb JXplorer](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.8.6)**

* **Apunts SOX Pere Sánchez: [Instal·lació LAT](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.8.9) i [Gestió d’usuaris amb LAT](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.8.10)**

* **Apunts SOX Pere Sánchez: [Diferències entre phpldapadmin, JXplorer i LAT](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?cap=1.8.12)**