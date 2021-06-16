# Soluciones de Sistema de Ecuaciones

## Método de descomposición de matrices

La resolución de sistemas de ecuaciones lineales de la forma $A\textbf{x}=\textbf{b}$ con el método de Gausss requiere un número de operaciones en el orden de $O(n^3)$.

Utilizando métodos de descomposición de matrices se puede lograr mayor eficiencia en la resolucion de sistemas de ecuaciones.

### Factorización LU

Si $A$ es una matriz $m \times n$ que puede ser reducida a la forma escalonada sin intercambio de filas entonces $A$ puede ser descompuesta en la forma $A=L\cdot U$ donde $L$ es una matriz triangular inferior $m \times m$ con $1s$ en la diagonal y $U$ es una matriz escalonada $m \times n$.

```{figure} images/unidad_3_matriz_LU.PNG
---
width: 50%
align: center
name: descomposicion LU
---
Descomposición LU
```

Cuando  $A=L \cdot U$ entonces $A\textbf{x}=\textbf{b}$ puede ser expresado como $L(U\textbf{x})=L\textbf{y}=\textbf{b}$. De esta manera, se podrá resolver el par de ecuaciones:

$$\begin{cases}L\textbf{y}=\textbf{b}\\U\textbf{x}=\textbf{y}\end{cases}$$

Primero se resuelve $L\textbf{y}=\textbf{b}$ para $\textbf{y}$ y luego se resuelve $U\textbf{x}=\textbf{y}$ para $\textbf{x}$. Como $L$ es triangular inferior se pude resolver por **sustitución hace adelante** y $U$ por se triangular superior se resuelve por **sustitución hacia atrás**. Esto permite, de manera recursiva, resolver los sistemas sin usar eliminación gaussiana.

#### Eficiencia computacional

```{margin}
**¿Por que usarlo?**

Digamos que tenemos que resolver frecuentemente el sistema de ecuaciones $A\textbf{x}=\textbf{b}$ para diferentes valores de $\textbf{b}$. Una vez realizado la factorización podemos reutilizarla. De esta manera, el número de operaciones es de orden $O(n^2)$.
```

- **Factorización LU**: Para una matriz densa (la mayoría de sus elementos son $\neq 0$) $A_{n \times n}$ la factorización LU toma $\frac{2}{3}n^3$ flops y para resolver $L \textbf{y}=\textbf{b}$ y $U\textbf{x}=\textbf{b}$ se requiere $2n^2$ flops

- $\textbf{x}=A^{-1}\textbf{b}$: Para computar $A^{-1}$ se requiere aproximadamente $\frac{8}{3}$ flops y multiplicar $A^{-1}\cdot b$ requiere $2n^3$ flops

- **Eliminación Guassiana**: Requiere en términos de operaciones, $n(n+1)/2$ divisiones, $(2n^3+3n^2-5n)/6$ multiplicaciones, y $(2n^3+3n^2-5n)/6$ sumas/restas. Siendo en totla aproximadamente $\frac{2}{3}$ flops.

#### Pseudocódigo

```{figure} images/unidad_3_factorizacion_LU.PNG
---
width: 80%
align: center
name: pseudocodigo descomposicion LU
---
Pseudocódigo Descomposición LU
```

### Factorización LU con cambios de filas

Ahora consideraremos que debe haber un cambio de filas para hacer la factorización LU. Usemos una matriz de permutación $P$ tal que $P\cdot A=L\cdot U$ entonces $A=(P^T\cdot L)\cdot U$. 

Digamos que tenemos la matriz $A = \begin{bmatrix}a_{11} & a_{12} & a_{13} \\a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{bmatrix}$ y la matriz $P=\begin{bmatrix}1 & 0 & 0 \\0 & 0 & 1 \\ 0 & 1 & 0 \end{bmatrix}$. La operación $P \cdot A$ cambiará la posición de la segunda fila por la tercera fila esto es $\begin{bmatrix}a_{11} & a_{12} & a_{13} \\a_{31} & a_{32} & a_{33} \\ a_{21} & a_{22} & a_{23} \end{bmatrix}$

De esta manera, al resolver el sistema de ecuaciones el vector $\textbf{x}$ estará permutado. Teniendo la matriz $P$ resolvemos

$$\begin{cases}L\textbf{y}=P\cdot \textbf{b}\\U\textbf{x}=\textbf{y}\end{cases}$$

### Factorización de Cholesky

Existen unas clases de matrices donde se puede aplicar la eliminación gaussiana efectivamente sin intercambio de las filas. La factorización Cholesky permite la resolución de una sistema lineal $A\textbf{x}=\textbf{b}$ que se puede aplicar cuando la matriz $A$ es *definida positiva*. En las siguientes unidades vamos a ver que el problema de optimizar una función de varias varibles esta relacionado a la resolución de sistemas de ecuaciones y que en el caso de funciones estrictamente convexas su hessiana es definida positiva. En estos casos se puede utilizar la factorización Cholesky. Cuando es aplicable esta factorización es mas rápida que la factorización LU.

```{div} definicion
**Matriz definida positiva**

Una matriz es definida positiva si es simétrica y $\textbf{x}A^T\textbf{x} > 0$ para cada vector $n$-dimensional $\textbf{x} \neq 0$
```

De la definición de una matriz definida positiva puede ser dificil verificar esta condición. El siguiente lema nos facilidad poder determinar esta condición en las matrices

```{div} definicion
**Lema**

Las siguientes declaraciones son equivalentes:

- $A$ es definida positiva
- Todos los valores propios de $A$ son positivos
- Todos los elementos diagonales en una factorización de Cholesky son positivos
- Cada una de sus submatrices principales tine su determinante (menor principal) positivo
- Exista una matriz no singular $L$ tal que $A=L \cdot L^T$

```
El anterior lema indica que podemos verificar los principales menores superiores (criterio de Sylvester) para determinar si la matriz es definida positiva

```{div} definicion
**Principal menor**

Los principales menores $D_k$, $k=1,2,...,n$ de una matriz $A=(a_{ij})_{n \times n}$ son definidas como

$$D_k=det \begin{pmatrix}a_11 & \cdots & a_{1k} \\ \vdots & \ddots & \vdots \\ a_{k1} & \cdots & a_{kk}\end{pmatrix}$$
```

#### Pseudocódigo

```{figure} images/unidad_3_algo_cholesky.PNG
---
width: 80%
align: center
name: pseudocodigo cholesky
---
Pseudocódigo factorización de Cholesky
```

Para resolver el sistema con la matriz $L$,


```{figure} images/unidad_3_algo_cholesky_sist.png
---
width: 80%
align: center
name: pseudocodigo sistema cholesky 
---
Pseudocódigo resolución de sistema de ecuaciones con factorización de Cholesky
```

#### Eficiencia computacional

Este método solo requiere $\frac{1}{6}n^3+\frac{1}{2}n^2-\frac{2}{3}n$ divisiones/multiplicaciones y $\frac{1}{6}n^3-\frac{1}{6}n$ sumas y restas. Luego, la resolución de del sistema requiere $n^2+n$ multiplicaciones/divisiones y $n^2−n$ sumas y restas.

De esta manera, Cholesky requiere menos operaciones en la factorización y en la resolución del sistema que la factorización LU.

## Método de Newton para resolución de sistemas de ecuaciones no lineales

En el capítulo 2 vimos el método de Newton para la resolución de una ecuación con una variable. Ahora aplicaremos el método para una sistema de ecuaciones no lineales.

Consideremos un sistema de $n$ ecuaciones y $n$ variables que puede ser representado como una función vectorial $F: \mathbb{R}^n \to \mathbb{R}^n$, esto es,

$$F(x_1, ..., x_n) = \begin{bmatrix}f_1(x_1,...,x_n) & \cdots & f_n(x_1,...,x_n) \end{bmatrix}^T$$

El problema es resolver el sistema de ecuaciones tal que $F(\textbf{x})=\textbf{0}$

Consideremos el polinomio de Taylor 

$$F(\textbf{x}) \approx F(\textbf{x}^{(k)}) + J(\textbf{x}^{(k)})(\textbf{x}-\textbf{x}^{(k)})$$

donde $J(\textbf{x}^{(k)})$ es la matriz jacobiana de $F$ evaluada en $\textbf{x}^{(k)}$

Sea $\textbf{x}^*$ la solución para $F(\textbf{x}^*)=0$. Suponga que exista un $\delta >0$ tal que:

- $\frac{\partial f_i(\textbf{x})}{\partial x_j}$ es continuo en $N_{\delta}=\{\textbf{x} | \|\textbf{x}=\textbf{x}^* \| < \delta \}$ para cada $i=1,...,n$ y $j=1,...,n$.

- $\frac{\partial^2 f_i(\textbf{x})}{\partial x_j \partial x_k}$ es continuo y $\big |\frac{\partial^2 f_i(\textbf{x})}{\partial x_j \partial x_k} \big | \leq M$ para alguna constante $M$ cuando $x \in N_{\delta}$ para cada $i=1,...,n$ y $k=1,...,n$.

- $\frac{\partial f_i(\textbf{x}^*)}{\partial x_k} = 0$ para cada $i=1,...,n$ y $k=1,...,n$.

Entonces un $\bar{\delta} \leq \delta$ existe tal que la secuencia generada por $\textbf{x}^{(k)}=F(x^{(k-1)})$ converge cuadráticamente a $\textbf{x}^*$ para cualquier elección de $x^{(0)}$ dado que $\|\textbf{x}^{(0)} - \textbf{x}^* \| < \bar{\delta}$. Ademas,

```{margin}
{eq}`convergencia_newton_sist_ec` sugiere orden de convergencia cuadrática si el punto inicial esta lo suficientemente cercana a la solución $\textbf{x}^*$.
```

```{math}
:label: convergencia_newton_sist_ec
\| \textbf{x}^{(k)} - \textbf{x}^* \|_{\infty} \leq \frac{n^2 M}{2} \| \textbf{x}^{(k-1)}-\textbf{x}^* \|^2_{\infty}
```

### Pseudocódigo

```{figure} images/unidad_3_metodo_newton.PNG
---
width: 80%
align: center
name: pseudocodigo newton sistema ecuaciones
---
Pseudocódigo Método de Newton para resolución de sistema ecuaciones no lineales
```