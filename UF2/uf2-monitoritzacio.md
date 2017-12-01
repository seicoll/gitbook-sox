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

## Monitorització dels processos

La comanda **top** mostra una llista interactiva dels processos i permet realitzar diferents accions sobre cadascun d’ells, com matar-los o canviar la seva prioritat.

```bash+theme:dark
top - 22:58:01 up 26 min,  1 user,  load average: 0,22, 0,25, 0,26
Tasks: 273 total,   3 running, 270 sleeping,   0 stopped,   0 zombie
%Cpu(s):  3,1 us,  1,2 sy,  0,0 ni, 95,1 id,  0,6 wa,  0,0 hi,  0,0 si,  0,0 st
KiB Mem :  5985624 total,   770544 free,  2628672 used,  2586408 buff/cache
KiB Swap:  6168572 total,  6168572 free,        0 used.  2166152 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND     
 1365 root      20   0  558316 111516  85580 R   4,9  1,9   0:42.35 Xorg        
 1836 usuari    20   0 2060704 146844  60344 R   4,9  2,5   0:51.43 cinnamon    
 2637 usuari    20   0 1383888 300880 137884 S   4,9  5,0   1:24.64 chrome      
 5361 usuari    20   0   43440   3828   3092 R   2,4  0,1   0:00.07 top         
    1 root      20   0  119912   6064   3972 S   0,0  0,1   0:01.69 systemd     
    2 root      20   0       0      0      0 S   0,0  0,0   0:00.00 kthreadd    
    4 root       0 -20       0      0      0 S   0,0  0,0   0:00.00 kworker/0:+ 
```

La comanda **ps** permet conèixer els processos que s’estan executant al sistema.
Sense opcions ens permet conèixer els processos que s’estan executant en el terminal actual.

```bash+theme:dark
usuari@usxxx:~$ ps -l
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000  5341  5337  0  80   0 -  6021 wait   pts/0    00:00:00 bash
4 R  1000  5775  5341  0  80   0 -  7607 -      pts/0    00:00:00 ps
```

* Per veure la informació detalla de tots els processos:
`ps aux`

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