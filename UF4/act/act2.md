<!-- notoc -->

# Activitat 2. Unir un client Linux a un domini Windows

En aquesta activitat configurarem un client Linux per tal que es pugui unir a un domini gestionat amb l’Active Directory del Windows Server. Per fer-ho utilitzarem un programa com **PBIS Open** que s’encarrega de realitzar la major part de la configuració i ens facilita molt la feina.

## Requisits

Treballarem amb dues màquines virtuals. Una amb **Windows Server** que farà de servidor i amb un domini creat anomenat **_bosccoma.local_**. 

I l’altra màquina amb **Ubuntu Desktop** que farà de client.

Configurar-les perquè estiguin connectades a una **xarxa NAT** anomenada SOX.

## Activitat 

**Configuració del client**

Configura un client Linux (Ubuntu Desktop) i connecta'l al domini del teu servidor Windows Server.

**Nota**: Si et surt un error al iniciar la interfície gràfica sobre la llibreria **libglade** executa:
 
```
sudo apt-get install libglade2-0
```

Configura **PBIS Open** de forma que els usuaris utilitzin el shell /bin/bash i que el seu directori personal sigui `/home/BOSCCOMA/usuari`.

Executa la comanda `getent passwd | tail -n 10` i enganxa una captura de pantalla:

Executa la comanda `getent group | tail -n 10` i enganxa una captura de pantalla:

Comprova que pots validar usuaris del domini, tant des del login gràfic ([Configuració del login gràfic](https://seicoll.gitbooks.io/sox/content/UF2/uf2-auteticacio-ldap.html#configurar-el-login-dubuntu)) com per consola (`sudo login usuariDomini@bosccoma.local`).

Un cop hagis accedit amb un usuari del domini, executa les comandes pwd i ls -l, i enganxa una captura de pantalla.
Captura de pantalla.

## Ampliació

Crea en el teu domini l'usuari **ADelteunom **(**_elteunom _**ha de ser el teu nom).
Desconnecta el client Linux del teu domini, posa'l en mode Bridged (Adaptador pont), configura'l per connectar-lo al domini d'un company, uneix-lo utilitzant la comanda **domainjoin-cli** i fes una captura de pantalla del resultat d'aquesta comanda.

Comprova que en la teva màquina es pot validar l'usuari **_ADnomdelcompany _**del domini del teu company (**_nomdelcompany _**és el nom del teu company). Un cop hagis accedit amb aquest usuari, executa les comandes pwd i ls -l, i enganxa una captura.

Desconnecta el client Linux del domini del teu company, posa'l en mode Xarxa NAT - SOX, configura'l per connectar-lo al teu domini i torna'l a connectar. Assegura't que funciona correctament validant usuaris del teu domini.