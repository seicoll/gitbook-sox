# Automatització de tasques

## Introducció

Moltes de les tasques d'administració d'un servidor s'han de **portar a terme de manera periòdica**.

**Per exemple**: 
  * fer còpies de seguretat dels teus arxius un cop al dia
  * actualitzar el sistema
  * canviar el fons de pantalla cada 30 minuts.

És necessari que el sistema operatiu ens proporcioni alguna eina per a poder **configurar totes aquestes tasques de forma automàtica i periòdica**.

El **dimoni [_daemon_]** anomenat **_crond_** és el que s'encarrega de gestionar tot el sistema d'execucions periòdiques.

## Servei cron

El Linux té un servei anomenat **_cron_** que funciona despertant-se cada minut i mirant un fitxer on hi ha les tasques programades.

Podem saber que el procés s'està executant amb la comanda: 

`ps aux | grep cron`

En el fitxer `/etc/crontab` conté la informació de les tasques programades.

Cada usuari té el seu propi fitxer **_crontab_**.

## Programar tasques periòdiques

La comanda `crontab` permet **programar tasques periòdiques** i especificar el moment d'execució.

> Es pot configurar el cron per cada usuari, tot i què normalment només es fa pel **root**.

* Per **veure les tasques programades** de l'usuari actual.

  `sudo crontab -l`

* Per **editar el fitxer de tasques** de l'usuari actual.

  `sudo crontab -e`
  
* Per **editar el fitxer de tasques** de l'usuari _root_.

  `sudo crontab -u root -e`

* Per **eliminar les taques programades** de l'usuari actual.

  `crontab -r`
  
## l????

Les línies són formades pels camps: 

**&lt; minut >  &lt; hora>  &lt; diaMes>  &lt; mes>  &nbsp;&nbsp;  &lt; diaSetmana>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &lt; usuari>  &lt; comanda>**
&nbsp;&nbsp; (0-59) &nbsp;&nbsp;&nbsp; (0-23) &nbsp;&nbsp;&nbsp; (1-31)   &nbsp;&nbsp;&nbsp;&nbsp; (1-12) &nbsp;  (0 o 7=diumenge - 6)


**Usuari:** l'usuari que s'utilitzarà per a executar la comanda especificada.

| Símbol        | Significat                                          | Exemple          |                                      |
|---------------|-----------------------------------------------------|------------------|--------------------------------------|
| *             | Cada unitat de temps                                |     diaMes *     | Cada dia                             |
| num           | Per indicar el moment concret                       |      Hora 15     | A les 15:00h                         |
| num-num       | Rang de números                                     |      Mes 1-6     | Del Gener al Juny                    |
| num, num, num | Per indicar valors concrets de hores, dies o mesos. | diaSetmana 1,3,5 | Cada dilluns, dimecres i divendres   |
| */num         | Cada determinat temps                               |     Hores */2    | Cada 2 hores                         |
| num-num/num   |                                                     |    Hora 8-20/5   | Entre les 8h i les 20h, cada 5 hores |


## Amb entorn gràfic

Per automatitzar tasques en mode gràfic, s'utilitza el programa anomenat **Tareas programadas (_gnome-schedule_)**.

Amb Ubuntu hi accedim des de **_Aplicacions> Eines del sistema > Tasques programades_**

Aquest programa permet programar tasques per ser realitzades només una vegada o periòdicament.

> IMATGE