# Windows Server

![Windwos Server 2012](/assets/WindowsServer2012-2.png)

<div class="alert alert-info">
És un sistema operatiu dissenyat per servidors que treballa sobre un model denominat **domini**.
<div>

Un **domini **és un conjunt d’equips (clients i sevidors) que comparteixen una política de seguretat i una base de dades comú. 

Cada domini té un nom únic.

El **controlador de domini** és una part essencial dels sistemes operatius de Microsoft. S’encarrega fonamentalment d’emmagatzemar les parelles usuari-contrasenya dels comptes d’usuari que tenen accés al domini de xarxa.

Aquest controlador centralitza la funció d’autenticar l’accés al domini

## Microsoft Windows Server 2012 R2

El llançament comercial de **Microsoft Windows Server 2012 R2** va tenir lloc l’any 2012.
Actualment la versió més recent és la Microsoft Windows Server 2016.

Els 3 trets diferenciadors que cal destacar en aquest sistema operatiu són els següents:

  * **Utilització d’una tècnica modular**. Dissenyat de manera independent els components del sistema operatiu. Permet eliminar o instal·lar components nous amb facilitat.
  * **Entorn de preinstal·lació i prearrencada**. 
  * **Control de comptes d’usuari**. Les aplicacions s’executaran sempre sota els privilegis d’un compte d’usuari. El control de comptes d’usuari (UAC, user account control) millora la seguretat de l’equip.
  * L’ús d’un **nou sistema d’arxius ReFS**.

Cal tenir present que una màquina gestionada amb el Microsoft Server 2012:

  * No pot ni hivernar ni entrar en mode suspès.
  * No es pot restaurar.
  * Té limitacions pel que fa a l’estalvi energètic.


![](/assets/WindowsServer2012Icon.png)

## Windows Server 2012 Edicions

* **Windows Server 2012 Foundation**. 
  * Per a petites empreses. 
  * Servidors amb 1 processador. 
  * Limitat a 15 usuaris.
* **Windows Server 2012 Essentials**. 
  * Per a petites/mitjnes empreses. 
  * Servidors amb un o dos processadors. 
  * Limitat a 25 usuaris. 
  * Limitacions en virtualització.
* **Windows Server 2012 Standard**. 
  * Limitat a un màxim de 2 instàncies virtuals.
  * Sistema de llicències per processador.
* **Windows Server 2012 Datacenter**. 
  * Per Datacenters amb alta virtualització.
  * Sense limitació d’instàncies virtuals.
  * Sistema de llicències per processador.

![](/assets/WindowsServerEdicions.png)

