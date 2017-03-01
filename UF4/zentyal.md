# Zentyal com a controlador de domini

## Introducció

**Zentyal** integra **Samba4** com a servei de directori, implementant la funcionalitat d'un controlador de domini Active Directory de Windows, a més de compartició de fitxers i impressores.

**Zentyal** implementa una sèrie de serveis, sent els més importants directori **LDAP**, el **servidor DNS** i l'autenticació distribuïda mitjançant **Kerberos**.

Per la compartició d'arxius, **Zentyal** utilitza el protocol **SMB/CIFS** per mantenir la compatibilitat amb els clients Microsoft. 

## Configuració de la xarxa

## Creació d'un domini amb Zentyal

Un cop tenim instal·lat Zentyal, podem crear un nou domini anant a **_Sistema > General_** i canvieu el nom del domini a **_ELTEUNOM.local_** (on _ELTEUNOM_ s'ha de substituir pel teu nom). 

Anem a **_Configuració de l'estat dels mòduls_** i comprovem que estan actius els mòduls:
* DNS
* NTP
* Domain Controller and File Sharing

Un cop haguem activat **_Usuaris, Equips i Fitxers_** podem proveir carpetes compartides, unir clients Windows al domini, configurar i enllaçar les polítiques GPO i acceptar connexions dels nous controladors de domini addicionals, tant Windows Server® com Zentyal.

Tot seguit anem al mòdul DNS i a Domains cliquem dins de ” Domain Ip Adress”. A dins hi tindrm les ip’s de les dues interfícies. Només hi ha d’haver la de la xarxa interna. Guardem abans de sortir.

Una de les primeres operacions que necessites fer en el teu domini és crear un usuari al directori i unir-lo al grup de **_Domain Admins_**. A l'unir-lo, l'usuari tindrà tots els permisos efectius sobre el domini.

* **_Users and computers > Manage_**
* Creem un usuari administrador
* Afegim l'usuari al grup **_Domain Admins_**.

![](/assets/zentyal-users.png)

## Unir un client Windows al domini Zentyal

Es fa de la mateixa forma que per unir-lo a un domini Windows:

1. Si el client està unit a un domini, primer cal desconnectar-lo del domini i reiniciar.

2. A la configuració de xarxa, canviar els servidors DNS posant com a **DNS principal** la IP del servidor de domini.

  ![](/assets/samba4_unir_client1.jpg)

3. Connectar-lo al nou domini: _**Panel de control > Sistema > Cambiar configuración > Dominio**_

  Caldrà posar el nom del domini (_ELTEUNOM_ o _elteunom.local_) i quan demani un usuari, s'ha de posar l'usuari **_Domain Admin_** que hem creat prèviament i és l'usuari administrador del domini.

  ![](/assets/samba4_unir_client2.jpg)

4. Reiniciem la màquina i ja tenim l’equip afegit al domini.
  El nostre client Windows apareixerà a l'arbre d'LDAP sota la Unitat Organitzativa **_Computers_**.

## Perfils mòbils

Un perfil és un entorn personalitzat especialment per a un usuari. El perfil conté la configuració de l’escriptori i dels programes de l’usuari. Cada usuari té un perfil, tant si l’administrador ho configura com si no, perquè el perfil es crea automàticament per a cada usuari quan s’inicia sessió en un equip.

Perfils mòbils: Quan l’usuari s’identifica en qualsevol dels equips de la xarxa, el perfil s’escaneja automàticament.

Creació de perfils mòbils a Zentyal. **_Domain> Settings_** i Marcar “enable roaming profil·les”

## Creació carpetes compartides

Des de **_Filesharing_** podeu crear tots els recursos compartits que necessiteu
tal com ho podíeu fer amb el Samba.

Per accedir-hi amb el client haureu d’anar **_Computer > Network_**

## Documentació i recursos

[Zentyal Documentació](https://wiki.zentyal.org/wiki/Es/4.1/Usuarios,_Equipos_y_Comparticion_de_ficheros)