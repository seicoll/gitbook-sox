# Zentyal com a controlador de domini

## Introducció

**Zentyal** integra **Samba4** com a servei de directori, implementant la funcionalitat d'un controlador de domini Active Directory de Windows, a més de compartició de fitxers i impressores.

**Zentyal** implementa una sèrie de serveis, sent els més importants directori **LDAP**, el **servidor DNS** i l'autenticació distribuïda mitjançant **Kerberos**.

Per la compartició d'arxius, **Zentyal** utilitza el protocol **SMB/CIFS** per mantenir la compatibilitat amb els clients Microsoft.

## Configuració de la xarxa

## Creació d'un domini amb Zentyal

Un cop tenim instal·lat Zentyal, podem crear un nou domini anant a _**Sistema &gt; General**_ i canvieu el nom del domini a _**ELTEUNOM.local**_ \(on _ELTEUNOM_ s'ha de substituir pel teu nom\).

Anem a _**Configuració de l'estat dels mòduls**_ i comprovem que estan actius els mòduls:

* DNS
* NTP
* Domain Controller and File Sharing

Un cop haguem activat _**Usuaris, Equips i Fitxers**_ podem proveir carpetes compartides, unir clients Windows al domini, configurar i enllaçar les polítiques GPO i acceptar connexions dels nous controladors de domini addicionals, tant Windows Server® com Zentyal.

Tot seguit anem al mòdul DNS i a Domains cliquem dins de ” Domain Ip Adress”. A dins hi tindrm les ip’s de les dues interfícies. Només hi ha d’haver la de la xarxa interna. Guardem abans de sortir.

Una de les primeres operacions que necessites fer en el teu domini és crear un usuari al directori i unir-lo al grup de _**Domain Admins**_. A l'unir-lo, l'usuari tindrà tots els permisos efectius sobre el domini.

* _**Users and computers &gt; Manage**_
* Creem un usuari administrador
* Afegim l'usuari al grup _**Domain Admins**_.

![](../../.gitbook/assets/zentyal-users.png)

## Unir un client Windows al domini Zentyal

Es fa de la mateixa forma que per unir-lo a un domini Windows:

1. Si el client està unit a un domini, primer cal desconnectar-lo del domini i reiniciar.
2. A la configuració de xarxa, canviar els servidors DNS posant com a **DNS principal** la IP del servidor de domini.

   ![](../../.gitbook/assets/samba4_unir_client1.jpg)

3. Connectar-lo al nou domini: _**Panel de control &gt; Sistema &gt; Cambiar configuración &gt; Dominio**_

   Caldrà posar el nom del domini \(_ELTEUNOM_ o _elteunom.local_\) i quan demani un usuari, s'ha de posar l'usuari _**Domain Admin**_ que hem creat prèviament i és l'usuari administrador del domini.

   ![](../../.gitbook/assets/samba4_unir_client2.jpg)

4. Reiniciem la màquina i ja tenim l’equip afegit al domini. El nostre client Windows apareixerà a l'arbre d'LDAP sota la Unitat Organitzativa _**Computers**_.

## Perfils mòbils

Un perfil és un entorn personalitzat especialment per a un usuari. El perfil conté la configuració de l’escriptori i dels programes de l’usuari. Cada usuari té un perfil, tant si l’administrador ho configura com si no, perquè el perfil es crea automàticament per a cada usuari quan s’inicia sessió en un equip.

Podem configurar els **perfils mòbils** per tal que els usuaris tinguin els mateix escriptori i accés als seus documents i configuracions des de qualsevol equip on es connectin. Trobem l’opció de configuració de perfils mòbils a  _**Domain &gt; Settings &gt; Marcar “enable roaming profiles”**_ .

El servidor Zentyal guarda els perfils mòbils a /home/samba/profiles

## Creació carpetes compartides

Des de _**Compartició de fitxers \[File Sharing\]**_ podeu crear tots els recursos compartits que necessiteu tal com ho podíeu fer amb el Samba.

## Documentació i recursos

[Zentyal Documentació](https://wiki.zentyal.org/wiki/Es/4.1/Usuarios,_Equipos_y_Comparticion_de_ficheros)

