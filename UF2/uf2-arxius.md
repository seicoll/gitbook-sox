# Gestió d'arxius

## Comprimir i descomprimir

### Comandes gzip i gunzip

> Les comandes **gzip/gunzip** serveixen per comprimir/descomprimir un únic arxiu o directori.

![](/assets/uf2-gzip.png)

El nom de l'arxiu comprimit és el mateix que el de l'arxiu original però afegint l'extensió **.gz**.

```
gzip -c document
gunzip -c document.gz
```
**Opcions:**
* `-c` manté l'arxiu original (evita que s'elimini automàticament)
* `-r` per comprimir de forma recursiva (directoris).

### Comanda tar

La comanda **tar** serveix per empaquetar/desempaquetar un conjunt d'arxius (sense comprimir-los).

![](/assets/uf2-tar.png)

**Opcions d'empaquetat:**
* `-c` crear arxiu empaquetat (si existeix, primer l'esborra).
* `-x` o `--extract` desempaquetar arxiu.
* `-f` indica la ruta al fitxer creat (tar).
* `-v` _verbose_ (mostra els arxius comprimits o descomprimits).



**Empaquetar i desempaquetar un directori**:

```
tar -cvf documents.tar ./documents/
tar -xvf documents.tar
```

Si a més es vol **comprimir/descomprimir** utilitzant el format **.gz** cal afegir el paràmetre **z**.



**Opcions de compressió:**
* `-z` comprimir / descomprimir amb algoritme gzip.

![](/assets/uf2-tar2.png)

Per **comprimir tot un directori**:

`tar -zcfv arxiu_comprimit.tar.gz directori`

Per **descomprimir**:

`tar -xfv arxiu_comprimit.tar.gz`

### Comanda zip

Les comandes `zip` i `unzip` permeten comprimir i descomprimir arxius i directoris.

![](/assets/uf2-zip.png)

**Paràmetres:**
* `-r` per comprimir de forma recursiva (directoris).

Per comprimir tot un directori:

`zip -r arxiu_comprimit.zip directori`

Per descomprimir:

`unzip arxiu_comprimit.zip`

## Documentació i altres recursos

* **Apunts SOX Pere Sánchez:** [Edició d'arxius](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?ref=2221)
* **Apunts SOX Pere Sánchez:** [Gestió d'arxius](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?ref=2222)
* **Apunts SOX Pere Sánchez:** [Gestió de carpetes](http://moodlecf.sapalomera.cat/apunts/smx/sox/index.html?ref=2223)



