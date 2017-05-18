<!-- notoc -->

# Activitat 4. Monitorització i automatització de tasques.

## PART 1. MONITORITZACIÓ

1. Processos

  a. Quants processos té en marxa l’Ubuntu Server?

  b. Quins són els tres que consumeixen més CPU?

  c. Quins són els tres que consumeixen més memòria?

2. Quina CPU té 	la teva màquina virtual? Indica amb quina comanda ho has trobat.

3. En un **Ubuntu Desktop**, instal·la el programa **ntop**. Executa algunes accions que facin servir la xarxa (ping, actualitzacions...). 
Fes una captura de pantalla on es vegi alguna gràfica o resultats de la utilització de la xarxa.

4. En un **Ubuntu Server**, instal·la el programa **iftop**. Executa algunes accions que facin servir la xarxa (ping, actualitzacions...). 
Fes una captura de pantalla on es vegi els resultats de la utilització de la xarxa.

## PART 2. AUTOMATITZAR TASQUES

1. Indica cada quan s'executaran les següents accions programades al crontab:

  a. \* \* \* \* 7
  
  b. \* \* 1 \* \*

  c. 0 \* \* \* \*

  d. \* 7 \* \* 1-5

  e. 0 0 1 1 \*

  f. 0 \* 15 \* \*

  g. 45 22 1 12 1

  h. 0-15 8 \* \* 6,7

  i. 0 9-21/6 \*/5 1-3 \*

  j. 45-59/3 23 * 1,4,9-12 *

  k. 17-22 \* \* 1-4,7

  l. 10 13,21 1,10-20 6-12/4 3

2. Com programaries el **crontab** per executar accions amb les següents periodicitats:

  a. Cada primer de mes, a les 8:00

  b. Cada dia a les 21:15

  c. Cada 10 minuts

  d. Els dissabtes i diumenges, a les 11:00

  e. Els dilluns, de les 6:00 a les 6:10, cada 2 minuts

  f. El primer dia de cada trimestre (a les 0:00)

  g. Els mesos de juliol i agost, cada 5 minuts, de les 10 a les 12 de la nit

  h. El dia 15 de cada mes, cada hora, des de les 8:00 a les 15:00, però només si és dia entre setmana (de dilluns a divendres)

  i. Els dies imparells de cada mes, entre el Gener i el Juny

  j. Del 10 al 20 de cada mes, a les 15:00, però només dilluns, dimecres i divendres

3. Fes un **script** per automatitzar les còpies de seguretat:

  a. Crea l'script **_backup.sh_**. 
La seva funció ha de ser fer una còpia de seguretat comprimida del directori `/home` dins de la carpeta `/backups`. 
Només el root ha de poder escriure a la carpeta /backups i executar aquest script.

  Enganxa una captura de pantalla d'aquest script i dels permisos que li has donat.

  b. Configura el **cron** del root de forma que l'script backup.sh 	s'executi cada dia, de dilluns a divendres, entre els mesos de setembre a maig, a les 20:25.
Comprova que l'script i la configuració del cron funcionen adequadament.

  Executa la comanda `sudo crontab -l` i enganxa una captura.

c. **Ampliació**: Fes que l’script també escrigui en un fitxer backups.log la data, hora i si la copia ha anat bé.	