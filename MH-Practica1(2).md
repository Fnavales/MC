Informe Técnico Meta-heurísticas - Práctica 1.b: Búsquedas por Trayectorias
===================
**Nombre:** Francisco Javier Navarro Morales
**DNI:** 75897957-G
**email:** frannavarromorales@correo.ugr.es
**Curso:** Tercero
**Grupo:** Viernes(17:30-19:30)  
**Problema:** *Selección de Características*  
**Algoritmos Realizados:** KNN, SFS, Local Search

---

2. Índice
---
[TOC]

---


3. Descripción del Problema
-------------

El problema que vamos a analizar es el de selección de características. Queremos reducir el número de características de distintas bases de datos (wdbc, movement-libras y arrhythmia) sin perder en calidad de la solución, de esta forma conseguimos ahorrar espacio eliminando aquellas características que no influyen en el resultado. 
Las bases de datos disponen de un numero finito de ejemplos con ciertas características clasificadas.
Para evaluar la calidad vamos a utilizar el numero de aciertos devuelto por el clasificador KNN (con k=3).
Luego utilizaremos dos tipos de soluciones distintas para intentar seleccionar las características más prometedoras, por un lado usaremos un algoritmo greedy o voráz, por otro lado usaremos distintas meta-heurísticas.

---

4. Descripción de la aplicación de los algoritmos
---
La solución obtenida es un vector del tamaño de las características de cada base de datos, S[ {0,1}* x número_características ], cada posición del vector indica si se elige (1) o  no se elige (0) dicha característica para la evaluacaión.

Las funciones comunes que he implementado son:  
> **Normalizar(data): **

> - Normaliza los valores(pasados a la función) de la base de datos para que todas las características tengan el mismo peso.
>  * Para cada característica:
	>      * Busca el max y el minimo
	>      * Operar con el valor de la característica 

> **Generar_particiones(data): **

> - Función que pasándole los datos divide las muestras entre train y test equitativamente entre clases(cada grupo contiene el mismo numero de ejemplos de cada clase)
>  * Separar los datos en clases
>  * Para cada grupo de muestras de una clase:
	>      * Mezclar aleatoriamente las muestras 
	>      * Dividir muestras entre train y test

> **getReduccion(mascara, n_caracteristicas): **

> - Función que calcula el porcentaje de reducción de la máscara.

> **getAccuracy(testSet, predictions):**

> - Función que calcula el porcentaje de acierto de la máscara, evaluando la clase del conjunto de test contra su predicción. 

> **generar_vecinos(mascara):**

> - Función que genera todos los vecinos de una máscara, para ello devuelve una lista con las posiciones cuyo valor es 0.
>  * Obtener lista de posibles vecinos(las posiciones de la mascara cuyo valor es 0), mezclarla aleatoriamente.
>  *  Poner la mascara a 1 en la posición que indique el primer valor de la lista de vecinos.
>  * Comprobar si el %acierto mejora
>          * En caso afirmativo:   
>          intercambiar mascara, actualizar %acierto.
>          * En caso negativo:
>          Quitar el último vecino de la máscara y terminar.
>  * Repetimos todo esto hasta que se vacíe la lista de vecinos.

---
5. Descripción en pseudocódigo de la estructura del método de búsqueda y las operaciones  relevantes
---

  

6. Descripción del algoritmo de comparación
---

> **knn(testSet, trainingSet, mascara, k=3, print_steps = False):**

> - Este algoritmo acepta los siguientes parámetros:
>  - testSet, es el conjunto que vamos a evaluar.
>   - trainingSet, el el conjunto sobre el que evaluamos los ejemplos de test.
>   - mascara, es una lista de {0,1} que representa si la característica ha sido o no seleccionada.
>    - k, número de vecinos.
>    - print_steps, sirve para ver los pasos resultados intermedios del algoritmo.

> El algoritmo genera una predicción de clases observando las k muestras mas cercanas a él, para medir la distancia entre las muestras usamos la suma de las distancias euclídeas de las características entra cada muestra. Para cada muestra de test se extraen las k muestras cercanas a él (denominados como  vecinos) y se elige la clase mayoritaria de entre sus vecinos, en case de empate se elige el vecino más cercano.


