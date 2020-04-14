# Windows Server

És un sistema operatiu dissenyat per servidors que treballa sobre un model denominat **domini**.

Un **domini** és un conjunt d’equips \(clients i sevidors\) que comparteixen una política de seguretat i una base de dades comú.

Cada domini té un nom únic.

El **controlador de domini** és una part essencial dels sistemes operatius de Microsoft. S’encarrega fonamentalment d’emmagatzemar les parelles usuari-contrasenya dels comptes d’usuari que tenen accés al domini de xarxa.

Aquest controlador centralitza la funció d’autenticar l’accés al domini

## Microsoft Windows Server 2016

Actualment la versió més recent és la **Microsoft Windows Server 2019** llançada comercialment l'any 2018. La versió anterior era el **Microsoft Windows Server 2016** .

![](../../.gitbook/assets/windowsserver2016.png)

Els trets diferenciadors que cal destacar en aquest sistema operatiu són els següents:

* **Utilització d’una tècnica modular**. 
  * Dissenyat de manera independent els components del sistema operatiu. 
  * Permet eliminar o instal·lar components nous amb facilitat.
* **Control de comptes d’usuari**. 
  * Les aplicacions s'executaran sempre sota els privilegis d’un compte d’usuari. 
  * El control de comptes d’usuari \(UAC, user account control\) millora la seguretat de l'equip.

Cal tenir present que una màquina gestionada amb el Microsoft Server:

* No pot ni hivernar ni entrar en mode suspès.
* No es pot restaurar.
* Té limitacions pel que fa a l’estalvi energètic.

## Windows Server Edicions

El sistema Windows Server es distribueix empaquetat en diferents **Edicions**.

### Windows Server 2016 i 2019 Edicions

Amb **Windows Server 2016** i **2019** es redueixen el nombre d'edicions respecte al Windows Server 2012, eliminant l'edició _**Foundation**_.

* **Essentials Edition**
  * Per a petites empreses.
  * Servidors amb 1 o 2 processadors. 
  * Limitat a 25 usuaris i 50 dispositius.
* **Standard Edition**
  * Per a petites/mitjanes empreses.
  * Limitacions en virtualització \(màxim 2 màquines virtuals\).
* **Datacenter Edition**
  * Per datacenters amb alta virtualització.
  * Sense limitació d'instàncies virtuals.

En el cas de **Windows Server 2019**, es pot trobar informació de les versions i els preus a: [https://www.microsoft.com/es-es/cloud-platform/windows-server-pricing](https://www.microsoft.com/es-es/cloud-platform/windows-server-pricing)

Aquestes 3 edicions principals es complementen amb 3 opcions més:

* **Store Server Edition**
  * Pot afegir-se a un servidor amb Active Directory per complementar el seu funcionament com a **servidor d'arxius** incorporant aspectes com el protocol NFS \(_Network File System_\).
* **MultiPoint Premium Server Edition**
  * Permet compartir recursos d'un servidor amb diferents usuaris, on cada usuari disposarà d'una estació de treball \(monitor, teclat i ratolí\). Aquesta estació de treball es connecta es connecta a un hub que s'uneix al servidor que aporta la capacitat de càlcul.
  * Només amb llicència educativa.
* **Microsoft Hyper-V Server Edition**
  * Edició gratuïta del hipervisor de Microsoft _**Hyper-V**_.

![](../../.gitbook/assets/windows2016_edicions.JPG)

## Documentació i recursos

* **SomeBooks.es: Ediciones de Windows Server 2016:** [http://somebooks.es/ediciones-windows-server-2016/](http://somebooks.es/ediciones-windows-server-2016/)

