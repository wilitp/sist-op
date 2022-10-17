# 8
 Una computadora proporciona a cada proceso 65536 bytes de espacio de direcciones
dividido en páginas de 4 KiB. Un programa específico tiene el segmento código de 32768 bytes de
longitud, el segmento montículo de 16386 bytes de longitud, y un segmento pila de 15870 bytes.
¿Cabrá el programa en el espacio de direcciones? ¿Y si el tamaño de página fuera de 512 bytes?
Recuerde que una página no puede contener segmentos de distintos tipos asi se pueden proteger cada
uno de manera adecuada.

RTA: 
total: 16 pages
code : 8  pages
heap : 5  pages
stack: 4  pages

No entran todos

pero con páginas de 512 bytes tenemos:

total: 128 pages
code : 64  pages
heap : 33   pages
stack: 31  pages

Si entran todos(exactamente)

# 9
Dada la free list:

10k -> 4k -> 20k -> 18k -> 7k -> 9k -> 12k -> 15k

Solicitudes := 12k, 10k, 9k.

a) first fit: 

10k -> 4k -> *8k* -> 18k -> 7k -> 9k -> 12k -> 15k

4k -> 8k -> 18k -> 7k -> 9k -> 12k -> 15k

4k -> 8k -> *9k* -> 7k -> 9k -> 12k -> 15k

b) best fit:

10k -> 4k -> 20k -> 18k -> 7k -> 9k -> 15k

4k -> 20k -> 18k -> 7k -> 9k -> 15k

4k -> 20k -> 18k -> 7k -> 15k

c) worst fit:

10k -> 4k -> *8k* -> 18k -> 7k -> 9k -> 12k -> 15k

10k -> 4k -> 8k -> *8k* -> 7k -> 9k -> 12k -> 15k

10k -> 4k -> 8k -> 8k -> 7k -> 9k -> 12k -> *6k*

d) next fit

10k -> 4k -> *8k* -> 18k -> 7k -> 9k -> 12k -> 15k

10k -> 4k -> 8k -> *8k* -> 7k -> 9k -> 12k -> 15k

10k -> 4k -> 8k -> 8k -> 7k -> 12k -> 15k

# 10

La TLB de una computadora con una pagetable de un nivel tiene una eficiencia del
95 %. Obtener un valor de la TLB toma 10ns. La memoria principal tarda 120ns. ¿Cuál es el tiempo
promedio para completar una operación de memoria teniendo en cuenta que se usa tabla de páginas
lineal?

0.95 * (10ns + 120ns) + 0.05 * (10ns + 120ns + 10ns + 120ns) = 136.5

# 11
a)
M := 1024
N := 64 * 1024

b)
M := 1024
N := 65 * 1024 en el caso que se invalide la entrada mas vieja

# 12
a) 4
b) 
- #39424

V = 9 -> F = 0b110 = 6
fisica = 0x6a00 valida

- #12416

V = 3 -> F = 0b101 = 5
fisica = 0x5080 valida

- #26112 = 0x6600 -> V = 6 -> F = 0

fisica = 0x0600 invalida

- #63008 = 0xF620
fisica = 0x2620

- #21760 = 0x5500
fisica = 0x1500

- #32512 = 0x7f00
fisica = 0x0f00

- #43008 = 0xa800
fisica = 0x4800

- #36096 = 0x8d00
fisica = 0x3d00

- #7424 = 0x1d00
fisica = 0x7d00

- #4032 = 0x0fc0
fisica = 0x0fc0

c)
- #16385 = 0x4001
F      := 0b100
offset := 0x001
virtuales := 0x4001, 0xa001

- #4321 = 0x10e1
F      := 1
offset := 0x0e1
virtual := 0x50e1

# 13
- 0x003FF666
offset := 0x666
level1 := 0x0
level2 := 0x3FF

fisica := 0xcaeea666

- 0x00000AB0

offset := 0xAB0
level1 := 0x0
level2 := 0x0
fisica := 0xCAFECAB0

- 0x00800B0B
offset := 0xB0B
level1 := 0x2
level2 := 0x0
fisica := 0xCACACB0B

# 14


a)
 --> page directory(siempre tenes uno de estos xd)
 |
4k + 8 * 4k = 36k
     ------
       |
       --> page directory entries

b) 4k + k * 4k = 4k + 4m

c) 
4g / length(page_frame) = 4g / 4k = m

Entonces necesitamos un mega pages. En una tabla lineal necesitamos 4 bytes por page -> necesitamos una tabla de 4m de tamaño
Menos, ya que no tendriamos el overhead del page directory, sino solo una tabla de 4m

d)

Doy el directorio y las dos page tables necesarias definidas en pseudo haskell:

```
pd[0] = {&pt, valid}
pd[2] = {&pt', valid}
pd[x] = {_, invalid}

pt[x] = {x, valid}

pt'[x] | x < 8  = {32k + x, valid}
       | otherwise = {_, invalid}
```

# 15

No se puede direccionar 4g, ya que no te queda espacio para las traducciones necesarias.

El máximo es 4g - 4k - 4m = 4(g - k - m) 

# 17 Verdadero o falso

a) hay una page table para cada proceso: V
b) La MMU siempre mapea memoria virtual más grande a memoria física más pequeña: F, no hay ninguna relación de tamaño fija
c) La dirección física siempre la entrega la TLB: F, Depende de si es hardware-managed
d) Dos páginas virtuales de un mismo proceso se pueden mapear a la misma página física: V


# 18 En el top-level directory se define la última entry como el mismo directory.

a) A dónde apunta la dirección virtual 0xFFC00000 = 0b11111111110..0

Apunta a la primera page-entry del address-space.

b) Y la 0xFFFE0000 = 0b111111111.1111110000

Apunta a la primera page-entry del directory indexado por 0b1111110000 en el directory principal.

c) 0xFFFFF000?

Apunta a la primera page-directory entry.

d) Para qué sirve?

Sirve para poder cambiar los mapeos de memoria.

# 19

### a) Acceso a null tira excepción.

La página en 0x0 es marcada como inválida.

### b) Archivo de intercambio o swap file

El sistema marca las páginas swapeadas como no presentes, por lo que si el usuario intenta accederlas habrá un page fault y el os podrá restaurar esa página en memoria.

### c) Demand paging para la carga de programas

No se carga todo el segmento de código de una, sino que se lo va cargando a medida que sea necesario. Esto es posible si marcamos las páginas como no presentes pero las identificamos como demand paging, luego cuando el programa intente accederlas podemos cargarlas. También se puede hace prefetching basado en algún criterio.

### d) Auto-growing stack.

Se puede poner una "guard page" arriba del stack. Esta sirve para alertar al os cuando el usuario intenta accederla y así incrementar el tamaño del stack.

### e) Non-executable stacks.

Las páginas que conforman el stack del proceso se marcan como no ejecutables.

### f) Memory mapped files mmap()

Nose

### g) Copy on write para fork()

Cuando se forkea, se marcan todas las páginas como read-only. Si un proceso faultea, entonces duplicamos el top-level page directory, duplicamos el page frame en cuestión y mappeamos el nuevo frame en el address-space del proceso.

### h) sbrk barato y malloc barato.

Supongo que se refiere a demand zeroing. La técnica consiste de no mapear page-frames posta hasta que el usuario no los acceda, sino que únicamente los marcamos(a las page table entries) mediante algún bit reservado para el sistema para que cuando el proceso faultee sepamos que tenemos que buscarle un page-frame.

### i) malloc(), memset(0) = calloc() barato.

Supongo que es lo mismo que lo de arriba pero sumado que cuando finalmente se mapean los page-frames también se los zeroea.

### j) Código compartido entre procesos: shared libraries, código de kernel, etc.

Para compartir memoria sólo hay que mapear entries a los mismos page-frames.

### k) Memoria compartida entre procesos.

Lo mismo que j)

