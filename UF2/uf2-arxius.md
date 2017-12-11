# Gestió d'arxius

## Comprimir i descomprimir

### Comandes gzip i gunzip

Les comandes **gzip/gunzip** serveixen per comprimir/descomprimir un únic arxiu.
El nom de l'arxiu comprimir és el mateix que el de l'arxiu original però afegint l'extensió **.gz**.

```
gzip -k document
gunzip -k document.gz
```

### Comanda tar

La comanda **tar** serveix per empaquetar/desempaquetar un conjunt d'arxius (sense comprimir-los).

```
tar -cvf documents.tar ./documents/
tar -xvf documents.tar
```

Si a més es vol comprimir/descomprimir utilitzant el format **.gz** cal afegir el paràmetre **z**.

```
tar -zcvf documents.tar.gz ./documents/
tar -zxvf documents.tar.gz
```

**Paràmetres:**
* `-z` comprimir / descomprimir.
* `-c` crear arxiu empaquetat (si existeix, primer l'esborra).
* `-x` desempaquetar arxiu.
* `-f` indica que ha de treballar amb arxius.
* `-v` verificar (mostra els arxius comprimits o descomprimits).

Per comprimir tot un directori:

`tar -zcfv arxiu_comprimit.tar.gz directori`

Per descomprimir:

`tar -xfv arxiu_comprimit.tar.gz`

### Comanda zip

**Paràmetres:**
* `-r` per comprimir de forma recursiva (directoris).

Per comprimir tot un directori:
`zip -r arxiu_comprimit.zip directori`

Per descomprimir:
`unzip arxiu_comprimit.zip`
