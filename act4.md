# Activitat 4. Zentyal com a controlador primari de domini

En aquesta activitat configurarem el servidor Linux amb **Zentyal** per tal que faci de controlador de domini de forma similar a l’Active Directory.

## Requisits

Treballarem amb dues màquines virtuals. Una amb **Zentyal** que farà de servidor i l’altra amb **Windows** que farà de client.

Configurar-les perquè estiguin connectades a una xarxa interna i tinguin una IP privada.

## Activitat

### Part 1: Configuració del servidor

Configura el **Zentyal** com

Controlador de domini \(DC\). Crea un domini _**ELTEUNOM.local**_

**Part 2: Configuració del client**

Uneix el client Windows al domini creat en el servidor Zentyal. 1. Primer de tot comprovarem la connectivitat fent un ping al vostre servidor de domini.  
2. Si el ping funciona, anirem a “Mi PC” i afegirem l’equip al domini que hem creat al Zentyal. 3. Ens demanarà el compte d’_**Administrador**_ i la seva contrasenya per tal de poder completar l’operació.  
4. Reiniciem la màquina i ja tenim l’equip agregat al domini.

> Captura de pantalla.

### Part 2: Administració del domini

Crea les següents unitats organizatives, usuaris i grups:

* \(OU\) groups            
  * alumnes        
  * professors        
* \(OU\) users

  * alumne1 \(membre del grup alumnes\)            
  * alumne2 \(membre del grup alumnes\)            
  * profe1 \(membre del grup professors\)            
  * profe2 \(membre del grup professors\)

  > Captura de pantalla on es vegin tots els usuaris creats.

### Part 3: Perfils mòbils

Un perfil és un entorn personalitzat especialment per a un usuari. El perfil conté la configuració de l’escriptori i dels programes de l’usuari. Cada usuari té un perfil, tant si l’administrador ho configura com si no, perquè el perfil es crea automàticament per a cada usuari quan s’inicia sessió en un equip.

Podem configurar els _**perfils mòbils**_ per tal que els usuaris tinguin els mateix escriptori i accés als seus documents i configuracions des de qualsevol equip on es connectin. Trobem l’opció de configuració de perfils mòbils a _**Zentyal. Domain &gt; Settings &gt; Marcar “enable roaming profiles”**_ .

El servidor **Zentyal** guarda els perfils mòbils a /home/samba/profiles

### Part4: Creació carpetes compartides

Des de _**Compartició de fitxers \[File Sharing\]**_ podeu crear tots els recursos compartits que necessiteu tal com ho podíeu fer amb el Samba.

1. Crea en el Servidor Zentyal les següents carpetes compartides:
   * notes
   * compartida
2. Prement l’icona de _**Control d’accés**_, posa els permisos adequats a les carpetes notes de forma que tots els usuaris del grup professors puguin llegir i escriure.

   > Captura de pantalla on es vegin els permisos de la carpeta notes. Captura de pantalla des del client windows on es vegi que un professor hi pot crear un document.

3. Posa els permisos adequats a la carpeta **compartida** de forma que tots els usuaris del grup alumnes només han de poder llegir i els usuaris del grup **professors** han de tenir control total.

   > Captura de pantalla on es vegin els permisos avançats de la carpeta compartida. Captura de pantalla des del client windows on es vegi que un professor hi pot crear un document. Captura de pantalla des del client windows on es vegi que un alumne NO hi pot crear un document.

### Ampliació

**Uneix un client linux al domini**

Uneix el client Ubuntu Desktop al domini creat en el servidor Zentyal. [http://www.tecmint.com/integrate-ubuntu-system-in-zentyal-pdc/](http://www.tecmint.com/integrate-ubuntu-system-in-zentyal-pdc/)

**Més informació:** [http://www.tecmint.com/install-zentyal-as-primary-domain-controller-and-integrate-windows-system/](http://www.tecmint.com/install-zentyal-as-primary-domain-controller-and-integrate-windows-system/)

