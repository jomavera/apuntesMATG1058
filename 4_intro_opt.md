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

### Existencia de solución optima

Aun asi una función  esta inferiormente acotada, no siempre existe un mínimo global pero si tiene un ínfimo como se indica en la siguiente definición.

```{div} definicion
**Ínfimo, Supremo**

Para una función $F:X \to \mathbb{R}$, su mayor cota inferior es llamdo el ínfimo y es denotado como $\inf_{x \in X} f(x)$. Similarmente, su menor cota superior es llamado supremo y es denotado por $\sup_{x \in X} f(x)$
```
Si $f$ no esta acotada inferiormente o superiormente, entonces $\inf_{x \in X} f(x)=-\infty$ o $\sup_{x \in X} f(x)=+\infty$, respectivamente.

Verificar si una función tiene una solución óptima global es difícil en general. Existen ciertos tipos de funciones donde se pueden garantizar la existencia de una solución óptima global.

```{div} definicion
**Teorema Weierstrass**

Los problemas $\min_{x \in X} f(x)$ y $\max_{x \in X} f(x)$, donde $X \subseteq \mathbb{R}^n$ es un conjunto compacto y $f: X \to \mathbb{R}$ es una función continua, tiene soluciones óptimas globales.
```