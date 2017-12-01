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
peter@ubuntu14:~$ cat /proc/meminfo
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