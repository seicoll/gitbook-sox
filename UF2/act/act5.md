<!-- notoc -->

# Activitat 5. Instal·lació d’un controlador de domini LDAP i configuració client LDAP.

> imatge

## Requeriments

Es pressuposa que disposeu de dos màquines virtuals:
* Una d'elles és un servidor Ubuntu Server.
* L’altra màquina és un client amb Ubuntu Desktop.
* Les dues màquin estan configurades en xarxa NAT anomenada SOX.

## Activitat

**1. Instal·lació del controlador de domini**

  1.1 Instal·la al teu servidor Ubuntu Server el servei de Directori **OpenLDAP**.

  1.2 Configura el servidor LDAP fent servir l’assistent de configuració i configura el domini: ** _bosccoma.local_**

  1.3 Una vegada configurat el servei, ens assegurem que funciona amb l’ordre següent:

```
  $sudo nmap localhost
``` 

  El servei ha d’escoltar en el port 389.

  1.4 Verifica el seu funcionament amb la comanda `slapcat` que permet veure la base de dades de l’OpenLDAP en format LDIF. 

**2. Instal·lació phpLDAPadmin**

  2.1 Instal·la al servidor el phpLDAPadmin amb la comanda:
apt-get install phpldapadmin

  2.2 Edita el fitxer **/etc/phpldapadmin/config.php** heu de modificar ‘dc=example,dc=com’ per ‘dc=**bosccoma**,dc=**local**’
> Amb l'editor nano, es pot buscar text amb la combinació de tecles **_Ctrl + W_**

  2.3 Des de l’ubuntu desktop, aneu a un navegador web i connecteu-vos al phpldapadmin.

  `http://IP/phpldapadmin`

  2.4 Crea un grup anomenat SMX.

  Opció **_Generico: Grupo Posix_**

  2.5 Crea un usuari anomenat alumne.
	
  **Dades d'usuari:**
  * Número UID: (automàtic)
  * Nom común: (cn) el sol posar el nom i cognom de l’usuari
  * ID del usuario: identificador del compte de l'usuari (login)
  * Directorio personal: /home/users/alumne
    * És preferible posar els usuaris de LDAP en un directori diferent dels usuaris locals (`/home/users/...`)
  * Número GID: grup principal al què pertany l'usuari
  * Contraseña: \*\*\*\*\*\* (md5)
  * Consola de login: cap (per defecte agafa /bin/bash)
.

**3. Connectar el client al domini**

  3.1 Instal·la i configura el client LDAP.
  
  3.2 Configurar l'autenticació d'usuaris en el client.
  
  3.3 Executa les comandes `getent passwd` i `getent group` i fes una captura de pantalla on es vegin el grup i l'usuari que has creat.

  3.4 Valida un usuari del domini des de la consola i fes una captura de pantalla. Actualment al domini només tenim l’usuari **_alumne_** que has creat anteriorment.

  3.5 Tanca sessió i valida l'usuari des del login gràfic. Recorda que cal confingurar el login d’Ubuntu perquè et demani un usuari al iniciar.

3.6 **Ampliació**: Modifica el perfil de l'usuari de forma que aparegui el seu nom al costat del rellotge i fes una captura de pantalla.





