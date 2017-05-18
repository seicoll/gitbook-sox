<!-- notoc -->

# Activitat 2. Gestió d’arxius, directoris, usuaris i grups.

## PART 1. TERMINALS, SHELLS I COMANDES BÀSIQUES

### 1. Terminals

  a. Obre un emulador de terminal en mode gràfic, executa la comanda “who” i posa aquí una captura amb el resultat.

  b. De quants terminals virtuals en mode text es disposa en Ubuntu?

  c.  Com es pot accedir a cada terminal?

  d. Accedeix al terminal 5, inicia sessió amb el teu usuari, executa la comanda “who”, escriu aquí el resultat i tanca la sessió.

  e. Com es pot tornar a l'entorn gràfic?

  f. Com es pot diferenciar a través de quin tipus de terminal ha accedit un usuari?

### 3. Shells

a. Escriu les comandes per fer les següents accions i el resultat:

    * Llista les últimes 10 comandes que has utilitzat

    * Repeteix la comanda nº 12 que vas executar

    * Veure per pantalla les 20 últimes ordres efectuades al meu shell i al mateix temps guardar el resultat en un fitxer amb el nom últimes.txt.

b. En quin arxiu es troba l'històric del bash

c.  Per a què serveix la comanda "history -c"

## PART 2. ARXIUS I DIRECTORIS

1. Quina comanda permet conèixer el directori de treball actual?

2. Vés a la teva carpeta Documents del teu usuari i crea una carpeta anomenada SOX.

3. Crea els arxius Interficies.txt, Arxius.sh, Xarxa.txt i Inventari.sh.

4. Llista els arxius mostrant detalladament la informació disponible.

5. Edita l'arxiu Inventari.sh afegint una comanda per llistar els arxius amb detall.

6. Guarda l'arxiu, surt de l'editor i mostra el contingut d'aquest arxiu.

7. Torna a la consola, executa l'arxiu Inventari.sh i copia aquí el resultat. És necessari canviar els permisos del fitxer perquè pugui ser executat.

8. Fes que l'arxiu Inventari.sh sigui només de lectura.

9. Amaga posant a ocults tots els arxius “sh”

10. Executa l'arxiu Inventari.sh i copia aquí el resultat. Apareixen ara els arxius ocults?

11. Canvia el nom de l'arxiu Xarxa.txt per Configuració de Xarxa.txt i després esborra'l

12. Esborra la carpeta SOX.

13. Quin és l’equivalent de chmod u+rwx “arxiu”;chmod go-rwx “arxiu”en notació octal ?

14. Com es pot, amb només una comanda, copiar els arxius ocults del meu directori de login al directori actual.

15. Busca tots els arxius del sistema amb la extensió .sh

16. Busca la paraula root en el fitxer d’usuaris (`/etc/passwd`)

## PART 3. USUARIS I GRUPS

1. Posa o canvia la contrasenya de l'administrador (root).

2. Amb quina comanda es pot obtenir la informació de l’usuari actual (nom, UID, GID, ruta de login, etc.)? I d’un altre usuari?

3. Gestió de grups i usuaris:

  a. Crea els usuaris “**alumne1**”, “**alumne2**”. Cada usuari ha de tenir el seu director /home/nom_usuari.
Comprova que s’han creat al fitxer d’usuaris /etc/passwd.

  b. Crea un grup anomenat “**alumnes**” i comprova que s’ha creat en el fitxer /etc/group.

  c. Fes que tots els usuaris que has creat anteriorment formin part d'aquest grup “alumnes”.

  d. Crea un usuari “alumne3” i afegeix-lo al grup “alumnes” amb una única comanda.

4. Com ho faries perquè a les carpetes de /home/alumne1, /home/alumne2 i /home/alumne3 només hi poguessin accedir els alumnes que pertanyin al grup “alumnes”?

5. Crea un usuari “**professor**”.

6. Crea un directori a **/home/compartit** i assigna permisos per a que l’usuari professor tingui permisos d’escriptura, lectura i execució, que el grup alumnes només tingui permisos lectura i la resta no tingui cap permís.

7. En quins arxius es troben:

  a. Els usuaris.
  b. Les contrasenyes encriptades dels usuaris.
  c. Els grups i els usuaris que pertanyen a cada grup.
  d. Els usuaris i grups que poden fer “sudo”.


