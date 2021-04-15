# Fundamentos de Análisis Numerico

## Tipos de Métodos (algoritmos) Numéricos

- Podemos clasificarlos en dos:

  - Métodos Iterativos

  ![metodo iterativo](images/unidad1_metodo_iterativo.png)

  - Métodos Directos

  ![metodo directo](images/unidad1_metodo_directo.png)

## Análisis de algoritmos: iterativos

Es natural hablar de *convergencia* para los métodos iterativos

Convergencia
: Puede definirse en terminos del límite de una sucecsión. Diremos que un algoritmo converge a $l$ si:

    $$\lim_{n \to \infty} x^{(n)}= l$$

    donde $x^{(n)}$ es la salida del algoritmo en la iteración $n$.

Por esto, dado un condicion de terminación que *trunca* el método dado como resultado el *error de truncamiento*

Error de truncamiento
: El errro de truncamiento en la iteración $n$ se define como:

    $$E_n=|x^*-x^{(n)}|$$

    donde $x^*$ es la solución y $x^{(n)}$ es la salida del algoritmo en la iteración $n$.

## Análisis de algoritmos: directos

En cambio, en los métodos directos en general se entrega una solucion exacta o aproximada.

Error de redondeo
: El error de redondeo de un algoritmo se define como:

    $$E = |x^* - \bar{x}|$$

    donde $x^*$ es la solución y $\bar{x}$ es la salida del algoritmo


## Análisis asintótico

Vamos a ver uan serie de algoritmos y debemos poder decir que tan *rapido* es el método o que número de operaciones aproximadamente realizara.

Queremos determinar una función $T(x): \mathbb{N} \to \mathbb{R}$ donde $x$ es un número natural que indica el tamaño del problema y $T(x)$ es un número real que se refiere al tiempo de convergencia/número de operaciones.

Para el análisis debemos decidir entre mayor **exactitud** o mayor **manejabilidad**. Para determinar esta función tratamos en:

- Enfocarnos en el peor caso
- Entender el panorama general
- Análisis asintotico 

### El *peor caso*

Ciertos algoritmos tiene diferentes tiempos de convergencia dependiendo de la entrada (e.g. solución inicial). Nos interesa saber que ocurre en el peor caso, no en el mejor de los casos. ¿Por que?

Queremos garantizar una acota superior del tiempo de convergencia. Esta acota se cumple para cualquier solución inicial y de cualquier suposición.




