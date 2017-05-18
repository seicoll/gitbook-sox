<!-- notoc -->

# Activitat 3. Samba 4 com a controlador primari de domini (AD DC)

En aquesta activitat configurarem el servidor Linux amb el **Samba 4** per tal que faci de controlador de domini de forma similar a l’Active Directory. A continuació, administrarem el domini, de forma remota, des d’un client Windows a través de l’eina d’administració RSAT.

## Requisits

Treballarem amb dues màquines virtuals. Una amb **Ubuntu Server** que farà de servidor on instal·larem el Samba 4. I l’altra amb **Windows **que farà de client on instal·larem l’eina RSAT.
Configurar-les perquè estiguin connectades a una xarxa interna i tinguin una IP privada.

## Activitat 

**Part 1: Configuració del servidor**

Instal·la **Samba 4** i configura’l com Controlador de domini (DC).
Crea un domini **_ELTEUNOM.local_**

> **Alerta**: Si al fer smbclient -L localhost -U% et surt un error que diu:
session setup failed: NT_STATUS_OBJECT_NAME_NOT_FOUND
> És necessari que instal·lis el paquet winbind
sudo apt-get install winbind

**Part 2: Administració amb RSAT**

2.1 Uneix el client Windows al domini Samba creat en el servidor Linux. 

2.2 Instal·la l’eina d’administració remota RSAT de Windows.

2.3 Amb l’eina d’Administració d’usuaris i equips del domini crea les següents unitats organizatives, usuaris i grups:
* (OU) grups			
  * alumnes		
  * professors		
* (OU) usuaris				
  * alumne1 (membre del grup alumnes)			
  * alumne2 (membre del grup alumnes)
  * profe1 (membre del grup professors)			
  * profe2 (membre del grup professors)
		
**Part 3: Perfils mòbils**

3.1. Crea en el **Servidor **dins de `/srv/samba` les següents carpetes:

* perfils
* privades
* compartida

3.2. Utilitzant Samba, comparteix aquestes carpetes amb permisos de lectura i escriptura per a tothom.

  > Captura de pantalla del fitxer de configuració de Samba.

3.3. Des del **Client**, posa els permisos adequats a les carpetes **perfils **i **privades **de forma que, quan es creï la carpeta per cada usuari, només els propietaris tinguin control total.

  > Captura de pantalla on es vegin els permisos avançats de la carpeta perfils.
  >Captura de pantalla on es vegin els permisos avançats de la carpeta privades.

3.4. Posa els permisos adequats a la carpeta **compartida **de forma que tots els usuaris del grup alumnes només han de poder llegir; els usuaris del grup **professors **i **administradors del domini** han de tenir control total.

  > Captura de pantalla on es vegin els permisos avançats de la carpeta compartida.

3.5. Fes que tots els usuaris tinguin el perfil mòbil en la **carpeta **perfils del servidor.

  > Captura de pantalla de la configuració en un usuari.

3.6. També han de tenir una carpeta **privada **en el servidor, dins de la carpeta privades, a la qual han d'accedir a través de la unitat de xarxa **Z:** que s’ha de connectar automàticament al iniciar la sessió.

  >Captura de pantalla de la configuració en un usuari.

3.7. Quan iniciïn sessió, s'han de connectar a la carpeta **compartida **a través la unitat de xarxa **X:**

3.8. **En el client Windows**, inicia sessió amb un alumne i un professor.
Comprova en quines carpetes (unitats de xarxa Z:, X:) no poden accedir o no tenen permís d'escriptura.