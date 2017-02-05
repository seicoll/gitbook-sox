# Instal·lació d'un controlador de domini Active Directory

![Active Directory](/assets/ActiveDirectory.png)

## Instal·lació del Directori Actiu

1. La instal·lació del **Directori Actiu** és la implementació d'una funció bàsica o rol del nostre Windows Server. Com qualsevol altre rol de servidor el podem instal·lar des l’**_Administrador del servidor_** i seleccionar l'opció _**Agregar roles y características**_ que obrirà l'assistent per afegir funcions.

  ![](/assets/AD_afegir.png)

2. Triem l'opció _**Instalación basada en características o en roles**_.

  ![](/assets/AD_ins2.png)

3. Després d’algunes pantalles d'informació on cal escollir a quin servidor el volem instal·lar, anirem amb el botó de **_Següent _** fins a la llista de possibles funcions per instal·lar en el sistema. 

  ![](/assets/AD_ins3.png)

4. Marcar l'opció **_Serveis de Domini d'Active Directory (AD DS)_** i **_DNS Server_** i prémer el botó de **_Següent_**.

5. Un cop finalitzada la instal·lació ens apareix una pantalla informativa on ens adverteix que per convertir el servidor en un controlador de domini funcional cal obrir l'assistent per crear un nou domini seleccionant _**Promover este servidor a controlador de dominio**_.

![](/assets/AD_ins4.png)

## Creació del domini
Un cop instal·lats els serveis bàsics de **Directori Actiu** és necessari completar la instal·lació mitjançant la creació d'un **nou domini** i la promoció de l'equip a controlador de domini mitjançant els següents passos:

1. En l’_**Administrador del servidor**_ ens apareix una notificació indicant que es requereix una confinguració del AD i mostra l’opció de _**Promover este servidor a controlador de dominio**_.

![](/assets/AD_ins5.png)

2. Després de la pantalla d'inici de l’assistent hi ha tres opcions: 
  * **_Afegir l'equip com a controlador de domini a un domini ja existent_**: serveix per afegir un controlador secundari a un domini ja creat. 
  * **_Afegir un nou domini en un bosc existent_**.
  * **_Afegir un nou bosc_**.
  
  Com que no tenim encara cap domini creat escollim la tercera opció _**Afegir un nou bosc**_.

  A continuació has d'introduir el nom complet del domini arrel. Aquest nom ha de complir l'estructura DNS (_Domain Name System_) amb sufix inclòs amb el que definirem el nom del bosc i l'espai de noms, per exemple `bosccoma.local`. 



    
        Imatge
  




3. Després ens demana el nivell de funcionalitat del sistema que es determina en funció de la compatibilitat per integrar amb altres dominis gestionats per versions anteriors. 
  En el nostre cas, per assegurar la compatibilitat amb Windows 2008 R2 cal seleccionar l'opció "**_Nivell de funcionalitat Windows 2012 R2_**" i prem **_Següent_**.

4. Després d'examinar la configuració DNS i, en el cas de no estar instal·lat aquest servei, has de deixar marcada la casella **_Servidor DNS_** i prémer Següent doncs **cal tenir instal·lat el servei de resolució de noms per al correcte funcionament del Directori Actiu**.

5. L'assistent ens demana ara una **contrasenya **per poder administrar el **Directori Actiu**. En general, encara que poden ser diferents, sol ser convenient posar la mateixa contrasenya que l'administrador de l'equip. 
  Introdueix doncs la contrasenya de l'administrador i prem **_Següent_**.

8. A continuació s'ha d'indicar la localització dels arxius bàsics que utilitzarà el Directori Actiu: la carpeta per a base de dades, la carpeta d'arxius de registre i la carpeta SYSVOL que conté els arxius públics del domini que han de ser compartits.

9. Se'ns informa a continuació mitjançant un **resum**, de tota les configuracions que hem seleccionat. En aquest punt podríem Exportar Configuració... és a dir, guardar aquestes seleccions en un arxiu per utilitzar-les en futures instal·lacions automàtiques.

10. En prémer **_Següent _**comença la instal·lació de **Directori Actiu** i el procés de **promoció de l'equip a Controlador de Domini**, que poden portar més o menys temps en funció de l'entorn i de les opcions seleccionades. 

11. Finalment apareix una pantalla informativa un cop acabada la instal·lació. Prémer **_Finalitza _**i després **Reiniciar l'equip** perquè el Directori Actiu s’iniciï i estigui operatiu.

12. Si tot ha funcionat correctament, el nostre equip ja està convertit en un controlador de domini del Directori Actiu per gestionar de forma centralitzada els recursos de la xarxa.

## Unir equips al domini

1. Configureu una **xarxa interna** en VirtualBox amb un servidor Windows 2012 com a controlador de domini i un ordinador client Windows 10.

2. Configureu la tarjeta de xarxa de les màquines virtuals en mode de **Xarxa interna**.

3. Assigneu IP Estàtica a la màquina servidor (per exemple 192.168.0.10) i a la màquina client (192.168.0.20). El controlador de domini també dona servei DNS al client per tant, al client, **cal posar com a servidor DNS principal la IP del servidor de domini**.

4. Fes pings per a verificar que el client pot comunicar-se amb el servidor.

5. Entreu a la màquina client i **afegiu-la al domini**, canviant el mode de grup de treball al mode de domini. Necessitareu les credencials d'administrador del domini. 

6. Ara entreu a la màquina client i veureu que podeu entrar al domini mitjançant les credencials de l'administrador. 

7. **Entra al servidor i busca el nou equip** a **_Eines administratives > Usuaris i equips de l’Active Directory_**.
