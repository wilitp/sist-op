# 1.
a) Al menos dos núcleos.

b) Porque durante esa diferencia de tiempo el sistema puede estar ejecutando otros procesos.

c) 

- La ejecución usa en gran proporción a un cpu.

- Se ejecuta cada instancia en un cpu distinto.

- Se ejecuta una instancia, pero a diferencia de la primera usa el cpu en menor medida(lo comparte más con otros procesos)

- Se ejecutan dos instancias en un cpu y las otras dos en otro. Usan la mayoría del tiempo de cpu.

- Tres instancias comparten los dos cpu's de alguna manera.

- Dos instancias se ejecutan usando ~2.40'' cada una en un walltime de ~5''. Esto da a entender que se ejecutaron ambas en un solo cpu.

- 4 instancias que insumen ~2.40'' de cputime tardan ~7'', lo que me hace suponer que corrieron tres instancias en un cpu y otra en otro. Otra opción es que hayan compartido más el cpu con otros procesos.

# 2.
Porque el proceso dgemm usa hilos, que pueden correr en distintos cpu's al mismo tiempo.

# 4.

a) Vale 100 en cada proceso.
b) La variable está en address spaces distintos. Si uno la cambia el otro no es afectado.
c) Si la variable estuviera en un registro entonces más que en address spaces distintos, está en contextos de ejecución distintos, por lo que el funcionamiento sigue siendo el mismo que en b).

# 5

RTA: 2^(f+1) - 1

# 6

La cantidad que imprima el programa `bin/date` si es que la llamada a `execv` es exitosa. Sino imprime "a" una vez.

# 7

El primero se ejecuta a si mismo pero sin el último argumento. El efecto es el mismo que ignorar los argumentos.

El segundo hace lo mismo pero ignorando los últimos dos argumentos. También hace un fork al medio pero el proceso hijo que se desprende retorna inmediatamente.

# 8

Con dup es posible tener más cuidado al cerrar stdin / stdout. También podemos preservar los streams std en otro file descriptor aunque los hayamos cerrado en 0 y 1.

# 9

Se puede mitigar el efecto de la bomba fork limitando la cantidad de procesos hijos que puede spawnear un proceso.

# 10
READY <-> RUNNING -> BLOCKED -> %

Si quitamos ready -> running, los procesos no podrían correrse nunca.

Si quitamos running -> ready, no podríamos ejecutar otro proceso a menos que este se bloquee esperando IO.

Si quitamos running -> blocked, los procesos no podrían esperar IO.

Si quitamos blocked -> ready, los procesos no podrían volver a ser ejecutados una vez que se bloquean.

# 11

Lo dice en el archivo explicitamente.

# 12

a) V porq se pueden ejecutar hilos en distitos cpu's.
b) F el chiste es que si puedan.
c) V 
d) F hay instrucciones que no están disponibles en modo usuario.
e) V no necesariamente el scheduler va a decidir ejecutar otro proceso cuando hay un trap por timer.
f) V el pid 0 está reservado para el kernel
g) V
h) F los procesos huérfanos son asignados como hijos de init(el primero proceso)
i) F se pueden comunicar usando memoria compartida, pipes y también mediante el exit code del hijo
j) F se ejecuta si la llamada no es exitosa(e.g el programa no existe)
k) F Si el proceso padre termina entonces se limpian a los hijos de la tabla

# 16
Asumiendo que un proceso que llega(arrival) en el momento x no puede ejecutarse en ese mismo momento y que todos lor procesos bloqueados no se excluyen mutuamente tenemos:

```
time    : 01234567890123456789
running :  AACBBACCBBBBAACBBABBCCBBBB
ready   : ACBBAABBB   ABBB    CBB                                        
            CA          C                                             
blocked :     CCCAAAAA   AAAA                     
                   CCCCC  CCCC                                     
                            B 
```

# 17

```
time    : 012345678901234567890
running :  ABCAADBECCDDEEAAACEA                                                                                      
ready   : ABCACCCCCDDAAAAEEEAA                                                                    
             BBBBDDAAEECCCCC                                                                                      
              DDAAAEECC 
                 E
```

# 18
a) F
b) F: caso con un solo proceso es un contraejemplo
c) V
e) F: no independiente del movimiento entre colas, sino independiente de los yields



