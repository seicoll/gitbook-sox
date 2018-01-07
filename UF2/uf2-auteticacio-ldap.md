# Autenticació LDAP

## Autenticació d'usuari LDAP

Com ja hem comentat anteriorment, una de les utilitats més importants d'un servidor LDAP és com a servidor d'**autenticació**. 

**Autentificar** és necessari per entrar en un sistema linux . 

També per accedir a alguns serveis com un **servidor FTP** o a **pàgines web privades** en un servidor web. 

En aquest tema veurem les modificacions que cal realitzar en un sistema Linux perquè autentifiqui als usuaris en un **servidor LDAP** en lloc d'utilitzar els clàssics arxius `/etc/passwd`, `/etc/group` i `/etc/shadow`.

## PAM (_pluggable autentication module_)

El **PAM **és un mecanisme que les aplicacions fan servir per a l’autenticació d’usuaris.

El **PAM **està compost per un paquet de llibreries compartides que permeten especificar la manera com les diverses aplicacions autenticaran els usuaris.

**Avantatges**:
* Permet utilitzar sistemes d’autenticació diferents del mecanisme tradicional d’autenticació dels sistemes GNU/Linux.
* Permet desenvolupar programes amb independència de l’esquema d’autenticació.
* La gran majoria de les aplicacions dels sistemes GNU/Linux estan preparades per utilitzar el Linux PAM.

## Configurar el client LDAP

A continuació configurarem un ubuntu desktop per tal que s’autentifiqui amb un domini ja creat en un servidor LDAP.

Per tal que en nostre ubuntu desktop client s'autentiqui per LDAP, instal·larem els paquets i eines necessàries per configurar el client. 

  `sudo apt-get install libnss-ldap`

* Et genera un fitxer a `/etc/ldap.conf`

> **ATENCIÓ**: Si la següent configuració no es fa correctament, el més probable és que la màquina no s'engegui o trigui molt en fer-ho!!!

Els paràmetres de configuració que demana són els següents:
* Servidor LDAP: **ldap://_IP_SERVIDOR_** (poseu la IP del vostre servidor!!)
* Base del domini (DN): **dc=ldapxxx,dc=local**
* Versió de LDAP: **3**
* Crear una base de dades local: **Sí**
* Determinar si es requereix login per accedir a la base de dades: **No**
* CN (common name) de l'usuari administrador del directori LDAP: **cn=admin,dc=ldapxxx,dc=local**
* Contrasenya per accedir a LDAP com a root: No posar contrasenya (Intro)

La comprovació es farà validant usuaris un cop s'hagin creat alguns.

### Configurar l’autenticació d’usuaris (NSS i PAM)

Les següents comandes serveixen per indicar al sistema que es puguin autenticar usuaris utilitzant tant base de dades d'usuaris locals (arxius `/etc/password`, `/etc/shadow` i `/etc/group`) com la base de dades del servei LDAP.


```
sudo auth-client-config -t nss -p lac_ldap
sudo pam-auth-update
```

> En la **segona comanda** s'ha de marcar l'opció **_Create home directory on login_**.
Si no se selecciona, no es crearà automàticament el directori de l'usuari i no podrà iniciar sessió (en el mode gràfic) o no tindrà un directori on guardar els seus arxius.

![](/assets/uf2-nsspam.png)

L'execució d'aquestes comandes, modifica la configuració de NSS en el fitxer `/etc/nsswitch.conf`.

> A partir ara, quan s'engegui la màquina, buscarà el servidor LDAP per validar els usuaris, per tant:
* **Cal tenir engegat el servidor** abans d'engegar el client.
* **Cal apagar el client abans que el servidor**.
* **No s'hauria de canviar l'adreça del servidor** (si es canvia, cal reconfigurar el client LDAP).


<!--
NO NECESSARI
Més configuracions necessàries

Per tal que que es crei un directori per l’usuari de forma automàtica quan s’inicia la sessió, editem el fitxer `/etc/pam.d/common-session` i afegim la següent línia just després del comentaris inicials:

`session required pam_mkhomedir.so skel=/etc/skel umask=0022`

-->

### Comprovació autenticació LDAP

Si s'ha configurat correctament el client LDAP, es podran veure els usuaris i grups LDAP amb la comanda `getent`:

`getent passwd`

```bash+theme:dark
usuari@ucxxx:~$ getent passwd
root:x:0:0:root:/root:/bin/bash
...
usuari:x:1000:1000:usuari,,,:/home/usuari:/bin/bash
usuariLDAP:*:10000:10000:usuariLDAP:/home/users/usuariLDAP:/bin/bash
```

S'haurien de veure tots els usuaris i grups, tant els locals com els configurats amb LDAP.

Els **usuaris i grups LDAP** tenen un * en lloc d'una x en el segon camp.

Si no es veuen els usuaris i grups LDAP, s'ha de tornar a reconfigurar el client LDAP.

<!--, l'identificador ha de ser superior o igual a 10000 i la carpeta personal ha d'estar dins de `/home/ldapUsuari`.-->

## Validar usuaris per consolar

Ara podem **validar-nos amb un usuari de LDAP a través de terminal** fent:

`sudo login usuariLDAP`

i veurem que s'ha creat la carpeta home per aquest usuari de LDAP. 

Per comprovar quin és el **directori de treball** de l'usuari es pot utilitzar la comanda `pwd`.

## Validar usuaris amb entorn gràfic

Per últim hem d'**activar el login d’Ubuntu** a la màquina client per poder escriure el nom de l’usuari. 

Cal crear el fitxer `/etc/lightdm/lightdm.conf` i afegim les línies següents:

```
[Seat:*] 
greeter-hide-users=false
greeter-show-manual-login=true
```

* **greeter-hide-users**: amaga (true) o mostra (false) la llista dels últims usuaris que han accedit.
* **greeter-show-manual-login**: si és true, obliga a introduir manualment l'identificador de l'usuari.

Per carregar aquesta configuració cal reiniciar **lightdm **(es tancarà la sessió):

`sudo service lightdm restart`

Per acabar, es convenient reiniciar el sistema i comprovar que pot entrar amb un usuari del domini.

> No cal indicar res especial per distingir usuaris locals o usuaris LDAP.

## Reconfigurar el client LDAP

Es pot reconfigurar el client LDAP amb la comanda 

`sudo dpkg-reconfigure ldap-auth-config`

## Anul·lar la validació d'usuaris LDAP

Per fer que un client deixi de validar usuaris LDAP cal executar la següent comanda:

`sudo auth-client-config -t nss -p lac_ldap -r`

