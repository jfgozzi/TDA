LEMA: 
Si una solución es optima, entonces al quitar cualquier objeto de ella, la solución restante debe ser optima para el subproblema correspondiente. 
### Complejidades
- Acceso a memoria, sea lectura o escritura, es `O(1)`.
- Asignación y manejo de estructuras, es `O(1)`.
- Operaciones entre valores lógicos (booleanos), es `O(1)`.
- Las sumas y restas son `O(n)`, y multiplicaciones y divisiones `O(nlogn)` si el n no es fijo. Si lo es, entonces son `O(1)`.

Definimos el tiempo de ejecución de un algoritmo A como $T_A(I)$. Donde $T_A(I)$ es la suma de los tiempos de ejecución de las instrucciones de A con la instancia I.
También decimos que `|I|` es la cantidad de bits que se necesitan para almacenar los datos de la entrada `I`.
Entonces, la complejidad final de un algoritmo A se puede definir como: 
$f_A(n) = max_{I:|I|=n} T_A(I)$ 

- `O(n)` se dice **lineal**.
- `O(`$n^2$`)` se dice **cuadratico**.
- `O(`$n^3$`)` se dice **cubico**.
- `O(`$n^k$`)` se dice **polinomial**.
- `O(log n)` se dice **logaritmico**.
- `O(n)` se dice **exponencial**.


### Fuerza bruta y Backtracking
#### Fuerza bruta
- Consiste en generar todas las soluciones factibles y quedarse con la mejor. 
- Es exacto, si hay una solución, la encuentra.
- Habitualmente tiene complejidad exponencial.

#### Backtracking
Básicamente, un fuerza bruta con podas.

### Programación Dinámica 
Aprovecha la superposición de problemas para evitar repetir llamadas recursivas.
#### Top-Down
Se implementa recursivamente, guardando el resultado de cada llamada particular en una estructura de datos (memorización).

#### Bottom-up
Se resuelven primero los subproblemas mas pequeños y se guardan.

### Greedy


O(N*K)

