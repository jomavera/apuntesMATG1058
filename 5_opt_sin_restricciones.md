# Optimización sin Restricciones

## Problemas de optimización univariante

Considerando una función $f : \mathbb{R} \to \mathbb{R}$ que tiene un único mínimo $c$ en un intervalo cerrado $[a,b]$. Además, $f$ es una función estrictamente decreciente en $[a,c]$ y estrictamente creciente en $[c, b]$. Funciones de este tipo son llamadas *unimodales*.

### Búsqueda de la sección dorada

Se busca reducir el espacio de búsqueda al localizar un intervalo mas pequeño donde se encuentra el mínimo. Digamos que quiero "probar" dos puntos $c$ y $d$ en el intervalo $l = [a, b]$. Si escojo un valor $\rho < 1/2$ que representa la fracción de $l$. De tal manera, que si exploro dos puntos $c=a + \rho \cdot l$ o $d = b - \rho \cdot l$, y efectivamente $x^* \in [c, b]$ o $x^* \in [a, d]$, respectivamente, entonces he reducido la incertidumbre en un factor de $(1 - \rho)$. ¿Cuál debe ser el valor de $\rho$ de tal manera que siempre se reduzaca la misma proporción? 


Consideremos el siguiente ejemplo con intervalo inicial $l=[a_0, b_0]$:

```{figure} images/golden_search_example-removebg.png
---
width: 50%
align: center
name: ej golden search
---
Ejemplo
```

donde los puntos interiores del intervalos son $a_1, b_1$  se determinan de la siguiente manera $a_1 - a_0 = b_0 - b_1 =\rho \cdot (b_0 - a_0)$. En este ejemplo, $f(a_1) < f(b_1)$ entonces es apropiado reducir la siguiente búsqueda en el intervalo $d=[a_0, b_1]$. El intervalo original se reduce en $(1-\rho)$,

$$d = (1-\rho)\cdot l$$
o expresado en otra manera,
```{math}
:label: igualdad 1
l = \frac{d}{1-\rho}
```

Si queremos que uno de los nuevos puntos interiores sea el ya evaluado $a_1$ para solo evaluar la función en un solo nuevo punto entonces se tiene que cumplir que $[a_0, a_1] = [a_0, b_2]$. Esta igual se la puede expresar como,

```{math}
:label: igualdad 2
\rho \cdot l = (1-\rho) \cdot d
```

Si reemplazamos {eq}`igualdad 1` en {eq}`igualdad 2` entonces nos queda la siguiente expresion

```{math}
:label: igualdad 3
\frac{\rho}{1-\rho}=1-\rho
```

Para ver que significa {eq}`igualdad 3` partamos de la definicion del número áureo:

> La suma de los dos segmentos $a$ y $b$ es al segmento mayor $a$, lo que este segmento mayor $a$ es al segmento menor $b$

La ecuación que describe esto es

```{math}
:label: numero aureo
\frac{a+b}{a}=\frac{a}{b}
```
y esta proporción es el número áureo

$$\frac{a}{b} = \varphi \approx 1.61803$$

Suponiendo que $\rho < 1/2$ entonces podemos considerar que $a=1-\rho$ y $b=\rho$. Entonces {eq}`numero aureo` queda expresado en esta manera,

```{math}
:label: numero aureo 2
\frac{1}{1-\rho}=\frac{1-\rho}{\rho}
```
{eq}`numero aureo 2` nos indica que $1-\rho = \frac{1}{\varphi}$, y esta es la razón del nombre del método. De esta manera, reducimos el intervalo de búsqueda en un factor de $1 - \rho \approx 0.618$ en cada interación.

#### Pseudocódigo

```{figure} images/unidad_5_golden_search.PNG
---
width: 80%
align: center
name: pseudocogio golden search
---
Pseudocódigo búsqueda de la sección dorada
```

### Búsqueda de Fibonacci

Consideremos el factor $\rho_t$ cambia en cada iteración $t$. Al igual en la búsqueda de la sección dorada solo queremos que en cada iteración solo se requiera una nueva evaluación de la función. Entonces según {eq}`igualdad 3`

```{math}
:label: restriccion fibonacci
\rho_t = 1 - \frac{\rho_t}{1-\rho_t}, \hspace{.4cm} t=1,...,n-1
```

Para minimizar el intervalo de incertidumbre en $n$ pasos se plantea el siguiente problema de minimización.

```{math}
:label: problema min fibonacci
\begin{aligned}
\min \hspace{.2cm} (1-\rho_1)\cdot (1-\rho_2) \cdots (1-\rho_n)\\
\text{s.a.}\quad \rho_t = 1 - \frac{\rho_t}{1-\rho_t}, & \hspace{.4cm}  t=1,...,n-1\\
0 \leq \rho_1 \leq \frac{1}{2}, & \hspace{.4cm} t=1,...,n
\end{aligned}
```

```{div} definicion
**Teorema**

La solución óptima del problema {eq}`problema min fibonacci` esta dada por

$$\rho_t = 1 - \frac{F_{n-t+1}}{F_{n-t+2}}, \hspace{.4cm} t=1,...,n$$

donde $F_n$ es el $n^{avo}$ elemento de la secuencia de Fibonacci.
```

Esta ecuación indica que en cada iteración $t$ el intervalo se reduce en $\frac{F_{n-t+1}}{F_{n-t+2}}$. Si realizamos $n$ iteraciones de la búsqueda de Fibonacci reducimos el intervalo inicial en un factor de $F_{n+1}$.

#### Pseudocódigo

```{figure} images/unidad_5_fibonacci_search.PNG
---
width: 80%
align: center
name: pseudocogio fibonacci search
---
Pseudocódigo búsqueda de Fibonacci
```

## Algoritmos de Busqueda Lineal

Dado el problema 

$$\min f(\textbf{x})$$

Los algoritmos clásicos para problemas de optimización sin restricciones usualmente construyen una secuencia de puntos $\{\textbf{x}^{(k)}: k \geq 0 \}$, tal que $\textbf{x}^{(k)} \to \textbf{x}^{*}$, $k \to \infty$, donde $\nabla f(\textbf{x}^{*})=\textbf{0}$.

Cada punto de la secuencia es obtenida del punto anterior moviéndose una distancia a lo largo de la dirección $\textbf{p}^{(k)}$:

$$\textbf{x}^{(k+1)} = \textbf{x}^{(k)} + \alpha^{(k)} \cdot \textbf{p}^{(k)}$$

En cada iteración $k$, dado el punto $\textbf{x}^{(k)}$ se escoge una dirección $\textbf{p}^{(k)}$. La dirección $\textbf{p}^{(k)}$ es seleccionada basado en:
- Métodos de primer orden: gradient $\nabla f(\textbf{x}^{(k)})$
- Métodos de primer orden: hessiana $\nabla^2 f(\textbf{x}^{(k)})$

A lo largo de esta dirección se busca una nueva solución con un mejor valor de la función. La longitud de paso se puede determinar resolviendo de manera aproximada (o exacta) el problema unidimensional:

$$\min_{\alpha \geq 0} f(\textbf{x}^{(k)} + \alpha \cdot \textbf{p}^{(k)} )$$

### Método de Descenso de Gradiente

Es un método de búsqueda lineal que se mueve a lo largo de la dirección $\textbf{p}^{(k)} = - \nabla f(\textbf{x}^{(k)})$ en cada paso. Esta dirección es donde la función decrece mas rápidamente.

#### Pseudocódigo

```{figure} images/unidad_5_gradient_descent.PNG
---
width: 80%
align: center
name: pseudocogio gradient descent
---
Método de Descenso de Gradiente
```

### Método de Gradiente Conjugado

Si partimos de la idea de optimizar una función cuadrática de la siguiente forma

$$\min_{\textbf{x}} f(\textbf{x}) = \frac{1}{2} \textbf{x}^T A \textbf{x} + \textbf{b}^T\textbf{x} + c$$

entonces $A$ es simétrica y positiva definida por ende la función tiene un único mínimo local. El método de Gradiente Conjugado utiliza direcciones mutuamente conjugados con respecto a $A$:

$$\textbf{p}_{(i)}^T \cdot A \cdot \textbf{p}_{(j)} = 0 \text{ para todo } i \neq j$$

El algoritmo empieza con la dirección de descenso de gradiente:

$$\textbf{x}^{(0)} = - \nabla f(\textbf{x}^{(0)})$$

En los pasos sucesivos se escoge la dirección basados en el gradiente evaluado en el siguiente punto y en la dirección pasada:

$$\textbf{p}^{(k+1)} = - \nabla f(\textbf{x}^{(k+1)}) + \beta^{(k)}\cdot \textbf{p}^{(k)}$$

Se puede determinar $\beta$ para un $A$ conocido, y partiendo del hecho que $\textbf{p}^{(k+1)}$ es conjugado de $\textbf{(k)}$:

$$\textbf{p}^{(k+1)T} \cdot A \cdot \textbf{p}^{(k)} = 0$$

$$\big( - \nabla f(\textbf{x}^{(k+1)}) + \beta^{(k)}\cdot \textbf{p}^{(k)} \big)^T \cdot A \cdot \textbf{p}^{(k)} = 0$$

$$ \beta^{(k)} = \frac{\nabla f(\textbf{x}^{(k+1)})^T\cdot A \cdot \textbf{p}^{(k)}}{\textbf{p}^{(k)T} \cdot A \cdot \textbf{p}^{(k)} }$$

Este método tambien puede ser aplicado a funciones no cuadráticas. Funciones suaves continuas se comportan como funciones cuadráticas en áreas cercanas al mínimo local. En estos casos el método converge muy rápido. En general, en estos casos no sabemos que matriz $A$ me permite aproximar a una función cuadrática. Existen varias opciones que tienden a funcionar bien para aproximar $\beta^{(k)}$:

- Fletcher-Reeves:


$$\beta^{(k)} = \frac{\nabla f(\textbf{x}^{(k)})^T \cdot \nabla f(\textbf{x}^{(k)})  }{ \nabla f(\textbf{x}^{(k-1)})^T \cdot \nabla f(\textbf{x}^{(k-1)}) }$$

- Polak-Ribiere:


$$\beta^{(k)} = \frac{\nabla f(\textbf{x}^{(k)})^T \cdot (\nabla f(\textbf{x}^{(k)}) - \nabla f(\textbf{x}^{(k-1)}) ) }{ \nabla f(\textbf{x}^{(k-1)})^T \cdot \nabla f(\textbf{x}^{(k-1)}) }$$

#### Pseudocódigo

```{figure} images/unidad_5_conjugate_gradient.PNG
---
width: 80%
align: center
name: pseudocogio conjugate gradient
---
Método de Gradiente Conjugado
```

### Calculo de longitud de paso

Para métodos de busqueda lineal es necesario determinar la longitud de paso $\alpha$. Esto es difícil para funciones no lineales. Además, nos enfrentamos a un trade-off. Queremos que el paso haga una reducción considerable al valor de la función $f$ pero al mismo tiempo que no tome demasiado tiempo en determinarlo. Los algoritmos para determinar la longitud de paso prueban una secuencia de candidatos de $\alpha$. Se escoge el $\alpha$ que cumple cierta condición. 

#### Backtracking

Una estrategia para determinar la longitud de paso es usar retroceso. Partimos con un $\alpha_0$ y lo disminuimos por un factor $\tau$ hasta encontrar un mejor valor de $f$.

```{figure} images/unidad_5_retroceso.PNG
---
width: 80%
align: center
name: retroceso
---
Backtracking para cálculo de longitud de paso
```


#### Condiciones de Wolfe
Las condiciones de Wolfe son las mas utilizadas y son las condiciones que se explican a continuación:

- **Condicion de Armijo**

Esta condición estipula que $\alpha^{(k)}$ debe dar un disminución suficiente en la función objetivo

$$f(\textbf{x}^{(k)} + \alpha \textbf{p}^{(k)}) \leq f(\textbf{x}^{(k)}) + c_1 \alpha \nabla f(\textbf{x}^{(k)})^T \cdot \textbf{p}^{(k)}$$

para una constante $c_1 \in (0,1)$. Si denotamos $l(\alpha) = c_1  \alpha \nabla f(\textbf{x}^{(k)})^T \cdot \textbf{p}^{(k)}$, esta función es un recta con pendiente negativa.

- **Condicion de Curvatura**

La condición de Armijo no es suficiente ya que se cumple para cualquier $\alpha$ pequeño. Para descartar pasos pequeños usamos la condición de curvatura


$$\nabla f(\textbf{x}^{(k)} + \alpha \textbf{p}^{(k)}) \geq c_2 \nabla f(\textbf{x}^{(k)})^T \cdot \textbf{p}^{(k)}$$

para alguna constante $c_2 \in (c_1, 1)$

Si combinamos la condición de Armijo con el procedimiento de retroceso podemos dispensar de la condición de curvatura y solo usar la condición suficiente de disminución para terminar el procedimiento de búsqueda lineal. Este procedimiento se muestra en el pseudocódigo a continuación:


```{figure} images/unidad_5_retroceso_armijo.PNG
---
width: 80%
align: center
name: armijo retroceso
---
Condicion de Armijo con backtracking para cálculo de longitud de paso
```

### Método de Newton

 Partiendo de las condiciones de optimalidad, un punto $\textbf{x}^* \in \mathbb{R^n$ es mínimo local si $\nabla f (\textbf{x}^*) = 0$. Entonces, dado un punto $\textbf{x} \in \mathbb{R}^n$ para el cual $\nabla^2 f (\textbf{x})$ es no singular, la siguiente solución es

 $$\textbf{x}^{(k+1)} = \textbf{x}^{(k)} - \big[\nabla^2 f (\textbf{x}^{(k)}) \big]^{-1} \nabla f (\textbf{x}^{(k)})$$


Este método puede ser visto como el método de descenso de gradiente pero usando la inversa de la hessiana para escalar el paso. La hessiana es definida positiva para todo $k$ entonces tenemos una dirección de descenso. Para determinar la inversa de la hessiana se puede resolver el siguiente sistema de ecuaciones:

$$\nabla^2 f (\textbf{x}^{(k)}) \cdot \textbf{p}^{(k)} = - \nabla f (\textbf{x}^{(k)})$$

#### Convergencia

Suponga que $f$ es doblemente diferenciable y la hessiana $\nabla^2 f(\textbf{x})$ es Lipschitz continua en un vecindario de $\textbf{x}^*$ en donde las condiciones suficientes de segundo orden son satisfechas. Considere que el paso $\textbf{x}^{(k+1)} = \textbf{x}^{(k)} + \textbf{p}^{(k)}$, donde $\textbf{p}^{(k)}$ es dado por el método de Newton. Entonces:

1. Si el punto inicial $\textbf{x}^{(0)}$  es suficientemente cerca de $\textbf{x}^*$, la secuencia de pasos converge a$\textbf{x}^*$

2. La tasa de convergencia de $\{\textbf{x}^{(k)} \}_{k=0}^{\infty} $ es cuadrática

3. La secuencia de las normas del gradientes $\{\|\nabla f( \textbf{x}^{(k)} ) \| \}_{k=0}^{\infty} $ converge cuadráticamente a cero.

#### Pseudocódigo

```{figure} images/unidad_5_newton.PNG
---
width: 80%
align: center
name: newton
---
Método de Newton
```

### Método de Newton con Modificación de Hessiana

Para puntos alejados de la solución puede ocurrir que la matriz Hessiana $\nabla^2 f(\textbf{x})$ puede no ser definida positiva, así que la dirección $\textbf{p}^{(k)}$ no necesarimente es una dirección de descenso. En ese caso, se modifica la hessiana con una aproximación que sea definida positiva. La hessiana modificada se obtiene añadiendo una matriz diagonal positiva o añadiendo una matriz de rango completo a la hessiana verdadera $\nabla^2 f(\textbf{x}^{(k)})$. De esta manera, se reemplaza la hessiana por $B^{(k)}$ tal que

$$B^{(k)} = \nabla^2 f(\textbf{x}^{(k)}) + E^{(k)}$$

Un enfoque para modificar la hessiana es mediante la factorización de Cholesky modificada. Se factoriza $\nabla^2 f(\textbf{x}^{(k)})$ pero se incrementa los elementos diagonales, encontrados durante la factorización, para asegurarse que son los suficientemente positivos. Este método garantiza que la factorización exista y que esta acotado relativamente a la norma de la hessiana.

#### Factorización de Cholesky Modificada - $LDL^T$

La factorización de Cholesky se puede expresar como 
$A = LDL^T$
donde $L$ es una matriz triangular inferior con elementos unitarios en su diagonal y $D$ es una matriz diagonal con elementos positivos. Si $A$ es indefinida, la factorización puede no existir. Una estrategia es computar $LDL^T$ y modificar los elementos de $D$ tal que sean los suficientemente positivos procurando que los elementos de $D$ y $L$ no sean muy grandes. Para controlar esto, se introduce dos parámetros $\delta$ y $\beta$.

En este método se requiere que en cada iteración para calcular la $j^{va}$ columna de $L$ y $D$ se satisfaga las siguientes cotas:

$$d_j \geq \delta, \hspace{2cm} |m_{i, j} | \leq \beta,\hspace{2cm} i=j+1, j+2, ... , n$$

donde $m_{i, j} = l_{i, j} \sqrt(d_j)$. Entonces para calcular las diagonales de $D$ es

$$d_j = \max \bigg( |c_{i, j} |, \bigg(\frac{\theta_j}{\beta}\bigg)^2, \delta \bigg) \hspace{0.5cm} \text{con } \theta_j= \max_{j < i \leq n} |c_{i, j} | $$

donde $c_{i, j} = a_{i, j} - \sum_{s=1}^{j-1} d_s l_{i, s} l_{j, s}$

##### Pseudocódigo

```{figure} images/unidad_5_cholesly_LDL.PNG
---
width: 80%
align: center
name: cholesky ldl
---
Factorización Cholesky Modificada
```

#### Factorización de Cholesky Modificada - $LL^T$

Si planteamos la factorización como 

$$A = L \cdot L^T$$

en este caso $L$ no necesariamente tiene una diagonal con elementos iguales a uno. Si la matriz $A$ no es definida positiva se podría incrementar los elementos diagonales. Esto es aplicado secuencialmente en el proceso de factorización obteniendo 

$$ L^{(k)}\cdot L^{(k)^T} = \nabla^2 f(\textbf{x}^{(k)}) + \Delta^{(k)} $$

donde $\Delta^{(k)}$ es diagonal.

El método consiste en introducir secuencialmente los elementos de $\Delta^{(k)}$ durante la factorización que se encuentra los valores de las diagonales, que pueden ser negativas o cercanas a cero indicando que $A$ no es definida positiva o casi singular.

Se deben escoger los valores $\mu_1$ y $\mu_2$ tal que $\mu_1 < \mu_2$. El algoritmo consiste en lo siguiente:

1. Determinar los elementos de la primera columna de $L$:

$$l_{1,1} = \begin{cases} \sqrt{a_{1,1}}  \hspace{0.2cm} \text{si } \mu_1 < a_{1,1} \\ \sqrt{\mu_2} \hspace{0.2cm} \text{de otra manera}\end{cases}$$

$$l_{i,1} = \frac{a_{i,1}}{l_{1,1}} \hspace{.2cm} \text{para } i=1, 2, ..., n$$

2. Dado los elementos de la 1, 2, ..., $i-1^{va}$ columna se obtiene los elementos de la $i^{va}$ columna

$$l_{j,j} = \begin{cases} \sqrt{a_{j,j}  - \sum_{k=1}^{j-1} l_{j, k}^2 }, \hspace{.2cm} \text{si } \mu_1 < a_{1,1} -  \sum_{k=1}^{j-1} l_{j, k}^2 \\ \sqrt{\mu_2}, \hspace{.2cm} \text{de otra manera} \end{cases}$$

$$l_{i,j} = \frac{a_{i,j} - \sum_{m=1}^{j-1} l_{j, m} \cdot l_{i, m}}{l_{j,j}}, \hspace{.2cm} \text{para } i=j+1, ..., n$$

El parámetro $\mu_1$ debe ser pequeño para evitar modificaciones grandes de la hessiana. Aquí probablemente hay prueba y error. Como regla practica es escoger $\mu_1 = 0$ e ir ncrementándolo si ocurren dificultades y normas grandes del vector dirección.

El parámetro $\mu_2$ generalmente deber ser escogido que se mucho mas grande que $\mu_1$.  $mu_2$ puede provocar que la hessiana sea casi singular. Una regla practica es hacer $\mu_2$ pequeño e incrementarlo si la longitud de paso generado es considerablemente menor que 1. La idea es que valores pequeños de $\mu_2$ tienden a producir direcciones con normas grandes y por ende longitudes de paso pequeñas.

```{figure} images/unidad_5_cholesly_LL.png
---
width: 80%
align: center
name: cholesky ll
---
Factorización Cholesky Modificada LL
```