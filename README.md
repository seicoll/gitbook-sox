
#Introducció

El llibre de **_Sistemes Operatius en Xarxa_** és un material didàctic enfocat als alumnes del _CFGM de Sistemes Microinformàtics i Xarxes_. En ell es desenvolupen els continguts del mòdul professional de _Sistemes Operatius en Xarxa_ i s’hi proposen activitats i qüestionaris d’autoavaluació.

Aquest llibre és un material viu que evoluciona dia a dia i pot trobar-se la última versió a  https://www.gitbook.com/book/seicoll/sox.

El llibre no hauria estat possible sense el meus alumnes que m’han anat comunicant, al llarg del curs, les errades que anaven trobant i els paràgrafs que no havien quedar redactats de forma clara. I així, el llibre ha anat millorant dia a dia.

I per suposat, també agrair a la meva dona i els meus fills que m’han recolzat i m’han permès obtenir el temps necessari per dedicar a aquest projecte.

![](/assets/Llibre3D.jpg)

<!--
# Continguts

### UF1. Sistemes operatius propietaris en xarxa
  * [Introducció als sistemes operatius en xarxa](UF1/uf1-introduccio.md)
    * [Windows Server](UF1/uf1-windowsserver.md)
    * [Instal·lació Windows Server](UF1/uf1-instalacio-windowsserver.md)
  * [Supervisió en Windows Server](UF1/uf1-supervisio.md)
  * [Gestió de dominis. Active Directory](UF1/gestio-de-dominis.-active-directory.md)
    * [Introducció als dominis](UF1/uf1-introduccio-dominis.md)
    * [Relacions de confiança](UF1/relacions-de-confianca.md)
    * [Instal·lació d'un controlador de domini en Active Directory](UF1/instalacio-AD.md)
    * [Usuaris, grups i unitats organitzatives](UF1/usuaris-grups-i-unitats-organitzatives.md)
    * [Perfils d'usuaris](UF1/perfils-usuari.md)
    * [Directives de grup](UF1/directives-de-grup.md)
  * [Activitats](UF1/uf1-activitats.md)
    * [Activitat 1. Instal·lació Windows Server 2012](UF1/act/act1-instalacio.md)
    * [Activitat 2. Administració i supervisió de Windows Server 2012](UF1/act/act2-supervisio.md)
    * [Activitat 3. Instal·lació d'Active Directory](UF1/act/act3-instalacio-AD.md)
    * [Activitat 4. Administració d'Active Directory](UF1/act/act4-administracio-AD.md)
    * [Activitat 5. Polítiques de grup d'Active Directory](UF1/act/act5-GPO-AD.md)
    * [Qüestionari](UF1/act/uf1-questionari.md)


### UF2. Sistemes operatius lliures en xarxa
  * [Gestió de dominis](UF2/uf2-gestio-dominis.md)
    * [Introducció als dominis en Linux](UF2/uf2-dominis-linux.md)
    * [Instal·lació d'un controlador de domini LDAP](UF2/uf2-LDAP.md)
    * [Gestionar LDAP amb interfície gràfica](UF2/uf2-LDAP-gestio-grafica.md)
    * [Autenticació LDAP](UF2/uf2-auteticacio-ldap.md)
  * [Activitats](UF2/uf2-activitats.md)
    * [Activitat 1. Instal·lació Ubuntu Server](UF2/act/act1.md)
    * [Activitat 2. Gestió d’arxius, directoris, usuaris i grups](UF2/act/act2.md)
    * [Activitat 3. Actualització i instal·lació de programari](UF2/act/act3.md)
    * [Activitat 4. Monitorització i automatització de tasques](UF2/act/act4.md)
    * [Activitat 5: Instal·lació d’un controlador de domini LDAP i configuració client LDAP](UF2/act/act5.md)
    * [Activitat 6: Administració de OpenLDAP](UF2/act/act6.md)
    * [Qüestionari](UF2/act/uf2-questionari.md)

### [UF3. Compartició de recursos i seguretat](UF3.md)
  * [Introducció a la compartició de recursos i seguretat](UF3/uf3-introduccio.md)
  * [Compartir recursos en xarxa i seguretat en sistemes de propietat](UF3/uf3-compartir-recursos-windows.md)
    * [Compartir arxius i carpetes en Windows](UF3/uf3-compartir-arxius-windows.md)
    * [Compartir impressores en Windows](UF3/uf3-compartir-impressores-windows.md)
  * [Compartir recursos en xarxa i seguretat en sistemes de lliures](UF3/uf3-compartir-recursos-linux.md)
    * [Compartir arxius i carpetes amb NFS](UF3/uf3-compartir-arxius-linux-nfs.md)
    * [Compartir impressores amb CUPS](UF3/uf3-compartir-impressores-cups.md)
  * [Activitats](UF3/uf3-activitats.md)
    * [Activitat 1. Compartir recursos i seguretat en Windows Server](UF3/act/act1.md)
    * [Activitat 2. Compartir impressores en Windows Server](UF3/act/act2.md)
    * [Activitat 3. Compartir carpetes en GNU/Linux amb NFS](UF3/act/act3.md)
    * [Activitat 4. Compartir impressores en GNU/Linux amb CUPS](UF3/act/act4.md)
    * [Qüestionari](UF3/act/uf3-questionari.md)

### [UF4. Integració de sistemes operatius](UF4/UF4.md)
  * [Compartició de recursos en escenaris heterogenis](UF4/uf4-introduccio.md)
    * [Compartir arxius i carpetes amb SAMBA](UF3/uf3-compartir-arxius-samba.md)
  * [Gestió de dominis en escenaris heterogenis](UF4/gestio-dominis.md)
    * [Samba 4 com a controlador de domini (DC)](UF4/controlador-domini-samba.md)
    * [Administrar el directori actiu de Samba 4](UF4/administrar-sambaAD.md)
    * [Perfils mòbils en un domini Samba AD](UF4/perfils-mobils-sambaAD.md)
    * [Zentyal com a controlador de domini](UF4/zentyal.md)
  * [Activitats](UF4/uf4-activitats.md)
    * [Activitat 1. Compartir recursos amb Samba](UF4/act/act1.md)
    * [Activitat 2. Unir un client Linux a un domini Windows](UF4/act/act2.md)
    * [Activitat 3. Samba 4 com a controlador primari de domini (AD DC)](UF4/act/act3.md)
    * [Activitat 4. Zentyal com a controlador primari de domini](UF4/act/act4.md)
    * [Qüestionari](UF4/act/uf4-questionari.md)


-->















