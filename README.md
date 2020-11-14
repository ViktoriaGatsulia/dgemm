# Перемножение матриц

## Профилирование с помощью perf

### 1. Установка perf

* Важно загрузить perf именно для вашей версии ядра (узнать версию ядра ````$ uname -r````)
````$ sudo apt install linux-tools-5.4.0-53-generic````

### 2. Компиляция
````gcc -O0 -g ./src/dgemm.c````

### 3. Определение количества cache-misses
````$ perfstat -e cache-misses ./dgemm````

### Поэлементный перебор
````
2048 289.492929

 Performance counter stats for './a.out':

    22 188 967 228      cache-misses                                                

     340,823636978 seconds time elapsed

     339,210189000 seconds user
       0,315812000 seconds sys
````

### Построчный перебор
````
2048 54.118265

 Performance counter stats for './a.out':

     1 766 519 519      cache-misses                                                

      94,647569887 seconds time elapsed

      94,419807000 seconds user
       0,095991000 seconds sys
````

### Блочный перебор
````
2048 35.702269

 Performance counter stats for './a.out':

       232 508 984      cache-misses                                                

      76,413201185 seconds time elapsed

      76,352782000 seconds user
       0,043998000 seconds sys
````
