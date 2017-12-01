# Monitorització

## CPU, memòria RAM i memòria d'intercanvi

Amb les comandes `cat /proc/cpuinfo` i `cat /proc/meminfo` es pot veure informació detallada sobre la **CPU** i la **RAM**:

```bash+theme:dark
usuari@usxxx:~$ cat /proc/cpuinfo
processor     : 0
vendor_id     : GenuineIntel
cpu family    : 6
model         : 15
model name    : Intel(R) Core(TM)2 Duo CPU     E6750  @ 2.66GHz
cpu MHz       : 2671.640
cache size    : 4096 KB
cpu cores     : 2
flags         : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge
                mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2
                ss ht tm pbe syscall nx lm constant_tsc arch_perfmon
                pebs bts rep_good nopl aperfmperf pni dtes64
bogomips      : 5343.28
cache_alignment    : 64
address sizes      : 36 bits physical, 48 bits virtual
```

```bash+theme:dark
usuari@usxxx:~$ cat /proc/meminfo
MemTotal:        4047564 kB
MemFree:          244320 kB
Buffers:           44824 kB
Cached:           669356 kB
SwapCached:        11084 kB
Active:          1477644 kB
Inactive:         941728 kB
SwapTotal:       1179644 kB
SwapFree:        1081312 kB
DirectMap4k:     1541632 kB
DirectMap2M:     2652160 kB
```

Amb la comanda `free` es pot veure informació resumida sobre la memòria RAM i la memòria virtual (memòria d'intercanvi o **swap**): el total, la quantitat utilitzada i la quantitat lliure.

```bash+theme:dark
usuari@usxxx:~$ free
                  total      usado        libre    compart.     búffers     almac.
Mem:            4047564    3640916       406648       96748       38364     532712
-/+ buffers/cache:         3069840       977724
Intercambio:    1179644      98332      1081312
```

## Monitorització de la xarxa

Per obtenir informació sobre la configuració de la xarxa, es poden utilitzar les següents comandes:
* **ipconfig** mostra l'adreça IP, la màscara (i altres, com per exemple l'adreça MAC).
* **route** permet veure la porta porta d'enllaç.
* **cat /etc/resolv.conf** serveix per saber quins servidors DNS s'han configurat.

Per comprovar la connectivitat:
* **ping** per comprovar la connectivitat punt a punt.
* **traceroute** per descobrir en quin punt falla la connectivitat entre dos punts.
* **host** permet comprovar la resolució DNS.
* **nslookup** (obsolet; és equivalent a host): per defecte no ve instal·lat.

Per comprovar la seguretat (ports oberts):
* **nmap**: serveix per comprovar els ports oberts en l'ordinador.

## Documentació i recursos

* **Guia del servidor de l'Ubuntu** [https://help.ubuntu.com/lts/serverguide/monitoring.html](https://help.ubuntu.com/lts/serverguide/monitoring.html)