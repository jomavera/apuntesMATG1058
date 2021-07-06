# Optimización sin restricciones

## Problemas de optimización univariante

Considerando una función $f : \mathbb{R} \to \mathbb{R}$ que tiene un único mínimo $c$ en un intervalo cerrado $[a,b]$. Además, $f$ es una función estrictamente decreciente en $[a,c]$ y estrictamente creciente en $[c, b]$. Funciones de este tipo son llamadas *unimodales*.

### Busqueda de la sección dorada

Se busca reducir el espacio de búsqueda al localizar un intervalo mas pequeño donde se encuentra el mínimo. Digamos que quiero "probar" dos puntos $c$ y $d$ en el intervalo $l = [a, b]$. Si escojo un valor $\rho < 1/2$ que representa la fracción de $l$. De tal manera, que si exploro dos puntos $c=a + \rho \cdot l$ o $d = b - \rho \cdot l$, y efectivamente $x^* \in [c, b]$ o $x^* \in [a, d]$, respectivamente, entonces he reducido la incertidumbre en un factor de $(1 - \rho)$.