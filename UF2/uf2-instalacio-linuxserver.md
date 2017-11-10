# Instal·lació Ubuntu Server

## Planificació de la instal·lació

### Comprovar els requeriments de maquinari

S'ha de comprovar a la web oficial, tant del sistema operatiu com de les aplicacions què s'han d'instal·lar, quins són els requeriments de maquinari.

### Preparar el programari a instal·lar i les dades a configurar

S'ha de tenir preparat tot el programari i les dades necessàries: CDs, controladors, claus d'activació...

### Crear la màquina virtual

S'ha de crear una màquina virtual amb les característiques recomanades per instal·lar **_Ubuntu Server 64 bits_**:

* El nom de la màquina pot ser **_SOX Ubuntu Server_**.
* Es recomana que l'espai del disc es reservi de forma dinàmica.
* Es pot posar més d'un processador.
* Connecta la MV a la [** xarxa NAT SOX**](http://moodlecf.sapalomera.cat/apunts/smx/sox/uf0/A012-VBoxPlus.html#config_nat_network).

Després de la instal·lació, la memòria RAM es pot reduir fins a 512 MB.

### Paràmetres bàsics de configuració

* Triar l'idioma i altres dades regionals (país, teclat...).
* **Nom de la  màquina**: **_usxxx_** (**_xxx_** són les teves inicials en minúscules).
* **Nom de l'usuari** (es pot posar nom i cognoms).
* **Nom del compte d'usuari** (una sola paraula, lletres minúscules o números...).
* **Contrasenya** (preferiblement que segueixi els criteris de seguretat).
* No cal encriptar la carpeta personal.
* Seleccionar la zona horària.


### Particionat del disc
### Planificar el disc

* Primer s'ha de seleccionar el particionat manual, triar el disc i crear la taula de particions.
  * En l'espai lliure, crear una partició nova de 6 GB.
  * Crear-la com a partició primària, al principi del disc i amb el format ext4.
  * El punt de muntatge ha de ser l'arrel del sistema (/).
  * No cal afegir cap opció addicional de muntatge.
Repetir els passos anteriors per crear una partició primària de 2 GB per la carpeta d'usuaris (/home).
Finalment, crear una altra partició primària amb la resta de l'espai per a la swap (àrea d'intercanvi).
Abans de confirmar, comprovar les particions creades:

### Planificar el disc

Cal planificar la utilització del disc, decidir les particions necessàries i el sistema de fitxers a utilitzar.

