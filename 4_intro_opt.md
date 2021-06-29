# Conceptos Básicos de Optimización No Lineal

En optimización no lineal sin restricciones consideramos el problema:

$$\begin{gather*}
\min f(\textbf{x})\\
\text{sujeto a } \textbf{x} \in \mathbb{R}^n
\end{gather*}$$

asumineo que $f$ es una función continuamente diferenciable.

## Optimalidad

En general, vamos a utilizar el sentido de minimización. En este sentido se puede definir dos tipos de mínimos:

```{div} definicion
**Mínimo local sin restricciones**

Un vector $\textbf{x}^*$ es un mínimo local sin restricciones de $f$ si no es peor que sus vecinos; esto es, si existe un $\varepsilon >0$ tal que 

$$f(x^*) \leq f(\textbf{x}), \hspace{.4cm} \forall \textbf{x} \text{ con } \|\textbf{x}-\textbf{x^*} \| < \varepsilon$$
```

```{div} definicion
**Mínimo global sin restricciones**

Un vector $\textbf{x}^*$ es un mínimo global sin restricciones de $f$ si no es peor que ningún vector; esto es,

$$f(\textbf{x}^*) \leq f(\textbf{x}), \hspace{0.4cm} \forall \textbf{x}\in \mathbb{R}^n$$
```

```{figure} images/unidad_4_min_global_local_bg.png
---
width: 40%
align: center
name: min global y local de una función
---
Mínimo global y local de una función
```
### Existencia de solución optima

Aun asi una función  esta inferiormente acotada, no siempre existe un mínimo global pero si tiene un ínfimo como se indica en la siguiente definición.

```{div} definicion
**Ínfimo, Supremo**

Para una función $F:X \to \mathbb{R}$, su mayor cota inferior es llamdo el ínfimo y es denotado como $\inf_{x \in X} f(x)$. Similarmente, su menor cota superior es llamado supremo y es denotado por $\sup_{x \in X} f(x)$
```
Si $f$ no esta acotada inferiormente o superiormente, entonces $\inf_{x \in X} f(x)=-\infty$ o $\sup_{x \in X} f(x)=+\infty$, respectivamente.

Verificar si una función tiene una solución óptima global es difícil en general. Existen ciertos tipos de funciones donde se pueden garantizar la existencia de una solución óptima global.

```{margin}
Este teorema nos indica que siempre y cuando una función sea continua en un conjunto **cerrado** y **acotado**, esta función tendrá un mínimo global en dicho espacio.
```

```{div} definicion
**Teorema Weierstrass**

Los problemas $\min_{x \in X} f(x)$ y $\max_{x \in X} f(x)$, donde $X \subseteq \mathbb{R}^n$ es un conjunto compacto y $f: X \to \mathbb{R}$ es una función continua, tiene soluciones óptimas globales.
```

## Problemas convexos

Dado a la estructura especial de los problemas convexos son un tipo importante de problemas dentro de la optimización.

```{div} definicion
**Problema convexo**

Un problema $\min_{x \in X}f(x)$ es llamado un problema de minimización
convexa si $f$ es una función convexa y $X$ es un conjunto convexo.
```

### Conjuntos convexos
Un conjunto $C$ es convexo si la línea entre cualquier dos puntos de $C$ se encuentra en $C$

```{div} definicion
**Conjunto convexo**

Un conjunto $X \subseteq \mathbb{R}^n$ se dice que es convexo para cualquier $x, y \in X$ y cualquier $\alpha \in (0,1)$ entonces $\alpha \cdot \textbf{x} + (1-\alpha )\cdot \textbf{y} \in X$
```

```{figure} images/unidad_4_conjuntos_convexos_bg.png
---
width: 60%
align: center
name: conjunto convexo y no convexo
---
Conjuntos convexo y no convexo
```

#### Ejemplos

- Una **línea** es convexa

- Los **conjuntos afines** son convexos. 

```{div} definicion
**Conjunto afín**

Un conjunto $C \subseteq \mathbb{R}^n$ es afín si la línea que atraviesa cualquier dos puntos en $C$ se encuentra en $C$, esto es, para cualquier $\textbf{x}_1, \textbf{x}_2 \in C$ y $\theta \in \mathbb{R}$ se cumple $\theta \textbf{x}_1 + (1-\theta)\textbf{x}_2 \in C$.
```

- Los **hiperplanos** $\{\textbf{x}| \textbf{a}^T\textbf{x} = b\}$ son conjuntos convexos.

- Los **semiespacios** $\{\textbf{x} | \textbf{a}^T\textbf{x} \leq b \}$, $\{\textbf{x} | \textbf{a}^T\textbf{x} \geq b \}$ son convexos.

- Sea $f$ un función convexa y $C$ un conjunto convexo entonces los conjuntos de nivel $\{\textbf{x} \in C | f(\textbf{x}) \leq \alpha \}$ son convexos para todos los escalares $\alpha$.

### Operaciones que preservan la convexidad

Conocer estas operaciones nos permite identificar conjuntos que a primera vista no podriamos determinar si son convexos.

- **Intersección**: Si $S_1$ y $S_2$ son convexos, entonces $S_1 \cap S_2$ es convexo

- **Funciones afines**: Una función $f$ es afín si es la suma de una función lineal y una constante, esto es, la forma $f(\textbf{x})=A\textbf{x}+\textbf{b}$ donde $A \in \mathbb{R}^{m \times n}$ y $\textbf{b} \in \mathbb{R}^m$. Suponga que $S \subseteq \mathbb{R}^n$ es convexo y $f: \mathbb{R}^n \to \mathbb{R}^m$ es un función afín. Entonces la imagen de $S$ debajo de $f$,

$$f(S) = \{f(\textbf{x}) | \textbf{x} \in S\}$$

es convexo.
- El conjunto de elementos que resultan de la suma de los elementos de dos conjuntos convexos $\{\textbf{x}_1 + \textbf{x}_2 | \textbf{x}_1 \in C_1, \textbf{x}_2 \in C_2\}$ es convexo.

### Funciones convexas

```{div} definicion
**Función convexa**

Dado un conjunto convexo $X \subseteq \mathbb{R}^n$, una función $f: X \to \mathbb{R}$ es convexa si 

$$f(\alpha \cdot \textbf{x} + (1-\alpha)\textbf{y}) \leq \alpha f(\textbf{x}) + (1-\alpha)\textbf{y} \hspace{1cm} \forall \textbf{x}, \textbf{y} \in X, \alpha \in (0,1)$$
```

```{figure} images/unidad_4_grafico_funcion_convexa_bg.png
---
width: 80%
align: center
name: funciones convexas y no convexas
---
Funciones convexa y no convexa
```


Otra manera de caracterizar las funciones convexas es con su epigrafo

```{div} definicion
El epigrafo de una función es el conjunto que se encuentra por **encima** de la función, i.e., si $C$ es un subconjunto de $\mathbb{R}^n$, y una función $f: C \to \mathbb{R}$, entonces el epigrafo de $f$ es:

$$\text{epi}(f) = \{(\textbf{x},z) | \textbf{x} \in \mathbb{R}^n, z \in \mathbb{R}, f(\textbf{x}) \leq z  \}$$
```

```{figure} images/unidad_4_epigrafo_funcion_convexa_bg.png
---
width: 80%
align: center
name: epigrafo
---
Epigrafo de funciones convexa y no convexa
```

#### Transformaciones lineales y afines

```{margin}
Una aplicación lineal puede ser representada por una matriz $m \times n$, esto es, $L(\textbf{x})=M\cdot \textbf{x}$
```

Una **aplicación (o transformación) lineal** $L: \mathbb{R}^n \to \mathbb{R}^m$ satisface:
- $L(\textbf{x}+\textbf{y}) = L(\textbf{x}) + L(\textbf{y})$
- $\alpha \cdot L(\textbf{x}) = L(\alpha \cdot \textbf{x})$ para una escalar $\alpha$

Una **aplicación o función afín** es una aplicación lineal mas una variación del origen. Tiene la forma de $f(\textbf{x})=M\textbf{x}+d$, donde $d \in \mathbb{R}^m$ 

```{div} definicion
**Lema**

Una función afín (y funciones lineales) son convexas y concavas
```

#### Operaciones que preservan la convexidad

- Para $C$ un conjunto convexo y cualquier colección $f_i: C \to \mathbb{R} | i \in \mathcal{J}$ de funciones convexas, una suma ponderada no negativa, esto es, $f=\sum_{i \in \mathcal{J}} w_i \cdot f_i$, donde $w_i \geq 0$, es convexa.

- Para un conjunto de indices $\mathcal{J}$, un conjunto convexo $C$, y $f_i:C \to \mathbb{R}$, una función convexa $\forall i\in mathcal{J}$, la función $h: C \to \mathbb{R}$ definida por $h(x) = \max_{i \in \mathcal{J}} f_i(x)$ es convexa

- Para un conjunto convexo $C \subseteq \mathbb{R}^n$, $f: C \to \mathbb{R}^m$ un conjunto convexo, y $g: \mathbb{R}^m \to \mathbb{R}$ una función convexa no decreciente, la función $h:C \to \mathbb{R}$ definida por $h(x)=g(f(x))$ es convexa.

#### Caracterización de funciones convexas

- **Primer orden:** Sea $C \subseteq \mathbb{R}^n$ un conjunto convexo y $f:C \to \mathbb{R}$ sea una función diferenciable sobre $C$.

    - La función $f$ es convexa si y solo si:

    $$f(y) \geq f(x)+\nabla^Tf(x)(y-x), \hspace{1cm} \forall x, y \in C$$
    - Si la desigualdad es estricta $\forall x \neq y$, entonces $f$ es estrictamtente convexa.

- **Segundo orden:** Sea $C \subseteq \mathbb{R}^n$ un conjunto convexo y $f: C \to \mathbb{R}$ sea dos veces continuamente diferenciable sobre $C$.

    - Si $f$ es convexa en $C$ y $C$ tiene un punto inferior, entonces $\nabla^2 f(x)$ es semidefinida positiva en todo $x \in C$.
    - Si $\nabla^2 f(x)$ es semidefinida positiva para todo $x \in C$, entonces $f$ es convexa en $C$
    - Si $\nabla^2 f(x)$ es definida positiva para todo $x \in C$, entonces $f$ es estrictamente convexa.

### Optimalidad de un problema convexo
```{margin}
Este teorema es evidente por la caracterización de segundo orden de una función convexa. Esta indica que la funcion tendra la forma de un *tazón.*
```

```{div} definicion
**Teorema**

Cualquier mínimo de un problema convexo es un mínimo global
```

## Condiciones necesarias de optimalidad

```{margin}
Estas aproximaciones nos permiten explorar el vecindario de vectores sin evaluar explicimente las funciones.
```
Si la función de costo es diferenciable, podemos usar el gradiente y el polinomio de Taylor para comparar el costo de un vector con los vector vecinos. En particular, consideremos pequeñas variaciones $\Delta \textbf{x}$ para un vector $\textbf{x}^*$ que aproximadamente da en primer orden una variación del costo

$$f(\textbf{x}^* + \Delta \textbf{x}) - f(\textbf{x}) \approx \nabla f(\textbf{x}^*)^T \cdot \Delta \textbf{x}$$

y en segundo orden da una variación del costo 

$$f(\textbf{x}^*+\Delta \textbf{x}) - f(\textbf{x}) \approx \nabla f(\textbf{x}^*) \cdot \Delta \textbf{x} + \frac{1}{2} \Delta \textbf{x}^T \cdot \nabla^2 f(\textbf{x}^*) \cdot \Delta \textbf{x}$$


Se espera que si $\textbf{x}^*$ es un mínimo local sin restricciones, la variación del costo de primer orden debido a pequeñas variaciones $\Delta \textbf{x}$ es no negativa.

$$\nabla f(\textbf{x}^*)^T \cdot \Delta \textbf{x} = \sum_{i=1}^{n} \frac{\partial f(\textbf{x}^*)}{\partial x_i}\cdot x_i \geq 0$$

En particular, si usamos $\Delta \textbf{x}$ con los valores positivos y negativos del vector unitario, obtenemos las condiciones $\frac{\partial f (\textbf{x}^*)}{\partial x_i} \geq 0$ y $\frac{\partial f(\textbf{x}^*)}{\partial x_i} \leq 0$ entonces denominamos la **condición necesaria de primer orden**, como
```{margin}
Todo *punto crítico* cumple la condición necesaria de primer orden. Un *punto de silla* es critico pero no es un mínimo. Por eso, la condición de primer orden es necesaria pero no suficiente.
```

```{math}
:label: fonc
\nabla f(\textbf{x}^*) = \textbf{0}
```

También esperamos de la variaci\'on de costo de segundo orden que sea no negativa:

$$\nabla f(\textbf{x}^*)^T \cdot \Delta \textbf{x} + \frac{1}{2} \cdot \Delta \textbf{x}^T \cdot \Delta^2 f(\textbf{x}^*) \cdot \Delta \textbf{x} \geq 0$$

ya que $\nabla f(\textbf{x}^*)^T \cdot \Delta \textbf{x} = 0$, obtenemos

$$\Delta \textbf{x}^T \cdot \nabla^2f(\textbf{x}^*) \cdot \Delta \textbf{x} \geq 0,$$

implica la **condición necesaria de segundo orden**,

```{math}
:label: sonc
\nabla^2 f(\textbf{x}^*): \text{es definida semipositiva}
```

## Condiciones suficientes de optimalidad

Suponga que tenemos un vector $\textbf{x}^*$ que satisface la condición de necesaria de primer orden {eq}`fonc`
y que

```{math}
:label: sosc
\nabla^2 f(\textbf{x}^*): \text{es definida positiva},
```

entonces para todo $\Delta \neq 0$ tenemos que

$$\Delta^T \cdot \nabla^2 f(\textbf{x})\cdot \Delta \textbf{x} > 0$$

Esto implica que $f$ aumenta estrictamente a pequeñas variaciones de $\textbf{x}^*$. Para una función doblemente diferenciable, se garantiza que una solución es un mínimo local si {eq}`fonc` y {eq}`sosc` se satifacen. Colectivamente estas condiciones son llamadas *condiciones suficientes de optimalidad de segundo orden*.
