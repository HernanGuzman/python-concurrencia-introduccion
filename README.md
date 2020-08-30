# To `join()` or not to `join()`...

En `dormilones.py` vimos tres ejemplos básicos de ejecución:

- Clásico secuencial,
- Con threads,
- Y con threads, pero esperando a que terminen usando `join()`.

Entonces responda:
- ¿Por qué los segundos que se imprimen que pasaron son 2, 0 y 1 (aprox.) respectivamente?
* Para el primer caso.
Primero llama a la función dormir. Esto hace que pase un 1.
Luego llama a la funcion dormir y vuelve a pasar 1 segundo, lo que en total suma 2 segundos.

* En el segundo caso
Se declaran dos hilos, que son inicializados y llaman a la funcion dormir. Pero en este caso el hilo 
principal continua y termina si esperar la finalizacion de los hilos creados. Por eso en este caso el
tiempo es casi 0, ya que no espera el tiempo de dormir.

* Tercer caso
En este caso se declaran dos hilos como en el caso anterior pero se espera a que el  hilo 1 termine de 
ejecutar dormir para lanzar el hilo 2. Esto hace que pase un segundo por el primer hilo pero al lanzarse el
segundo hilo el hilo principal continua y termina, por eso es que el tiempo se acerca a 1 segundo.


- ¿Cuántos hilos o threads hay en cada caso?

* Primer caso
1 hilo, el principal.

* Segundo caso
3 hilos, el principal mas t1 y t2

* Tercer caso
3 hilos, el principal mas t1 y t2

- Los últimos dos ejemplos tienen la misma cantidad de threads cada uno, ¿cuál sería la diferencia entonces?
La difernecia es que en el ejemplo dos los hilos hilos t1 y t2 se ejecutan a la vez. Mientras que en 
el ejemplo 2 para la ejecucion del hilo t2 hay que esperar que termine el hilo t1.

- En el último ejemplo, ¿qué desventaja o desventajas le ve al uso del `join()`?
La ventaja con el uso del join es que si se precisa un resultado del hilo t1 para ejecutar el hilo t2 
se debe esperar que este termine. Ahora bien si no comparten el misme recurso no es correcto que un hilo 
espere al otro de forma secuencial.

# Muchos threads

En `muchosThreads.py` hay algunas cosas básicas de Python:
- `from tiempo import Contador` importa desde `tiempo.py` la clase `Contador`.
- Cómo crear una lista vacía.
- Cómo hacer un loop con cantidad de iteraciones fija.
- Cómo agregar elementos (al final) a una lista.
- Cómo hacer un loop que itere sobre una lista.

## Parte 1
Mirá el código y fijate de entender la sintaxis. 

## Parte 2
Ahora corré el script: ¿por qué tarda lo que tarda? 

* Tarda el tiempo que se setea a dormir los hilos


# Intercalación en concurrencia

**Dos reglas importantes** para `contadorConcurrente.py`:
- Mirá el código pero _no lo ejecutes_,
- Mirá el código pero _no lo ejecutes_.

(Referencia [The First Rule of Fight Club (1999)](https://www.youtube.com/watch?v=dC1yHLp9bWA))

Mirando el código de `contadorConcurrente.py`, pero sin ejecutarlo:
- Al ejecutar la función `cuenta()`, ¿cuántas veces se ejecuta el `for` que tiene adentro, y qué hace cada iteración del `for`?
El for se ejecuta (El valor seteado en la variable MAX_COUNT dividido la cantidad de la variable THREADS),
para el caso del ejemplo es 1000000/2 que da 500000. Lo que hace cada iteraccion es sumar uno a la variable
counter.

- ¿Es verdad que cada thread lanza una ejecución de la función `cuenta()`?
Si

- ¿Es verdad que se está esperando a que termine cada thread?
Si

- ¿Cúal te parece que es el valor que se imprime de `counter`?
1000000

Ahora corré `contadorConcurrente.py`:
- Correlo varias veces, ¿qué observás que pasa?
Que el valor de counter no llega a 1000000 y varia.

- ¿Por qué está pasando eso que observás?
Entiendo que se debe a que no llega a terminar la ejecucion del hilo 1 y como comparten el mismo recurso
comienza a sumar antes que llegue a 500000.

# ¿Secuencial clásico, concurrente o paralelo?

Para cada una de las siguiente situaciones, decidí si es secuencial clásico, concurrente o paralelo. Intentá justificar señalando las ideas esenciales de cada caso.

- Cuál persona de un total de 50 corre más rápido una maratón.
    - opción 1) Cada persona corre secuencialmente en la pista, y medimos cada tiempo.
    - opción 2) Todas las personas corren en la misma pista, y la que llega primero listo.
		- Preguntas: ¿hay algún recurso compartido? ¿genera problemas?
    Para la opción 1 no se comparte ningun recurso pero el tiempo que se llevará para controlar el tiempo
    sera alrededor de 50 veces mas que en la opcion 2 que corren todos juntos en la misma pista.
    En la opción dos el recurso compartido es la pista y cada corredor peleara por tener la mejor posición,
    y puede generar problemas de lugar en la pista.

    - opción 3) Cada persona corre en una pista distinta, todas al mismo tiempo.
		- Pregunta: ¿hay un aumento de recursos respecto al anterior?
    Si, la cantidad de pistas
    - Pregunta: ¿pros y contras de cada opción?
    En el caso de que todas las personas corran en una misma pista lucharan por el recurso de la pista
    para encontrarse en la primera posición. En el case que cada persona tenga una pista se tendran que poner una pista para cada corredor aumentando considerablemente el lugar donde se realizará la carrera.

- Competencia de triples en basquet: quién mete más en 10 intentos.
    - opción 1) Cada persona secuencialmente realiza 10 intentos, y anotamos la cantidad de triples.
    - opción 2) Todas las personas tiran los 10 intentos al mismo tiempo.
		- Preguntas: ¿hay algún recurso compartido? ¿genera problemas?
    El recurso compartido es el aro y generará problemas debido a que si dos pelotas al mismo tiempo intentan entrar puede que se bloqueen mutuamente.

    - opción 3) Cada persona tira en un aro distinto, todas al mismo tiempo.
    - Pregunta: ¿pros y contras de cada opción?
    pros: No existe un recurso compartido ya que cada persona tiene su propio aro.
    contra: se debe aumentar la cantidad de recursos a la cantidad de personas que realizarán la prueba.