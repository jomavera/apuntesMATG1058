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