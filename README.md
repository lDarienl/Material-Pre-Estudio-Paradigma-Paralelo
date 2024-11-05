# Índice
* [**Introducción**](#introducción)
   * [**Relación entre el paradigma paralelo y la computación paralela**](#relación-entre-el-paradigma-paralelo-y-la-computación-paralela)
* [**Conceptos**](#conceptos)
* [**¿Por qué es un paradigma?**](#por-qué-es-un-paradigma)
* [**Ventajas y Desventajas**](#ventajas-y-desventajas)
  * [**Ventajas**](#ventajas)
  * [**Desventajas**](#desventajas)
* [**Podemos desglosar este paradigma para entenderlo mejor:**](#podemos-desglosar-este-paradigma-para-entenderlo-mejor)
* [**Ejemplos en Codigo**](#ejemplos-en-codigo)
  * [**Python**](#python)
  * [**C++**](#c-con-openmp)
* [**Anexos y Bibliografias**](#anexos-y-bibliografias)



# Introducción
Estos son recursos con los que pueden aprender lo básico o estudiar más a fondo sobre el paradigma paralelo, que trataremos el día miércoles 11/4/2024.

> [!TIP]
> Este paradigma no solo es útil en áreas de alto procesamiento, sino también en aplicaciones comunes como redes sociales y videojuegos, donde mejorar la eficiencia es clave.

## Relación entre el paradigma paralelo y la computación paralela
Mientras que el paradigma paralelo es una estrategia de diseño y programación que describe cómo dividir y resolver tareas simultáneamente, la computación paralela es la implementación práctica de ese paradigma, que ocurre en sistemas de hardware y software que permiten la ejecución simultánea de varias tareas. En otras palabras:

- El paradigma paralelo es el conjunto de principios y técnicas que guían el diseño de software paralelo.
- La computación paralela es la práctica de usar múltiples procesadores o núcleos para resolver un problema mediante los principios del paradigma paralelo.

## Conceptos

El paralelismo es una técnica de computación que busca dividir un problema grande en problemas más pequeños que pueden resolverse al mismo tiempo, permitiendo ejecutar más instrucciones en menos tiempo. Es fundamental en áreas que requieren un alto procesamiento y memoria, como las simulación científicas y la generación de gráficos computacionales.
La esencia de la computación paralela reside en una premisa sencilla pero poderosa: dividir un problema grande en subproblemas más pequeños y resolverlos simultáneamente. 
>[!NOTE]
>Esta estrategia, conocida como "divide y vencerás", permite acelerar significativamente el proceso de cálculo, ya que múltiples procesadores o núcleos trabajan de forma coordinada en diferentes partes del problema.

## ¿Por qué es un paradigma?

Un **paradigma** es una perspectiva que reúne conceptos, teorías y prácticas para abordar problemas y guiar la investigación. En otras palabras, es una especie de lente a través del cual vemos y entendemos la realidad. Los paradigmas son fundamentales en cualquier disciplina, ya que guían la investigación, la enseñanza y la resolución de problemas.
La programación paralela es un paradigma porque ha transformado cómo abordamos problemas computacionales, impulsando nuevas herramientas, técnicas y hardware.

>[!TIP]
>Este cambio de paradigma requiere un cambio en la forma de pensar en comparación con paradigmas secuenciales.

Para aprovechar al máximo la computación paralela, se han desarrollado lenguajes, bibliotecas y frameworks específicos, además de arquitecturas de hardware avanzadas como procesadores multinúcleo y GPUs.

## Ventajas y desventajas:

### Ventajas

- Resuelve problemas que no se podrían realizar en una sola CPU y resolver en un tiempo razonable
- Permite ejecutar problemas de gran escala, más complejos y en menor tiempo.
- Obtención de resultados en menos tiempo
- Permite la ejecución de varias instrucciones en simultáneo y dividir una tarea en partes independientes
- Ofrece mejor balance entre rendimiento y costo que la computación secuencial
- Gran expansión y escalabilidad

>[!NOTE]
>La computación paralela permite ejecutar instrucciones simultáneamente, lo cual es ideal para problemas complejos y de gran escala.

### Desventajas

- Mayor consumo de energía y complejidad en la escritura de programas.
- Dificultad para lograr una buena sincronización y comunicación entre las tareas
- Retardos ocasionados por comunicación ente tareas
- Número de componentes usados es directamente proporcional a los fallos potenciales
- Altos costos por producción y mantenimiento
- Condiciones de carrera

>[!CAUTION]
>El costo de comunicación entre tareas puede consumir tiempo y recursos, y el debugging en paralelo puede ser más complejo que en código secuencial.

## Podemos desglosar este paradigma para entenderlo mejor:
**Problema:** El problema es aquello que queremos resolver, la tarea inicial a la cual queremos darle una solución.

**Tareas:** Las tareas son aquellas en las que descomponemos el problema, es decir, las partes en las que vamos a dividirlo para darle una solución más rápida y efectiva. Estas están compuestas por un conjunto de instrucciones que luego serán interpretadas y ejecutadas por un procesador.

**Granularidad:** Es el tamaño de nuestro problema y sus tareas, esta dividida en dos tipos de granularidad, las gruesas y finas.

**Granularidad Gruesa:** La granularidad gruesa implica pocas tareas independientes de gran complejidad que, al unirse, resuelven el problema original.

**Granularidad fina:** La granularidad fina involucra numerosas tareas pequeñas que dependen entre sí, resolviendo el problema inicial en conjunto.

## Ejemplos en Codigo

### Python

```python
import multiprocessing
import time

def calcular_cuadrado(numeros):
    resultados = []
    for num in numeros:
        resultados.append(num * num)
    return resultados

if __name__ == '__main__':
    numeros = list(range(1000000))
    num_procesos = 4

    # Iniciar el tiempo de ejecución
    start_time = time.time()

    # Dividir la lista en fragmentos
    fragmentos = [numeros[i:i + len(numeros) // num_procesos] for i in range(0, len(numeros), len(numeros) // num_procesos)]

    # Crear los procesos
    with multiprocessing.Pool(processes=num_procesos) as pool:
        resultados = pool.map(calcular_cuadrado, fragmentos)

    # Combinar los resultados
    resultados_finales = [num for sublista in resultados for num in sublista]

    print("Tiempo de ejecución:", time.time() - start_time)
```

>[!NOTE]
>La variable start_time ahora captura el tiempo al inicio para medir la duración completa del proceso.

**Explicación:**

1. Dividir la lista: Se divide la lista de números en fragmentos iguales para que cada proceso trabaje en una parte.
2. Crear procesos: Se crea un pool de procesos con el número especificado.
3. Aplicar la función en paralelo: Se utiliza pool.map para aplicar la función calcular_cuadrado a cada fragmento en paralelo.
4. Combinar resultados: Se combinan los resultados de todos los procesos en una única lista.

### C++ con OpenMP

**¿Qué es OpenMP?**
OpenMP (Open Multi-Processing) es una API (Interfaz de Programación de Aplicaciones) que proporciona una forma sencilla y portátil de añadir paralelismo a programas C++ y Fortran. Permite a los programadores aprovechar la potencia de múltiples procesadores o núcleos en un sistema, sin la necesidad de escribir código altamente especializado.

**La biblioteca omp.h**
La biblioteca omp.h es la cabecera que debes incluir en tu código C++ para utilizar las directivas y funciones de OpenMP. Esta biblioteca proporciona una interfaz estándar para la programación paralela, lo que facilita la portabilidad de los programas a diferentes plataformas que soporten OpenMP.

**¿Cómo funciona OpenMP?**
OpenMP utiliza directivas que se añaden al código fuente para indicar al compilador cómo paralelizar ciertas secciones del programa. Estas directivas suelen empezar con #pragma omp.



```c++
#include <iostream>
#include <omp.h> // Biblioteca para OpenMP

int main() {
    const int N = 1000000;
    int arr[N];

    // Inicializar el arreglo
    for (int i = 0; i < N; ++i) {
        arr[i] = i;
    }

    int suma = 0;

    // Ejecución secuencial
    double start_time = omp_get_wtime();
    for (int i = 0; i < N; ++i) {
        suma += arr[i];
    }
    double end_time = omp_get_wtime();
    std::cout << "Suma secuencial: " << suma << " Tiempo: " << end_time - start_time << std::endl;

    // Ejecución paralela
    suma = 0;
    start_time = omp_get_wtime();
    #pragma omp parallel for ejecuta el bucle en múltiples hilos. 2. La reducción reduction(+:suma) asegura que los valores parciales de suma se sumen correctamente."
    for (int i = 0; i < N; ++i) {
        suma += arr[i];
    }
    end_time = omp_get_wtime();
    std::cout << "Suma paralela: " << suma << " Tiempo: " << end_time - start_time << std::endl;

    return 0;
}
```

>[!IMPORTANT]
>Asegúrate de habilitar OpenMP en el compilador y usar #include <omp.h> para el correcto funcionamiento de la paralelización.

**Explicación:**

1. Directiva #pragma omp parallel for: Esta directiva indica al compilador que el bucle for debe ejecutarse en paralelo en múltiples hilos.
2. Reducción (+:suma): La cláusula reduction(+:suma) garantiza que todas las contribuciones parciales a la variable suma se sumen correctamente al final.

**Ventajas de usar OpenMP**
- **Sencillez:** Permite añadir paralelismo a código secuencial existente con relativamente pocas modificaciones.
- **Portabilidad:** Los programas OpenMP pueden compilarse en diferentes plataformas que soporten OpenMP.
- **Flexibilidad:** Ofrece una amplia gama de directivas para controlar el paralelismo, la sincronización y la distribución de tareas.
- **Eficiencia:** Puede proporcionar una aceleración significativa en aplicaciones que son intensivas en cálculo.

**¿Para qué sirve OpenMP?**
OpenMP es ideal para paralelizar bucles, secciones críticas y tareas que pueden dividirse en partes independientes. Es ampliamente utilizado en aplicaciones científicas, de ingeniería y de procesamiento de datos, donde el rendimiento es crítico.

## Anexos y Bibliografias

- [**Aprender C++ Basico**](https://learnxinyminutes.com/docs/es-es/c++-es/)
- [**Aprender Python Basico**](https://learnxinyminutes.com/docs/es-es/python-es/)
- [**Programación Paralela**](https://ferestrepoca.github.io/paradigmas-de-programacion/paralela/paralela_teoria/index.html#two)
- [**Introduction to Parallel Computing Tutorial**](https://hpc.llnl.gov/documentation/tutorials/introduction-parallel-computing-tutorial)
- [**Algoritmos Paralelos**](https://informatica.uv.es/iiguia/ALP/materiales/1_1_a_ComputacionParalela.pdf)
- [**Multitarea e Hilos en Java con ejemplos**](https://jarroba.com/multitarea-e-hilos-en-java-con-ejemplos-thread-runnable/)
