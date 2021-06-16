# Soluciones de Ecuaciones No Lineales

Vamos a ver algoritmos para resolver ecuaciones no lineales. Estos métodos son la base para algoritmos de optimización no lineal. 

**¿Raíz de una función? ¿Solución de una ecuación?**
Frecuentemente nos encontramos con estas dos expresiones. Estas son equivalentes ya que una ecuación puede ser definida como una función y la raíz de la función es la solución de la ecuación, por ej.,
- La ecuación $x^3+30x^2=10$.
- La función $f(x)=x^3+30x^2-10$.

La raíz $r$ de $f(x)$ es tal que $f(r)=0$ que asu vez es una solución para la ecuación. 

## Método de la Bisección

Es un método iterativo que permite encontrar la solución de ecuaciones no lineales de una variable. La idea del algoritmo es que si graficamos una función $f(x) = \mathbb{R} \to \mathbb{R}$ en un intervalo $[a,b]$, entonces existe la raíz de $f(x)$ en este intervalo si y solo si un subintervalo de la gráfica es negativa y otro subintrevalo es positivo. Entonces, si divido el intervalo en dos, la solución estará en alguno de los dos subintervalos. Si sigo sucesivamente este procedimiento llegaré a un intervalo lo suficientemente pequeño que su punto medio será muy cercano a la raíz.

Por ejemplo, tengamos las siguientes funciones:
- $x^2-10=0$
- $x^2+2=0$.

y las graficamos ({numref}`Fig. {number} <comparativo funciones>`) en el intervalo $[0,6]$

```{margin}
Claramente si partimos con un intervalo donde no se encuentra la raíz el método no converge.
```

```{figure} images/unidad_2_ejemplo_biseccion.PNG
---
width: 80%
align: center
name: comparativo funciones
---
Funciones con y sin raiz en el intervalo
```

Si aplicamos el método de la bisección a la ecuación $x^2-10=0$ y seleccionamos el criterio para detener el método cuando la longitud del intervalo es menor que 0.8. En la tercera iteracion llegamos a un intervalo de $4.5-3.75<0.8$. Entonces nuestra solución es $\frac{4.5+3.75}{2}=4.125$.

```{figure} images/unidad2_ej_biseccion.png
---
width: 90%
align: center
name: ej biseccion
---
Método de la bisección aplicado a $f(x)=x^2-10$
```

### Pseudocódigo

```{figure} images/unidad_2_algo_biseccion.PNG
---
width: 80%
align: center
name: pseudocodigo metodo de la biseccion
---
Pseudocódigo método de la bisección
```

### Orden de Convergencia
Para cada iteración $n$ el método de bisección tenemos que $b_n-a_n=\frac{b-a}{2^{n-1}}$ para $n \geq 1$.

Si $c_n=\frac{1}{2}(b_n+a_n)$ entonces $E_n=|c_n-c^*|\leq \frac{1}{2}(b_n-a_n)=\frac{b-a}{2^n}=O\bigg(\frac{1}{2^n}\bigg)$.

Esto es lo mismo que

```{margin}
{eq}`convergencia_biseccion` indica que el error se reduce linealmente. Por lo tanto, el orden de convergencia del método es lineal.
```

```{math}
:label: convergencia_biseccion
c_n = c^* + O\bigg(\frac{1}{2^n}\bigg)
```

## Método de Punto Fijo

El número $p$ es un punto fijo para alguna función $g(x)$ si $g(p)=p$. El método de punto fijo consiste en replantear el problema de encontrar la raíz de $f(x)$ en el problema de encontrar el punto fijo de otra función $g(x)$. Estos dos problemas son equivalentes dado $g(x)=x-f(x)$ en el siguiente sentido:
- Si $f(p)=0$, entonces $g(p)=p$.
- Por el contrario, si $g(p)=p$ entonces $f(p)=0$.

```{figure} images/unidad2_ej_ptofijo.png
---
width: 80%
align: center
name: ej punto fijo
---
Ejemplo de $f(x)$ y $g(x)$
```

### Pseudocódigo

```{figure} images/unidad_2_algo_punto_fijo.png
---
width: 80%
align: center
name: pseudocodigo metodo de punto fijo
---
Pseudocódigo método de punto fijo
```

### Existencia y unicidad de punto fijo

**Existencia**.

Si $g(a)=a$ o $g(b)=b$, entonces $g$ tiene un punto fijo en los extremos. Si no, entonces $g(a) >a$ y $g(b)< b$. La función $f(x)=g(x)-x$ es continua en $[a,b]$, con $f(a)=g(a)-a > 0$ y $f(b)=g(b)-b<0$. Por el teorema de valor medio, hay un punto $p \in [a,b]$ para que $f(p)=0$. Entonces, el numero $p$ es un punto fijo para $g$ porque

$$f(p)=g(p)-p \hspace{0.2cm}\to \hspace{0.2cm} g(p)=p$$

**Unicidad**.

Suponga que $|g'(x)|\leq k <1$, y que $p$ y $q$ son dos puntos fijos en $[a,b]$. Si $p \neq q$, el teorema del valor medio implica que existe un número $\varepsilon$ entre $p$ y $q$ con,

$$\frac{g(p)-g(q)}{p-q}=g'(\varepsilon)$$

entonces $|p-q|=|g(p)-g(q)|=|g'(\varepsilon)||p-q|\leq|p-q|<|p-q|$ lo que es una contradicción, y solo se cumple para $p=q$ por lo que el punto fijo en $[a,b]$ es único.



```{div} definicion
**Teorema (Existencia y Unicidad de Punto Fijo)**

Sea $g: [a,b] \to [a,b]$ una función diferenciable tal que:

$$|g'(x)|\leq \alpha < 1 \text{ para todo } x\in[a,b]$$

entonces $g$ tiene únicamente un solo punto fijo $p$ en $[a,b]$
```

### Orden de Convergencia

Asumiendo que $|g'(x)|\geq k < 1$ y si la función $g$ cumple con el teorema de punto fijo entonces las acotas del error para ciertas interacion $n$ es 

$$|x^{(n)}-p| \leq k^n \cdot \max\{x^{(0)}-a, b-x^{(0)}\}$$

y

$$|x^{(n)}-p| \leq \frac{k^n}{1-k} |x^{(1)}-x^{(0)}|$$

## Método de Newton para la resolución de ecuaciones de una variable

Se utiliza la derivada de la función para actualizar una solución inicial y así converger a la raíz de la función. Si partimos de la aproximación de Taylor de primer orden de $x$:

$$q(x) \approx f(x^{(n)}) + (x - x^{(n)})f'(x^{(n)})$$

e igualamos a cero obetenemos la *formula de Newton*:

$$f(x^{(n)}) + (x - x^{(n)})f'(x^{(n)}) = 0$$


```{math}
:label: formula newton
x^{(n+1)} = x^{(n)} - \frac{f(x^{(n)})}{f'(x^{(n)})}
```

### Pseudocódigo

```{figure} images/unidad_2_algo_newton.png
---
width: 80%
align: center
name: pseudocodigo metodo de newton
---
Pseudocódigo método de Newton
```

### Orden de convergencia

Podemos aproximar el valor de $f(x)$ para un $x \in I$ por el polinomio de Taylor como

$$f(x) = f(p) + f'(p)(x-p)+\frac{f''(\varepsilon)}{2}(x-p)^2$$

donde $\varepsilon$ esta entre $x$ y $p$. Si asumimos que $f'(p)=0$ y $f(p)=p$ implica que 

$$f(x)=p+\frac{f''(\varepsilon)}{2}(x-p)^2$$

Si definimos $x^{(n+1)}=f(x^{(n)})$,

$$x^{(n+1)}=p+\frac{g''(\varepsilon_n)}{2}(x^{(n)}-p)^2,$$

$$\frac{|x^{(n+1)}-p|}{|x^{(n)}-p|^2}=\frac{|g''(\varepsilon_n)|}{2}.$$

Como $|g'(x)|\leq k < 1$, entonces $\{x^{(n)}\}_{n=0}^{\infty}$ converge a $p$ y $\{\varepsilon_n\}_{n=0}^{\infty}$ también converge a $p$ entonces


```{math}
:label: orden de convergencia newton ec
\lim_{n \to \infty} \frac{|x^{(n+1)}-p|}{|x^{(n)}-p|^2} = \frac{|g''(p)|}{2}
```
