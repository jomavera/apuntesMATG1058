# Fundamentos de Análisis Numérico

## Tipos de Métodos (algoritmos) Numéricos

- Podemos clasificarlos en dos:

  - Métodos Iterativos

    ```{figure} images/unidad1_metodo_iterativo.png
    ---
    width: 90%
    align: center
    name: metodo iterativo
    ---
    Gráfico dirigido de un método iterativo
    ```

  - Métodos Directos
    ```{figure} images/unidad1_metodo_directo.png
    ---
    width: 55%
    align: center
    name: metodo directo
    ---
    Gráfico dirigido de un método directo
    ```

## Análisis de algoritmos: iterativos

Es natural hablar de *convergencia* para los métodos iterativos

```{div} definicion
**Convergencia**

Puede definirse en terminos del límite de una sucecsión. Diremos que un algoritmo converge a $l$ si:

$$\lim_{n \to \infty} x^{(n)}= l$$

donde $x^{(n)}$ es la salida del algoritmo en la iteración $n$.
```

Por esto, dado un condicion de terminación que *trunca* el método dado como resultado el *error de truncamiento*


```{div} definicion
**Error de truncamiento**

El error de truncamiento en la iteración $n$ se define como:

$$E_n=|x^*-x^{(n)}|$$

donde $x^*$ es la solución y $x^{(n)}$ es la salida del algoritmo en la iteración $n$.
```

## Análisis de algoritmos: directos

En cambio, en los métodos directos en general se entrega una solucion exacta o aproximada.

```{div} definicion
**Error de redondeo**

El error de redondeo de un algoritmo se define como:

$$E = |x^* - \bar{x}|$$

donde $x^*$ es la solución y $\bar{x}$ es la salida del algoritmo
```

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

### El panorama general

**No** debemos preocuparnos por términos específicos, esto es, constantes y/o de orden inferior.

- *Manejabilidad*: Especificar las constantes y los términos de orden inferior necesitan un análisis mas detallado que en general no ayudarán a entender mejor el tiempo de convergencia.
- *Constantes dependen de capacidad computacional*: Segun lenguaje y  computadora usada cada flop puede tardar mas o menos cierto tiempo.

```{margin}
En la {numref}`Fig. {number} <panorama general>` podemos ver que las constantes y los términos de orden inferior tienen un peso importante cuando $x \to \infty$
```

```{figure} images/unidad1_panorama_gen.png
---
width: 80%
align: center
name: panorama general
---
Funciones para diferentes valores de $x$
```


### La asíntota

Queremos determinar la asíntota. Esto es que pasa con $T(x)$ cuando $x$ es muy grande.
¿$T(x)$? cuando $x \to \infty$

```{margin}
En la {numref}`Fig. {number} <asintota>` vemos que para $x$ pequeño $f(x)$ no resulta en una cota superior de $g(x)$.
```

```{figure} images/unidad1_asintota.png
---
width: 65%
align: center
name: asintota
---
Grafico de la función $g(x)$ y función que la acota $f(x)$
```

## Notación *Gran O*

Esta notación ayuda a caracterizar el crecimiento de una función. En este caso vamos a tratar con la función que caracteriza el numero de operaciones de un algoritmo. La  letra $O$ es usada porque se refiere al *orden* de la función. La notación provee una cota superior a una función mientras su argumento se acerque a algún valor.

```{div} definicion
**Notación Gran O**

$T(n) = O(f(n))$ si y solo si $T(n)$ es eventualmente acotada superiormente por un múltiplo constante de $f(n)$. Esto es, para constantes positivos $c$ y $n_0$ se cumple

$$ T(n) \leq c \cdot f(n)$$

para todo $n \geq n_0$
```

$T(n)$ es el tiempo de convergencia del peor de los escenarios y $f(n)$ es una función “canónica”, e.g., $n$, $\log n$, $n^2$.

En esta notacion, el simbolo “=” no se usa en sentido estricto. Por ejemplo, $x^3=O(x^3)$ y $2x^3+x=O(x^3)$, pero claro $x^3 \neq 2x^3+x$.

Por ejemplo, polinomios de grado $k$ son $O(n^k)$. 
Un ejemplo especifico es: si tenemos un algoritmo cuyo tiempo de convergencia es $T(n) = 10n5+3n3+n$ entonces ¿Cuál es $f(n)$ tal que $T(n)=O(f(n))$?

```{margin}
Si escojo $f(x)=x^3$ entonces $n_0=15$ y $c=6$ cumplen con $T(x)= c \cdot f(x)$
```

```{figure} images/unidad1_gran_o_ej.png
---
width: 80%
align: center
name: gran o ejemplo
---
Ejemplo de función que acota a $T(x)$
```


## Orden de convergencia para métodos iterativos

Supongamos que tengamos una secuencia que $\{x^{(n)}\}_{n=0}^{\infty}$ a $x^*$, con $x^*$ con $x^{(n)} \neq x^*$ para todo $x^{(n)}$. Si existen constantes positivas $\lambda$ y $\alpha$ con

```{math}
:label: orden de convergencia
\lim_{n \to infty} \frac{|x^{(n+1)}-x^*|}{|x^{(n)}-x^*|^{\alpha}}=\lambda
```

entonces $\{x^{(n)}\}_{n=0}^{\infty}$ converge a $x^*$ en orden $\alpha$ con error constante asintótico $\lambda$.

- Un algoritmo de mayor orden de convergencia $\to$ más rápido.

- $\lambda$ afecta la velocidad de convergencia pero $\alpha$ predomina.

- Métodos en este curso se caracterizan de la siguiente manera:
    - Si $\alpha=1$ y $0< \lambda < 1$ la secuencia es **linealmente convergente**
    - Si $\alpha=1$ y $\lambda=0$ es **superlinealmente convergente**
    - Si $\alpha=1$ y $\lambda=1$ es **sublinealmente convergente**
    - Si $\alpha=2$, la secuencia es **cuadráticamente convergente**
