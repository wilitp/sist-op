# Lab 0

#### 1)
```bash
grep "model name" /proc/cpuinfo # Intel i5
```

#### 2)

```bash
grep "model name" /proc/cpuinfo |wc -l # 12
```

#### 3)
```bash

# Descargamos el archivo y lo escribimos al stdout
# Hacemos el reemplazo con sed y direccionamos el output al archivo nuevo

wget -O - https://raw.githubusercontent.com/andergd/separadorSilabas/master/Carroll%2C%20Lewis%20-%20Alicia%20En%20El%20Pa%C3%ADs%20De%20Las%20Maravillas.txt | sed 's/Alicia/Guille/g' > Guille_en_el_pais_de_las_maravillas.txt
```

#### 4)
```bash
sort weather_cordoba.in -k 5 -g | head -n 1 |awk '{printf "Minima %u/%u/%u\n", $2, $3, $1}' && sort weather_cordoba.in -k 5 -g | tail -n 1 |awk '{printf "Maxima %u/%u/%u\n", $2, $3, $1}'

# Alternativa para no ordenar al pedo

# Tenemos un bloque de inicializacion, uno para ir actualizando el min y el max y uno que los imprime al final
# Despues le cambiamos el formato a las dos lineas que imprimimos
awk '!init{min = max = $5; lin_min = lin_max = $0; init=1; next;} {if($5 > max){max = $5; lin_max = $0} ; if($5 < min){min=$5; lin_min = $0} } END {print "Minima " lin_min; print "Maxima " lin_max}' weather_cordoba.in | awk '{printf "%s %s/%s/%s\n", $1, $3, $4, $2 }' 
```

#### 5)

```bash
sort -k --sort=g atpplayers.in # --sort=g <- ordenar interpretando como números
```

#### 6)
```

# Primero imprimimos todas las lineas pero con (puntaje + goles a favor - goles en contra) como ultima columna
# Despues ordenamos segun la nueva columna
# Imprimimos todas las lineas, pero antes le restamos 1 a NF(number of fields) para que print imprima todas las columnas menos la ultima

awk '{printf "%s %s\n", $0, ($2 + $7 - $8)}' superliga.in | sort --sort=g -k 2 -k 9 -r |awk '{NF--;print}'

```

#### 7)
```bash
ip l |grep 'link/ether ..:..:..:..:..:..' |grep  '..:..:..:..:..:..' # imprime las macs de todas las interfaces de ethernet 
```

#### 8)

```bash
# a)
touch fma_S1_{01..10}_es.srt

# b)
for f in *_es*; do mv $f ${f%_es.srt}.srt; done
```


