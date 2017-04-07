<!-- notoc -->

# Activitat 2. Administració i supervisió de Windows Server 2012

![](/assets/WindowsServer2012-2.png)

## Activitat

####1. Administrador de tasques

  1.1. Quins operacions/tasques ens permet fer l’administrador de tasques?
   
  1.2. Indica les 4 formes d’accedir a la consola d'administració de tasques. 
  
  1.3. Enumera i resumeix la utilitat de les 5 pestanyes que formen l'administrador de tasques. Posa una captura de pantalla de cada una d’aquestes pestanyes del Windows Server 2012 R2. 
  
  1.4. Obre la línia de comandes (cmd) des de l’administrador de tasques. 
  
  1.5. Que és el PID d’un procés? 

####2. Administrador de serveis

  2.1. Què significa el “tipus d'inici” d'un servei? 
  
  2.2. Per a què serveix la pestanya de Recuperació que trobem dins les propietats d’un servei? 
  
  2.3. Modifica el servei “Client dhcp” per a que tingui un inici manual. Canvia la teva IP a DHCP (Obtenir IP automàticament) i reinicia el sistema. Què hauria d'anar malament? Per què? Torna-ho a deixar com estava. 

#### 3. Usuaris 

3.1. Com podem desconnectar a un usuari que s'ha connectat remotament al nostre servidor? 

3.2. Desconnecta el teu propi usuari. 

3.3. Obre un altra sessió de Windows 2012 amb un altre nom d'usuari (recorda que tindrà que pertànyer al grup d'administradors per poder obrir sessió local en el servidor). Ara canvia d'usuari i torna a la sessió inicial. Comprova en l'administrador de tasques quins usuaris estan connectats (enganxa aquí una captura de la finestra). 

3.4. Envia un missatge a l'altre usuari connectat. Canvia a la seva sessió i comprova que ha arribat (enganxa aquí una captura de la finestra del missatge). Ja pots tancar aquesta sessió. 

#### 4. Registre d’esdeveniments 

4.1. Ara torna a entrar a la sessió de l'administrador però primer amb una contrasenya incorrecta. Això genera errors d'auditoria que queda registrat. Una vegada has posat la contrasenya correcta i has entrat com administrador engega el visor d'esdeveniments ("visor de eventos") i indica el que trobis a la secció de _**Registros de windows > seguridad**_ relacionat amb aquests accessos no autoritzats. 

4.2. Fes una captura de pantalla amb l’error que trobis al registre. Quina informació et dóna? 

#### 5. Actualitzacions 

  5.1. Actualitza el sistema operatiu. Quin és l'últim "service  pack" disponible? 
  
  5.2. Programa perquè es descarreguin les actualitzacions crítiques però demani si les volem insta·lar. 
  
  5.3. Configureu les actualitzacions crítiques perquè es realitzin sempre a una hora determinada.  

6. Executa l’eina **_Administrador del servidor_**. Quins rols i característiques es poden configurar?  

7. Mostra, des del Windows Server, el processador, la RAM i l’espai de disc que té el sistema. 

8. (**_AMPLIACIÓ_**) Busqueu informació sobre com instal·lar la funció Terminal Server i com podem connectar-nos des d'una màquina remota. Crea un usuari amb el teu nom i cognom (nomcognom). Configura aquest usuari perquè es pugui connectar al servidor des del Windows client mitjançant el terminal server.