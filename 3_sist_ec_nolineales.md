# Solución de sistema de ecuaciones

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
**¿Por que usarlo**

Digamos que tenemos que resolver frecuentemente el sistema de ecuaciones $A\textbf{x}=\textbf{b}$ para diferentes valores de $\textbf{b}$. Una vez realizado la factorización podemos reutilizarla. De esta manera, el número de operaciones es de orden $O(n^2)$.
```

- **Factorización LU**: Para una matriz densa (la mayoría de sus elementos son $\neq 0$) $A_{n \times n}$ la factorización LU toma $\frac{2}{3}$ flops y para resolver $L \textbf{y}=\textbf{b}$ y $U\textbf{x}=\textbf{b}$ se requiere $2n^2$ flops

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

### Factorización Cholesky

Existen unas clases de matrices donde se puede aplicar la eliminación gaussiana efectivamente sin intercambio de las filas. La factorización Cholesky permite la resolución de una sistema lineal $A\textbf{x}=\textbf{b}$ que se puede aplicar cuando la matriz $A$ es *definida positiva*. En las siguientes unidades vamos a ver que el problema de optimizar una función de varias varibles es equivalente a la resolución de un sistema de ecuaciones y que en el caso de funciones estrictamente convexas su hessiana es definida positiva. En estos casos se puede utilizar la factorización Cholesky.

