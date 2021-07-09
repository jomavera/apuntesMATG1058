# Optimización sin Restricciones

## Problemas de optimización univariante

Considerando una función $f : \mathbb{R} \to \mathbb{R}$ que tiene un único mínimo $c$ en un intervalo cerrado $[a,b]$. Además, $f$ es una función estrictamente decreciente en $[a,c]$ y estrictamente creciente en $[c, b]$. Funciones de este tipo son llamadas *unimodales*.

### Búsqueda de la sección dorada

Se busca reducir el espacio de búsqueda al localizar un intervalo mas pequeño donde se encuentra el mínimo. Digamos que quiero "probar" dos puntos $c$ y $d$ en el intervalo $l = [a, b]$. Si escojo un valor $\rho < 1/2$ que representa la fracción de $l$. De tal manera, que si exploro dos puntos $c=a + \rho \cdot l$ o $d = b - \rho \cdot l$, y efectivamente $x^* \in [c, b]$ o $x^* \in [a, d]$, respectivamente, entonces he reducido la incertidumbre en un factor de $(1 - \rho)$. ¿Cuál debe ser el valor de $\rho$ de tal manera que siempre se reduzaca la misma proporción? 


Consideremos el siguiente ejemplo con intervalo inicial $l=[a_0, b_0]$:




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
\rho \cdot l = (1-\rho)
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

$$\frac{a}{b} = \varphi$$

Suponiendo que $\rho < 1/2$ entonces podemos considerar que $a=1-\rho$ y $b=\rho$. Entonces {eq}`numero aureo` quedaria de esta manera:
```{math}
:label: numero aureo 2
\frac{1}{1-\rho}=\frac{1-\rho}{\rho}
```
{eq}`numero aureo 2` nos indica que $1-\rho = \frac{1}{\varphi}$. Por esto el nombre del método, así el intervalo se reduce en un factor de $1 - \rho \approx 0.618$ en cada interación.