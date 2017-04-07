<!-- notoc -->

# Activitat 3 Instal·lació Active Directory

![Active Directory](/assets/ActiveDirectory.png)

## Activitat

Instal·la el **Active Directory** i converteix el servidor en controlador de domini primari. 

**Documenta la pràctica **i anota-hi tots els problemes que has trobat durant la instal·lació.

#### 1. Instal·lació del Directori Actiu

La instal·lació del **Directori Actiu** és la implementació d'una funció bàsica o rol del nostre Windows 2012 Server. Com qualsevol altre rol de servidor el podem instal·lar des l’**_Administrador del servidor_**.

1. Obrir l’Administrador del servidor i seleccionar al panell esquerre l'opció **Administrar **i **Afegir funcions i característiques** amb el que s’obrirà l'assistent per afegir funcions. 

2. Després d’algunes pantalles d'informació anirem amb el botó de **Següent **fins a la llista de possibles funcions per instal·lar en el sistema. 

3. Marcar l'opció **Serveis de Domini d'Active Directory (AD DS)** i **DNS Server** i prémer el botó de **Següent**.

4. Un cop finalitzada la instal·lació ens apareix una pantalla informativa on ens adverteix que per convertir el servidor en un controlador de domini funcional cal **obrir l'assistent per crear un nou domini.**

#### 2. Creació del domini

Un cop instal·lats els serveis bàsics de **Directori Actiu** és necessari completar la instal·lació mitjançant la **creació d'un nou domini i la promoció de l'equip a controlador de domini** mitjançant els següents passos:

1. En l’Administrador del servidor ens apareix una notificació indicant que es requereix una confinguració del AD i mostra l’opció de **_Promover este servidor a controlador de dominio_**.

2. Després de la pantalla d'inici de l’assistent hi ha tres opcions: 

    * Afegir l'equip com a controlador de domini a un domini ja existent. 

    * Afegir un nou domini en un bosc existent.

    * Afegir un nou bosc.

3. Com que no tenim encara cap domini creat escollim la tercera opció **_Afegir un nou bosc_**.

4. A continuació has d'introduir el nom complet del domini arrel que serà el primer del nostre bosc. Aquest nom ha de complir l'estructura DNS (Domain Name System) amb sufix inclòs amb el que definirem el nom del bosc i l'espai de noms, per exemple **bosccoma.local. **Introdueix ara** bosccoma.local** i prem **Següent**.

5. Després de comprovar si el nou nom de bosc ja existís, l'assistent ens convida a determinar el nivell de funcionalitat del sistema que es determinem en funció de la compatibilitat per integrar amb altres dominis gestionats per versions anteriors. En el nostre cas, per assegurar la compatibilitat amb Windows 2008 R2 cal seleccionar l'opció **_"Nivell de funcionalitat Windows 2012 R2"_** i prem **Següent**.

6. Després d'examinar la configuració DNS i, en el cas de no estar instal·lat aquest servei, has de deixar marcada la casella "**Servidor DNS**" i prémer Següent doncs **cal tenir instal·lat el servei de resolució de noms per al correcte funcionament del Directori Actiu.**

7. L'assistent ens demana ara una **contrasenya **per poder administrar el **Directori Actiu** en determinades circumstàncies. En general, encara que poden ser diferents, sol ser convenient posar la mateixa contrasenya que l'administrador de l'equip. Introdueix doncs la contrasenya de l'administrador i prem **Següent**.

8. A continuació s'ha d'indicar la localització dels arxius bàsics que utilitzarà el Directori Actiu: la carpeta per a base de dades, la carpeta d'arxius de registre i la carpeta SYSVOL que conté els arxius públics del domini que han de ser compartits.

9. Se'ns informa a continuació mitjançant un **resum**, de tota les configuracions que hem seleccionat. En aquest punt podríem Exportar Configuració... és a dir, guardar aquestes seleccions en un arxiu per utilitzar-les en futures instal·lacions automàtiques.

10. En prémer **Següent **comença la instal·lació de **Directori Actiu** i el procés de **promoció de l'equip a Controlador de Domini**, que poden portar més o menys temps en funció de l'entorn i de les opcions seleccionades. 

11. Finalment apareix una pantalla informativa un cop acabada la instal·lació. Prémer **Finalitza **i després **Reiniciar l'Equip** perquè el Directori Actiu s’iniciï i estigui operatiu.

12. Si tot ha funcionat correctament, el nostre equip ja està **convertit en un controlador de domini** del Directori Actiu per gestionar de forma centralitzada els recursos de la xarxa.

#### 3. Unir equips al domini

1. Configureu una **xarxa interna** en VirtualBox amb un servidor Windows 2012 com a controlador de domini i un ordinador client Windows 7.

2. Configureu la tarjeta de xarxa de les màquines virtuals en mode de **Xarxa interna**.

3. Assigneu IP Estàtica a la màquina servidor (per exemple 192.168.0.10) i a la màquina client (192.168.0.20). El controlador de domini també dona servei DNS al client per tant, al client, **cal posar com a servidor DNS principal la IP del servidor de domini**.

4. Fes pings per a verificar que el client pot comunicar-se amb el servidor.

5. Entreu a la màquina client i **afegiu-la al domini**, canviant el mode de grup de treball al mode de domini. Necessitareu les credencials d'administrador del domini. 

6. Ara entreu a la màquina client i veureu que podeu entrar al domini mitjançant les credencials de l'administrador. Posa una captura de pantalla que mostri que has pogut accedir.

7. **Entra al servidor i busca el nou equip **a Eines administratives > Usuaris i equips de l’Active Directory.



