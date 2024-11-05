
# Material Pre-Estudio Paradigma Paralelo
Estos son unos recursos en el cual puede aprender lo principal o estudiar mas afondo sobre el paradigma paralelo que hablaremos el dia miercoles 11/4/2024

## Conceptos

El paralelismo es una técnica de computación que busca dividir un problema grande en problemas más pequeños que pueden resolverse al mismo tiempo, permitiendo ejecutar más instrucciones en menos tiempo. Es fundamental en áreas que requieren un alto procesamiento y memoria, como las simulacion científicas y la generación de gráficos computacionales.
La esencia de la computación paralela reside en una premisa sencilla pero poderosa: dividir un problema grande en subproblemas más pequeños y resolverlos simultáneamente. Esta estrategia, conocida como "divide y vencerás", permite acelerar significativamente el proceso de cálculo, ya que múltiples procesadores o núcleos trabajan de forma coordinada en diferentes partes del problema. Pero estamos hablando de la computacion y no un paradigma, ¿Por qué es un paradigma?

## ¿Por qué es un paradigma?

Un paradigma es un modelo o conjunto de conceptos, teorías, prácticas y métodos que definen una visión del mundo y una forma de abordarlo. En otras palabras, es una especie de lente a través del cual vemos y entendemos la realidad. Los paradigmas son fundamentales en cualquier disciplina, ya que guían la investigación, la enseñanza y la resolución de problemas.
El hecho de que la programación paralela sea un paradigma se debe a que ha transformado la manera en que abordamos los problemas computacionales, impulsando el desarrollo de nuevas herramientas, técnicas y hardware. Este cambio de paradigma ha permitido resolver problemas antes inabordables y ha abierto nuevas posibilidades en diversos campos de la ciencia y la tecnología, esto también nos demuestra que existe una razón por la cual no ha dejado de ser necesaria.

Ha dado lugar a nuevas herramientas y técnicas de programación:
Para aprovechar al máximo el potencial de la computación paralela, se han desarrollado lenguajes de programación específicos, bibliotecas y frameworks que facilitan la escritura de programas paralelos. Además, han surgido nuevas técnicas de programación como la programación concurrente y la programación distribuida.
Ha impulsado el desarrollo de nuevas arquitecturas de hardware:
Para soportar las cargas de trabajo paralelas, se han diseñado procesadores multinúcleo, sistemas multiprocesador y aceleradores como las GPUs. Estas nuevas arquitecturas permiten ejecutar múltiples hilos de ejecución de forma simultánea y mejorar el rendimiento de las aplicaciones paralelas.

## Ventajas y desventajas:

### Ventajas

- Resuelve problemas que no se podrían realizar en una sola CPU
- Resuelve problemas que no se pueden resolver en un tiempo razonable
- Permite ejecutar problemas de un orden y complejidad mayor
- Permite ejecutar código de manera más rápida (aceleración)
- Permite ejecutar en general más problemas
- Obtención de resultados en menos tiempo
- Permite la ejecución de varias instrucciones en simultáneo
- Permite dividir una tarea en partes independientes
- Ofrece mejor balance entre rendimiento y costo que la computación secuencial
- Gran expansión y escalabilidad

### Desventajas

- Mayor consumo de energía
- Mayor dificultad a la hora de escribir programas
- Dificultad para lograr una buena sincronización y comunicación entre las tareas
- Retardos ocasionados por comunicación ente tareas
- Número de componentes usados es directamente proporcional a los fallos potenciales
- Altos costos por producción y mantenimiento
- Condiciones de carrera

## Podemos desglosar este paradigma para entenderlo mejor:
**Problema:** El problema es aquello que queremos resolver, la tarea inicial a la cual queremos darle una solución.

**Tareas:** Las tareas son aquellas en las que descomponemos el problema, es decir, las partes en las que vamos a dividirlo para darle una solución más rápida y efectiva. Estas están compuestas por un conjunto de instrucciones que luego serán interpretadas y ejecutadas por un procesador.

**Granularidad:** Es el tamaño de nuestro problema y sus tareas, esta dividida en dos tipos de granularidad, las gruesas y finas.

**Granularidad Gruesa:** Es una cantidad grande de trabajo en extensión, tiene alta independencia entre sus tareas. Una granularidad gruesa esta conformada por el problema inicial y pocas tareas (1,2,3), pero cada tarea es complicada y al juntarlas resuelven el problema inicial con facilidad.

**Granularidad fina:** son cantidades pequeñas de trabajo, pero están divididas en muchas tareas (5,6,7), lo cual significa que para un problema inicial pueden salir bastantes tareas, al ser de esta forma es necesaria una mayor dependencia de unas con otras, normalmente al unirlas todas, primero se resuelven problemas entre las tareas y al finalizar si se resuelve el problema inicial.

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

    # Dividir la lista en fragmentos
    fragmentos = [numeros[i:i + len(numeros) // num_procesos] for i in range(0, len(numeros), len(numeros) // num_procesos)]

    # Crear los procesos
    with multiprocessing.Pool(processes=num_procesos) as pool:
        resultados = pool.map(calcular_cuadrado, fragmentos)

    # Combinar los resultados
    resultados_finales = [num for sublista in resultados for num in sublista]

    print("Tiempo de ejecución:", time.time() - start_time)
```
