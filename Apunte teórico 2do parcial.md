# Extras
- Para demostrar igualdad entre dos "expresiones" A y B, basta con probar que A$\leq$B y A$\geq$B.

# Grafos general | agregar alguna cosa de las representaciones de grafos (lista de adyacencia, matriz, etc)
- Un **multigrafo** es aquel grafo que admite varias aristas entre un mismo par de vertices.
- Un **pseudografo** es aquel grafo que admite varias aristas entre un mismo par de vertices y ademas aristas que unan un vértice consigo mismo(loops).
- Un grafo **completo** es aquel cuyos vertices tienen todos grado n-1, donde n es la cantidad de vertices del grafo.
- Un grafo G es **junta** si se puede escribir G como $G_1 + G_2$ disjuntos, donde en la suma se agregan todas las aristas posibles entre los vertices de cada uno de los subgrafos.
- Un grafo G es union cuando se puede escribir como $G_1 \cup G_2$ disjuntos, donde no se agrega ninguna arista entre vertices de ambos subgrafos. 
- Un grafo es **cactus** si cada una de sus aristas pertenece a un único ciclo. 
### Trazas de un grafo
- Un **recorrido** en un grafo es una secuencia alternada de vertices y aristas $v_0e_1v_1...v_{k-1}e_kv_k$ que describe el trayecto de $v_0$ hasta $v_k$.
	- En un grafo, un recorrido queda definido por una secuencia de vertices como la de arriba.
- Un **camino** es un recorrido que no pasa dos veces por el mismo vértice.
	- Una **sección** de un camino P es una subsecuencia de dicho P. 
- Un **circuito** es un recorrido que empieza y termina en el mismo vértice. 
	- Un **ciclo** es un circuito de 3 o mas vertices que no pasa dos veces por el mismo vértice.

### Subgrafos
- Un **subgrafo** de un grafo G es un grafo H tal que sus vertices y aristas "salen" de G.
- Se nota como $H \subseteq G$.
	- Si $H \subseteq G$ y $H \neq G$ entonces $H \subset G$.
- H es un **subgrafo generador** de G si $H \subseteq G$ y sus vertices son los mismos.
- H es un **subgrafo inducido** de G si todo vértice que este en H tiene las aristas posibles del grafo original G.

### Propiedades varias
- Dos grafos G = (V, X) y G' = (V', X') se dicen **isomorfos** si existe una funcion biyectiva $f: V \rightarrow V'$ tal que para todo v, w $\in$ V:$$ (v, w) \in X \Longleftrightarrow (f(v), f(w)) \in X' $$
- Los grafos densos son aquellos que tienen mas de $\epsilon . n^2$ aristas, con $\epsilon \in \{ 0...1 \}$.
- Los grafos ralos tienen menos de $c.n$ aristas, con $c \in \{ 1 ... \}$.


# Algoritmos | agregar sort topológico
## Arbol generador
- Todo grafo conexo tiene al menos un arbol generador.
- Un grafo G tiene un único arbol generador si y solo si G es un arbol.
- Sea T = (V, $X_T$) un arbol generador de G = (V, X) y e una arista que no esta en T, si le agrego la arista e a T, se forma un circuito/ciclo, luego si tomo cualquier arista de dicho circuito/ciclo que no sea e y la quito de T, T sigue siendo un arbol generador.
### DFS
- Implementa la lista de vertices como **pila**.
- Tiene complejidad `O(|V|+|E|)`.
- Se puede usar para chequear que hayan ciclos.
	- En un dígrafo, hay un ciclo orientado si y solo si hay una backward edge en dicho grafo. 
- Se encuentran las componentes fuertemente conexas de un dígrafo.
- Se usa tambien para el sort topológico. 
- Encuentra los puentes y puntos de articulación. 
- Genera un bosque a través de los caminos generados (?
- Clasifica las aristas del grafo en(solo me interesan las primeras 2):
	- Tree edges: aquellas que forman parte del arbol DFS.
	- Backward edges: las que van de un vértice hacia un ancestro(osea un vértice ya visitado).
	- Forward edges: las que van hacia un descendiente, osea tree edges entiendo. En dígrafos NO.
		- Cross edges: las que van de un arbol del bosque a otro. En dígrafos NO. 

### BFS
- Implementa la lista de vertices como **cola**.
- Tiene complejidad `O(|V|+|E|)`.
- Corriéndolo desde un vértice raíz v se puede obtener el camino mínimo hacia cualquier vértice, siempre que el grafo no este ponderado.  
- Se usa para encontrar el AGM de un grafo no ponderado.
- Encuentra todos los nodos alcanzables desde una raíz.
- Encuentra el camino mínimo mas largo(diámetro del grafo) y distancias.
- Tambien encuentra ciclos, el orden topológico y las componentes fuertemente conexas.
- Si el grafo no es ponderado, encuentra caminos mínimos desde la raíz(AGM). 
- Sirve para el chequeo de un grafo bipartito.

### Prim
- Tiene complejidad O($n^2$) con una implementación estándar, O(m log n) usando un heap binario y O(m + n log n) usando heap Fibonacci. 
- Todo arbol $T_k$ que el algoritmo de Prim genera en su k-esima iteración es un subarbol de un arbol generador mínimo de G, siendo G el arbol del que se parte con Prim.
- Puede usarse aun si el grafo tiene aristas de peso negativo. 
- Es un algoritmo goloso.

### Kruskal
- Sea $B_k$ el bosque que genera el algoritmo de Kruskal en algún momento con k aristas, $B_k$ es un subgrafo generador sin ciclos de un arbol generador mínimo de G, siendo G el arbol del que se parte con Kruskal. 
- Tiene complejidad O(m * n) con implementación estándar, O(m log n + m log n) usando "union and find" (por rango) y O(m log n + m * $\alpha$(n)) usando "union and find" (por rango + compresión de camino).
- Es un algoritmo goloso.

### Camino Maximin
Todo camino entre dos vertices de un arbol generador minimo T es `maximin`.

# Correctness
## Camino mínimo
Se pueden definir distintos tipos de variantes de caminos mínimos:
- Unico origen - único destino (uno a uno): Determinar el camino mínimo entre dos vertices específicos.
- Unico origen - múltiples destinos(uno a todos): Determinar el camino mínimo entre un vértice especifico y todo el resto de vertices del grafo. 
- Múltiples orígenes - múltiples destinos(todos a todos): Determinar un camino mínimo entre todo par de vertices de G.
#### Matices y propiedades
- Si desde un vértice de inicio se puede llegar a un ciclo negativo, el problema deja de estar bien definido.
- Tambien si tiene ciclos normales.
- Se cumple la propiedad de subestructura optima. (Dado un camino P que va de $v_1$ a $v_k$, el subcamino que va de $v_1$ a $v_{k-2}$ es justamente el camino mínimo posible).
- **Desigualdad triangular**: Para toda arista $(u, v) \in E$, se tiene que $m(s, v) \leq m(s, u) + p(u, v)$, donde $m(s, v)$ es la funcion que devuelve el camino minimo entre $s$ y $v$, y $p(u, v)$ el peso de dicha arista.
- Si no hay un camino existente entre dos vertices, su camino minimo es de $\infty$.
- 


### Dijkstra
- Tiene complejidad O($n^2$) con implementación trivial. Usando una cola de prioridad a las aristas de igual peso la complejidad queda O((m+n) log n) con heap binario y O(m + n log n) usando heap Fibonacci.
	- Mas bien, $min\{n^2, m*log(n) \}$ sobre lista de adyacencias.
- No funciona para aristas negativas.
#### Invariante de Dijkstra
Sea S el conjunto de vertices "finalizados", y W = V \ S los restantes. Entonces se cumple siempre que:
- Para todo u $\in$ S: d[u] es su verdadera distancia mínimo desde el origen.
- Para todo v $\in$ W: d[w] es una cota superior de la distancia mínima, y ademas $d[v] \geq \underset{u \in S}{min}\  d[u]$ 



### Bellman-Ford
- Tiene complejidad O(n * m).
- **Principio de optimalidad**: Todo subcamino minimo es un camino minimo(siempre que no haya ciclos negativos)
#### Invariante de Bellman-Ford
Sea $d_k[v]$ la mejor distancia conocida desde el origen a usando a lo sumo k aristas. Tras la iteración k se cumple:
- $d_k[v]$ es la distancia mínima desde el origen a v usando k o menos aristas.
- Por lo tanto, al iterar hasta k = |V| - 1, dado que los caminos siempre tienen |V|-1 o menos aristas, al final de cada d[v] será la distancia mínima real. Siempre que no hayan ciclos negativos.
Tambien se puede leer como que luego de i iteraciones, para cada vértice v se tiene que d[v] es la menor distancia posible desde el origen con i o menos aristas. Como al final i vale |V| - 1, se asegura que se considere todos los caminos posibles.
 
### Floyd
- Determina los caminos mínimos entre todos los pares de nodos de un grafo orientado sin ciclos negativos.
- Tiene complejidad O($n^3$)
- Conviene por sobre el de Johnson si el grafo es denso
#### Invariante de Floyd-Warshall
Sea $D_k[i][j]$ la distancia mínima entre los vertices $i \rightarrow j$ usando únicamente vertices intermedios del conjunto {1... k}, entonces:
- Al inicio k = 0, $D_0[i][j]$ es el peso de la arista, que puede existir o no.
- Tras el paso k se cumple que $D_k[i][j] = min(D_{k-1}[i][j], D_{k-1}[i][k] + D_{k-1}[k][j])$ 
- Al final, cuando k vale |V|, quedan los valores reales de distancia entre todos los nodos.


### Dantzig
- Determina los caminos mínimos entre todos los pares de nodos de un grafo orientado sin ciclos negativos.
- Tiene complejidad $O(n^3)$.
- La parte de recalcular las distancias cuando agrego una entrada a la matriz es en $O(n^2)$.

### Algoritmo de Khan
- Devuelve un orden topológico de los nodos de un digrafo.
- Si no hay ninguna arista de grado de entrada 0, hay un ciclo, por lo que no se puede dar un orden topologico.
- Si hay mas de un nodo de grado 0, agarra cualquiera.

### Algoritmo de Johnson
- Tiene complejidad O(nm + n* m * log(n)) = O(n * m * log(n))
- Conviene por sobre el de Floyd si el grafo es ralo/disperso

### Algoritmo de Ford-Fulkerson
- Tiene complejidad O(nmU), siendo U = $min_{ij \in A}\ u_{ij}$ 
- Si las capacidades son irracionales, puede no detenerse.

### Algoritmo de Edmonds y Karp
Similar a Ford-Fulkerson, pero usando BFS para encontrar los caminos de aumento restantes.\
- Su complejidad es $O(nm^2)$


## DAG (dígrafo sin ciclos)
- Con DFS o BFS en O(n + m) puedo ver si un digrafo es DAG. 
- No todo digrafo tiene un orden topologico. 
- Todo DAG tiene un orden topológico(no único).
- Todo digrafo que tiene orden topológico es DAG.
- Un digrafo con n vertices tiene como mucho `n(n-1)` ejes(aristas dirigidas).

Para obtener un DAG de caminos mínimos:
- BF desde nodo origen (aDest)
- Traspongo y BF desde nodo destino (aOri)
- Creo un nuevo grafo T con los nodos de G sin aristas
- Itero sobre las aristas (u, v) de G, las que cumplen que $aOri[u] \  + \ peso(u, v) + \ aDest(v) = aDest(ori)$, se agrega a T
Tambien si no hay aristas negativas ni ciclos, se puede usar directamente Khan u otro algoritmo de ordenamiento topologico y relajar las aristas en ese orden

## Demostración de correctitud
Para la demostración queremos ver que el algoritmo devuelve la solución óptima, donde la solución óptima es lo que me plantea la consigna que busque, y lo que devuelve el algoritmo, lo que sea que devuelva el algoritmo planteado

# Flujo
Se tiene que cumplir que:
- Conservación de flujo: salvo s y t, en cada nodo la cantidad de flujo que entra debe ser igual a la que sale.
- Restricción de capacidad: 0 ≤$x_{ij}$ ≤$u_{ij}$ para todo ij ∈A.
- El valor del flujo es el flujo neto que sale de s.

Pasos en los ejercicios de flujo:
- Modelado
- Semántica del flujo 
- Conexión modelo-problema 

Algunas formas de acotar el flujo máximo en problemas donde no es tan directo:
- La suma de las capacidades de las aristas que salen de s.
- La suma de las capacidades de las aristas que entran a t.
- Si U es la capacidad más grande de todas las aristas, podemos acotar el flujo por O(nU), siendo n la cantidad de vértices.

La demostración principal en un problema de flujo es:
$$
\text{Existe un flujo valido en N de valor F} \Longleftrightarrow \text{Una solucion posible para el problema P modelado con la red N tiene valor F}
$$
![[Screenshot 2025-11-16 at 12.22.05.png]]

Si las unidades de flujo son enteras, por el teorema de integridad de flujo, el flujo máximo se considera entero.
Por el teorema del corte mínimo, el valor del flujo máximo es igual al tamaño del corte mínimo.
### Caminos disjuntos

### Asignación

### Transporte de objetos

### Modelo con corte mínimo

### Flujo máximo de costo mínimo
