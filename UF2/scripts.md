# Scripts

> Un **script** és un arxiu de text executable que conté una sèrie de comandes. Quan s'executa l'script, s'executen les comandes que conté.

Es pot crear i editar un script amb qualsevol editor de text pla (nano, gedit...).

El més habitual és posar l'extensió **.sh** als scripts de Linux:

`nano crea_directoris.sh`

En la primera línia cal indicar amb quin intèrpret de comandes s'han d'executar les comandes que conté (#!/bin/bash).
A continuació es posen les comandes en el mateix ordre en què s'han d'executar:

```bash
#!/bin/bash
mkdir /home/usuari/SOX
mkdir /home/usuari/SOX/UF1
mkdir /home/usuari/SOX/UF1/Apunts
mkdir /home/usuari/SOX/UF1/Practiques
```

Un cop creat el script cal modificar els permisos de l'arxiu per permetre que s'executi:

```bash+theme:dark
chmod a+x crea_directoris.sh
```

Per executar-lo des del mateix directori on es troba cal posar ./ (o la ruta sencera):

```bash+theme:dark
./crea_directoris.sh
```

També es pot executar amb la comanda bash.
En aquest cas no caldria canviar els permisos ni posar ./ al davant si estem en el mateix directori:

```bash+theme:dark
bash crea_directoris.sh
```

## Exemples d'scripts

### Trobar els 10 directoris més grans donat un path

```bash+theme:dark
$ cat grans
#!/bin/bash
# Llista els 10 directoris que ocupen més espai donat un path

 du $1 | sort -n | tail
 ``` 
 

