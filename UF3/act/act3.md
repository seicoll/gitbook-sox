<!-- notoc -->

# Activitat 3. Compartir carpetes en GNU/Linux amb NFS

![](/assets/nfs.jpg)

## Requisits

* Utilitzeu dues màquines virtuals amb Ubuntu (Client i Servidor).

* Configureu-les per tal de que estiguin connectades a una **xarxa interna** i tinguin una IP privada.

## Activitat

Crea carpetes compartides en el teu servidor utilitzant NFS i accedeix-hi des d'un client.


**Exercici 1: Configuració del servidor**

Crea les carpetes següents a `/srv/nfs` i comparteix-les per tots els usuaris:

* **SOX**: Hi has de poder accedir **només** en mode lectura i només des de la IP del ordinador client. Mostra també com no pots accedir-hi des d'un segon client.

* **Xarxes**: S'hi ha de poder accedir en mode lectura i escriptura des de tots els ordinadors de la xarxa.

* **Seguretat**: Només s'hi ha de poder accedir amb permisos de lectura/escriptura des d'un ordinador concret (Tria tu la IP). Des dels altres només s'hi ha de poder accedir amb permisos de  lectura.

  > Caldrà que mostris la configuració del fitxer `/etc/exports`.

**Exercici 2: Configuració del client**

2.1. En un màquina **client Linux**, crea les carpetes que farem servir després com a **punt de muntatge** per a les carpetes compartides del servidor.

```
sudo mkdir /mnt/nfs/SOX /mnt/nfs/Xarxes /mnt/nfs/Seguretat
```

2.2. Munta els tres directoris remots mitjançant l’ordre **mount**.

  a. Comprova que no tens permisos d’escriptura a la carpeta SOX.

  b. Comprova que pots escriure a la carpeta Xarxes.

2.3. Configurar el **muntatge automàtic** d’aquestes carpetes utilitzant el fitxer `/etc/fstab` per tal que aquestes carpetes es muntin automàticament al iniciar sessió.
