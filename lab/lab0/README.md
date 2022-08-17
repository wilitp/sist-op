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
curl https://raw.githubusercontent.com/andergd/separadorSilabas/master/Carroll%2C%20Lewis%20-%20Alicia%20En%20El%20Pa%C3%ADs%20De%20Las%20Maravillas.txt | sed 's/Alicia/Guille/g' > Guille_en_el_pais_de_las_maravillas.txt
```

#### 4)
```bash
sort weather_cordoba.in -k 5| head -n 1 |awk '{printf "Minima %u/%u/%u\n", $2, $3, $1}'
sort weather_cordoba.in -k 5| tail -n 1 |awk '{printf "Maxima %u/%u/%u\n", $2, $3, $1}'
```

#### 5)

```bash
sort -k --sort=g atpplayers.in # --sort=g <- ordenar interpretando como números
```

#### 6)
```
```


