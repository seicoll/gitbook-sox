<!-- notoc -->

# Activitat 6. Administració de OpenLDAP.

**OpenLDAP** té eines gràfiques de gestió com per exemple **phpLDAPadmin**.

![](/assets/phpLDAPadmin.jpg)

## REQUERIMENTS

Per començar aquesta activitat necessitem 
* **Ubuntu Server** (amb OpenLDAP instal·lat i domini bosccoma.local creat)
* **Ubuntu Desktop**

Tots dos amb xarxa NAT.

Recorda que per configurar un nou domini cal executar al servidor:

`dpkg-reconfigure slapd`

## ACTIVITAT

1. Des de l’ubuntu desktop, aneu a un navegador web i connecteu-vos al phpldapadmin.

  `http://IP/phpldapadmin`

  > Captura del phpLDAPadmin un cop has iniciat sessió

2. Afegeix al domini **_bosccoma.local_** la següent estructura d’objectes:

  ![](/assets/LDAP Domain.png)

  > Captura del phpLDAPadmin on es vegi les OUs creades.


3. Crea els següents usuaris en la unitat organitzativa indicada i assignant-los al grup corresponent:

  | Unitat organitzativa | Nom usuari | Grup |
  | ------------- |:-------------:| -----:|
  | Gestió | conserge | administratius |
  | Gestió | secretaria | administratius |
  | ESO | alumne1ESO | alumnes |
  | ESO | profeESO | profes|
  | Cicles | alumne1SMX | alumnes |
  | Cicles | alumne2SMX | alumnes |
  | Cicles | profeCicle | profes |

4. Comprova que pots iniciar sessió des del login gràfic amb els usuaris **_conserge_**, **_profeESO _**i **_alumne1SMX_**.

  Configura el sistema fent que surti el nom de l'usuari al costat del rellotge i fes captures de pantalla.
	
  > 3 captures de pantalla, una per cada usuari

5. Finalment, exporta-ho en format LDIF.
	Captura mostrant com s’exporta en el phpLDAPadmin
	
## AMPLIACIÓ

A part del phpLDAPAdmin, també hi ha altres programes en entorn gràfic que permeten gestionar LDAP de forma remota.
Instal·la el **JXplorer** i el **LAT** i crea un nou usuari al LDAP amb cadascun d’ells.

[Tutorial Instal·lació JXplorer](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf2/A221-LDAPServer.html#toc_14) i [Gestió d’usuaris amb JXplorer](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf2/A222-LDAP-Usuaris.html#toc_3)
[Tutorial instal·lació LAT](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf2/A221-LDAPServer.html#toc_15) i [Gestió d’usuaris amb LAT](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf2/A222-LDAP-Usuaris.html#toc_6)






