# Compartir recursos i seguretat en Windows

## Activar unitats compartides

Per activar les unitats compartides has de fer el següent:

1. Fer clic a **_Inici > Xarxa_** per accedir al centre de Xarxes i recursos compartits.
2. Activar l’**_Ús compartit d’arxius i impressores_**.

![](/assets/win-activar-us-compartit.PNG)

* L’opció **_Ús compartit d’arxius i impressores_** controla l’accés als recursos compartits per mitjà de la xarxa i a les impressores connectades a l’equip.

* L’opció **_Ús compartit de la carpeta públic_** controla l’accés a les carpetes públiques de l’equip.  

## Utilització d’unitats compartides

Per compartir recursos de l’equip podem fer servir:

1. L’explorador de Windows i fent botó dret del ratolí > **_Compartir amb_**

2. L’administració d’equips [_Computer Management_]

  IMATGE

  Des de l’administració d’equips veiem això:
    
  * **Nom del recurs:** és el nom del recurs compartit.
  * **Ruta de la carpeta:** és la ruta sencera en el sistema local.
  * **Tipus:** és el tipus d’ordinador que pot utilitzar el recurs.
  * **Num. de connexions de client:** és la quantitat de clients que estan accedint al recurs en aquell precís moment.
  * **Descripció:** és la descripció del recurs.

3. El **Server Manager**, dins **_File and Storage Services > Shares_**

  IMATGE

  * **Nom del recurs compartit:** és el nom del recurs compartit.
  * **Ruta local:** és la ruta completa de la carpeta en el sistema local.
  * **Protocol:** és el nom del protocol utilitzat per compartir la carpeta.
  * **Espai lliure:** és la quantitat d’espai lliure en el disc si no hi ha quotes establertes.
  * **Quota:** és el resum de l’estat de les quotes de l’administrador de recursos sobre la carpeta compartida.
  
4. Executant la a comanda 

  ```net share```

  permet veure les unitats que tenim compartides en l’equip actual.
  
  IMATGE
  
  
## Crear carpetes compatides

## Permisos de carpetes compartides

## Carpetes compartides ocultes

* Si es vol compartir un recurs però que no sigui visible (només es podrà connectar qui conegui la ruta a aquest recurs) només cal afegir un $ darrera del nom del recurs.
  * Per exemple: C$
  
* Amb **\\\ip_equip** o **\\\nom_equip** es pot veure els recursos compartits visibles.

* Es pot accedir a un recurs compartit ocult si es conneix tota la ruta.
  * Per exemple: \\\192.168.0.1\C$

* Si l'**usuari** autentificat a la màquina client està **reconegut** per la màquina servidor i té accés al recurs, aquest es podrà connectar.

* Sinó es possible que demani un usuari i contrasenya que sigui reconegut pel servidor.

* Si volem que es pugui connectar qualsevol usuari caldrà donar permisos a l'usuari convidat i, si cal, habilitar aquest usuari.

## Conèixer els permisos d’un rescurs compartit

Per **conèixer els permisos** que té un recurs, es poden seguir els passos que es mostren a continuació:

1. Connecteu-vos al recurs dins de l’administració d’equips.
2. Expandiu Eines de sistema, Carpetes compartides i cliqueu a Recursos compartits.
3. Cliqueu amb el botó dret al recurs que vulgueu examinar i cliqueu a Propietats.
4. La fitxa Permisos dels recursos compartits us mostrarà l’usuari o grups d’usuaris que tenen accés al recurs i com és aquest accés. Aquesta fitxa permet modificar els permisos existents.

IMATGE

## Connexió a unitats de xarxa

* Per connectar-se a una unitat de xarxa i accedir als recursos que conté, només cal executar l’ordre: 

  ```net use```

* Per exemple, si es vol accedir a un recurs amb l'etiqueta Imatges que s'emmagatzema en una màquina anomenada Multimedia i la lletra de la unitat és la d, cal escriure el següent:

  ```net use d: \\Multimedia\Imatges```




