# Perfils d'usuari

## Què és el perfil d'un usuari?

> El **perfil d'un usuari** és un conjunt de dades que serveixen per personalitzar l'entorn de treball d'aquest usuari.

Aquestes dades inclouen:
* En quina carpeta es guarda la configuració que l'usuari fa del seu entorn de treball (fons de l'escriptori, mida de les icones, la lletra del sistema, configuració del teclat i ratoli...).
* En quina carpeta es guardaran els seus arxius personals. Només ell hi podrà accedir.
* Quin script s'executarà cada cop que l'usuari iniciï sessió. Pot servir entre altres coses per què l'usuari pugui accedir a impressores i carpetes compartides

Si es fa què la carpeta del seu perfil es guardi en un servidor, l'usuari tindrà la seva configuració en qualsevol màquina del domini, i en aquest cas es diu que té un **perfil mòbil**.

Si no es configura la carpeta de perfil, en cada màquina se li crearà un **perfil local**.

## Tipus de perfils

**Perfil local**: quan s'accedeix amb un usuari local, el perfil d'usuari què s'utilitzarà és el què hi a la mateixa màquina. Si encara no té cap perfil guardat, se li crea un per defecte. Quan l'usuari tanca sessió, es guarden els canvis què ha fet (el seu perfil) en la mateixa màquina

**Perfil temporal**: es crea un perfil temporal quan no es pot carregar el perfil. Els canvis que faci l'usuari s'esborren quan es tanca la sessió

**Perfils de xarxa**: quan s'accedeix amb un usuari del domini, es carrega el perfil guardat en el servidor. D'aquesta forma, l'usuari tindrà la seva configuració en qualsevol ordinador. Els canvis què faci (si és un perfil mòbil) també es guardaran al servidor quan tanqui la sessió
* **Perfil Mòbil**: l'usuari pot fer canvis en el seu perfil
* **Perfil Obligatori**: l'usuari pot fer canvis però s'esborren al tancar la sessió
* **Perfil Súper-obligatori**: si no es pot carregar el perfil, no es pot iniciar sessió

## Configuració de perfils d'usuaris

