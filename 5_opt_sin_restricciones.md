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

## Problemas de optimización multivariante

Dado el problema 

$$\min f(\textbf{x})$$

Los algoritmos clásicos para problemas de optimización sin restricciones usualmente construyen una secuencia de puntos $\{\textbf{x}^{(k)}: k \geq 0 \}$, tal que $\textbf{x}^{(k)} \to \textbf{x}^{*}$, $k \to \infty$, donde $\nabla f(\textbf{x}^{*})=\textbf{0}$.

Cada punto de la secuencia es obtenida del punto anterior moviéndose una distancia a lo largo de la dirección $\textbf{p}^{(k)}$:

$$\textbf{x}^{(k+1)} = \textbf{x}^{(k)} + \alpha^{(k)} \cdot \textbf{p}^{(k)}$$


### Algoritmos de Busqueda Lineal

En cada iteración $k$, dado el punto $\textbf{x}^{(k)}$ se escoge una dirección $\textbf{p}^{(k)}$. La dirección $\textbf{p}^{(k)}$ es seleccionada basado en:
- Métodos de primer orden: gradient $\nabla f(\textbf{x}^{(k)})$
- Métodos de primer orden: hessiana $\nabla^2 f(\textbf{x}^{(k)})$

A lo largo de esta dirección se busca una nueva solución con un mejor valor de la función. La longitud de paso se puede determinar resolviendo de manera aproximada (o exacta) el problema unidimensional:

$$\min_{\alpha \geq 0} f(\textbf{x}^{(k)} + \alpha \cdot \textbf{p}^{(k)} )$$

#### Método de Descenso de Gradiente

Es un método de búsqueda lineal que se mueve a lo largo de la dirección $\textbf{p}^{(k)} = - \nabla f(\textbf{x}^{(k)})$ en cada paso. Esta dirección es donde la función decrece mas rápidamente.

##### Pseudocódigo

```{figure} images/unidad_5_gradient_descent.PNG
---
width: 80%
align: center
name: pseudocogio gradient descent
---
Método de Descenso de Gradiente
```

#### Método de Gradiente Conjugado

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

##### Pseudocódigo

```{figure} images/unidad_5_conjugate_gradient.PNG
---
width: 80%
align: center
name: pseudocogio conjugate gradient
---
Método de Gradiente Conjugado
```