# Ejercicio 1 🧱
![[Screenshot 2025-10-28 at 14.54.35.png]]
## a)
### $\Longrightarrow)$
Asumo que $v \rightarrow w$ es $st$-eficiente y quiero probar que $d(s, v) + c(v \rightarrow w) + d(w,t) = d(s,t)$ 
Que la arista  $v \rightarrow w$ sea $st$-eficiente ya de por si significa que pertenece a algún camino minimo entre s y t. 
Sea C el camino que pasa por la arista $v \rightarrow w$, d(s, t) = d(C) es igual a la suma de los pesos de todas las aristas de C, como se que $(v \rightarrow w) \in C$ puedo descomponer la formula de la distancia del camino C como $d(s, v) + c( v \rightarrow w) + d(w, t)$.
### $\Longleftarrow)$ 
Asumo que $d(s, v) + c(v \rightarrow w) + d(w,t) = d(s,t)$ y quiero probar que  $v \rightarrow w$ es $st$-eficiente.
Como la funcion $d(.,.)$ devuelve el peso de un camino minimo entre dos vertices, y estoy asumiendo que justamente, el peso de un camino minimo entre el vértice `s` y el vértice `t` lo puedo escribir como la suma entre el peso de un camino minimo entre `s` y `v`, el peso de la arista ($v \rightarrow w$) y el peso de un camino minimo entre `w` y `t`, queda explícitamente claro que para el camino minimo entre `s` y `t` que se este teniendo en cuenta en la funcion d, la arista ($v \rightarrow w$) forma parte de el, por lo que siguiendo la consigna, ($v \rightarrow w$) es $st$-eficiente.
## b)
 
# Ejercicio 2 ✅ (re-hacer la demo)
![[Screenshot 2025-10-28 at 14.55.57.png]]
Corro una vez Dijkstra desde s, traspongo el grafo y lo corro desde t. Luego recorro todas las aristas del grafo original y separo las que cumplan que $d(s, w_1) + c(w_1, w_2) + d(w_2, t) \leq c$, las guardo en un conjunto separado y retorno la que mayor peso tenga.

Propongo que la correctitud venga de que no puede pasar que una arista que no fue tenida en cuenta por el algoritmo propuesto antes puede cumplir con la consigna.
Al correr Dijkstra por primera vez desde `s` voy a obtener los caminos mínimos desde s hacia todo el resto de vertices, incluido `t` (asumiendo G conexo). Por otro lado, correr Dijkstra desde `t` me da los caminos mínimos desde `t` hacia cualquier otro vértice del grafo. Como la consigna me esta pidiendo la arista de mayor peso que este entre `s` y `t`, usando los caminos mínimos entre ellos obtenido con Dijkstra la voy a conseguir, en realidad consigo todas las aristas involucradas en algún camino minimo entre ellos, fijándome puntualmente en los caminos mínimos entre `s` y un vértice de la arista que este viendo(lo mismo con `t`), obteniendo así el camino minimo que involucre dicha arista.
# Ejercicio 3 ✅ 
![[Screenshot 2025-10-28 at 14.56.03.png]]
- Creo un grafo G' a partir de G, que es idéntico a G solo que sin las aristas de peso negativo.
- Corro Dijkstra desde `s` y obtengo los caminos mínimos desde `s` hacia todo el resto de vertices de G'.
- Corro una segunda vez Dijkstra pero ahora desde $\overline{G'}$(o $G'^t$) y como vértice inicial `t`, así obtengo los caminos mínimos desde `t` hacia todo el resto de vertices de G'.
- Itero sobre todas las aristas negativas de G, sin perdida de generalidad las nombro $(w_1 \rightarrow w_2)$ y calculo cuanto es el peso final del camino minimo que pasa por esa arista, si es que existe, usando: ($d(s, w_1) + c(w_1 \rightarrow w_2) + d(w_2, t)$)
- Devuelvo el camino que tenga menor peso total.

### Correctitud
Veo que la solución optima del ejercicio es `min(peso del recorrido que no pasa por ninguna arista negativa (P_{sin}), peso del recorrido que pasa por 1 arista negativa (P_{con}))`.
Mientras que el algoritmo devuelve $min(\underset{camino\ minimo\ sin\ pesos\ negativos,\ P'_{sin}}{\underbrace{d(s,t)}},\underset{camino\ minimo\ con\ un\ peso\ negativo,\ P'_{con}}{\underbrace{d(s, w_1) + c(w_1 \rightarrow w_2) + d(w_2, t)}} |\ w_1 \rightarrow w_2 \ arista\ negativa)$  
Veo que trivialmente $P_{sin}$ y $P'_{sin}$ son lo mismo, ya que el primero viene de la implementación de lo segundo. 
Luego, para ver que $P_{con} = P'_{con}$ veo que $P_{con} \leq P'_{con}$ y $P_{con} \geq P'_{con}$ 
### $P_{con} \leq P'_{con}$ 
En $P'_{con}$ tengo los caminos mínimos de `s` a $w_1$ y de $w_2$ a `t`, agregando a la vez una arista negativa $w_1 \rightarrow w_2$, por lo que puedo decir que $P'_{con} \subseteq P_{con}$, luego gracias a eso puedo decir que $P_{con} \leq P'_{con}$, ya que el hecho de que $P'_{con}$ este contenido en $P_{con}$ me dice que el minimo de $P_{con}$ es al menos tan chico como el de $P'_{con}$, que tiene menos elementos.
### $P_{con} \geq P'_{con}$ 
Como $d(s, w_1)$ es el camino minimo de `s` al vértice $w_1$, $d(w_2, t)$ el camino minimo de $w_2$ al vértice `t`, y todas las aristas nombradas como $(w_1 \rightarrow w_2)$ son negativas, tengo que $min(d(s, w_1) + c(w_1 \rightarrow w_2) + d(w_2, t)) \leq min( Pesos\ de\ los\ caminos\ minimos\ con\ una\ arista\ negativa)$, que es lo mismo que $min(P'_{con}) \leq min(P_{con})$

# Ejercicio 4 🧱 la demo
![[Screenshot 2025-10-28 at 14.56.09.png]]
- Dijkstra desde `s` en G.
- Dijkstra desde `t` en $G^t$.
- Para cada arista $e = (w_1 \rightarrow w_2) \in E ∉ E(G)$ veo si $$d_{G+e} = d(s, w_1) + c(w_1 \rightarrow w_2) + d(w_2, t) \lt d_G(s, t)$$
# Ejercicio 5 🧱 la demo y consultar el algoritmo
![[Screenshot 2025-10-28 at 14.56.16.png]]
- Dijkstra desde `s` en G.
- Dijkstra desde `t` en $G^t$.
- Para cada arista $e = (w_1 \rightarrow w_2) \in E ∉ E(G)$ veo si $$d_{G+e} = d(s, w_1) + c(w_1 \rightarrow w_2) + d(w_2, t) = d_G(s, t)$$
- Con cada una de las aristas que lo cumplan, armo un nuevo grafo G' que seria el "grafo de caminos mínimos"
- Para cada arista (v, w) de dicho grafo, veo si no existe otro camino que vaya de v a w y que tenga menor peso, si no lo hay, es critica.
# Ejercicio 6 🧱
![[Screenshot 2025-10-28 at 14.56.22.png]]

# Ejercicio 7 🧱 buscar item c
![[Screenshot 2025-10-28 at 14.56.34.png]]
## a)
Nodos como cabinas, aristas positivas como peajes comunes y aristas negativas como peajes inversos.
## b)
Agrego un nodo fantasma a todos los vertices del grafo con peso 0 y corro Bellman-Ford desde dicho nodo. Luego el algoritmo de Bellman-Ford con la modificacion vista en la teórica detecta si hay o no ciclos negativos. 
## c)

# Ejercicio 8 🧱
![[Screenshot 2025-10-28 at 14.56.42.png]]
orden topologico
# Ejercicio 9 ✅
![[Screenshot 2025-11-05 at 11.08.59.png]]
## a)
Los vertices del grafo son las distintas n monedas diferentes y las aristas $v_i \rightarrow v_j$ es el tipo de cambio que hay de la moneda $i$ para pasar a la moneda $j$.
Por la consigna ademas defino al peso de la arista $v_i \rightarrow v_j$ como $-log(r_{ij})$, siendo $r_{ij}$ el numero por el que se multiplica una cantidad de moneda $i$ en moneda $j$. Puede ser menor que 1, pero no menor que 0.
Ejemplo de esto ultimo: si un dólar son 1400 pesos, la arista $dolar \rightarrow peso$ tiene peso, valga la redundancia, 1400.
En este modelo, el hipotético arbitraje se veria como un ciclo $v_1, v_2, ..., v_k, ..., v_1$ tal que el producto de sus aristas sea mayor que 1. 
Por GPT tengo la siguiente relación:
$$
\prod r_{ij} \gt 1 \Longleftrightarrow \sum -log(r_{ij}) \lt 0
$$
## b)
Tomando lo anterior, hay arbitraje si y solo si hay un ciclo negativo, Bellman-ford viene bien acá. 
Agrego un "nodo fantasma" al grafo y lo conecto con todos los otros nodos a peso 0. Corro Bellman-Ford desde ese nodo fantasma. Si hay un ciclo/arbitraje lo va a detectar. 
## c)
La complejidad estándar de Bellman-Ford de `O(n.m)`, ya que agregar el nodo fantasma me cuesta `O(n)`, por lo que domina la primer complejidad.
# Ejercicio 10 ✅
![[Screenshot 2025-11-05 at 11.09.07.png]]
![[Screenshot 2025-11-05 at 11.09.12.png]]
## a)
Los nodos son puntos en el mapa sin nada particular, y las aristas ponderadas $v_i \rightarrow v_j$ según si el robot gasta energía en dicha arista, o si gana energía.
## b)
La condición que lo garantiza es el hecho de que el robot pueda almacenar infinita energía. Significa que si encuentra un ciclo de peso negativo alcanzable tanto desde `s` como desde `t`, no esta definida realmente la cantidad máxima de energía con la que puede llegar 
## c) preguntar mi idea
El problema acá estaría en ver si hay algún ciclo negativo alcanzable tanto desde `s` como desde `t`, cosa de que un camino desde `s` pase por el ciclo negativo para llegar a `t` e indefina el problema de camino minimo.

Bellman-Ford desde `s`. Si no detecta ciclos negativos, devolver el camino minimo entre `s` y `t`. En cambio, si detecta un ciclo negativo, separo los vertices involucrados del mismo, invierto la orientación de las aristas y corro Bellman-Ford desde `t`, si encuentra un ciclo negativo, lo separo y comparo con el ciclo negativo encontrado antes. Si son iguales, significa que el ciclo es alcanzable tanto desde `s` como `t`, por lo que el problema de camino minimo no estaría bien definido. Si por el contrario no son iguales, significa que un camino desde `s` no puede pasar por dicho ciclo negativo y llegar a `t`, por lo que en este caso el problema si esta bien definido. 
Complejidad: `O(n.m) + O(n + m) + O(n.m) = O(n.m)`

La idea de GPT fue hacer BF desde `s`, y si detecta un ciclo negativo, separar los vertices del mismo, invertir el grafo, y hacer DFS/BFS desde `t` para ver si alcanza alguno de ellos. 
Complejidad: `O(n.m) + O(n+m) + O(n+m) = O(n.m)`
# Ejercicio 11 ✅
![[Screenshot 2025-11-05 at 11.09.19.png]]
Este ejercicio no vi antes que si asumo que es DAG, puedo usar Topological Sort + DP con `O(n+m)`.
## a)
Sea G el grafo inicial:
- Multiplico el peso de todas las aristas por -1(quiero el camino que maximice el puntaje, el equivalente a camino minimo con pesos invertidos). 
- Obtengo G' quitando todas las aristas "especiales", pero separándolas y dejándolas a mano. 
- Bellman-Ford desde el nivel 1.
- Traspongo el grafo y Bellman-Ford desde el nivel n
- Itero sobre las aristas especiales y calculo el camino minimo entre el nivel 1 y el nivel n que pasa por dicha arista, es decir: $d(1, n) = d(1, v) + p(v \rightarrow w) + d(w, n)$
- Devuelvo el minimo entre $d(1, n)$ sin aristas especiales y $d(1, n)$ con una arista especial.
## b)
Cuando en el grafo ya con los pesos invertidos hay ciclos negativos, o en el normal ciclos positivos.
Bellman-Ford ya detecta ciclos negativos.
## c)
- Multiplico por -1 los pesos.
- Bellman-Ford desde nivel 1.
- Si encuentra ciclo negativo, separo los nodos involucrados y para cada uno hago DFS/BFS para ver si desde uno de ellos consigo llegar a nivel n.
# Ejercicio 12 ✅
![[Screenshot 2025-11-05 at 11.09.25.png]]
## a)
- Multiplico por -1 los pesos de las aristas.
- BF sobre s. Si encuentra un ciclo negativo, separa los vertices de dicho ciclo y hace DFS/BFS sobre el grafo traspuesto en `t` para ver si alguno alcanza a t. Si alguno lo alcanza, entonces existe dicho recorrido.
## b)
Idem ítem a.
## c)
`O(n.m) + O(n + m) + O(n + m) = O(n.m)` 
# Ejercicio 13 🧱
![[Screenshot 2025-11-05 at 11.09.32.png]]
![[Screenshot 2025-11-05 at 11.09.46.png]]
## a)

## b)

## c)

## d)

# Ejercicio 14 🧱
![[Screenshot 2025-11-05 at 11.09.54.png]]
## a)

## b)

## c)

## d)
# Ejercicio 15 (ex 9) ✅
![[Screenshot 2025-10-28 at 14.56.50.png]]
El grafo tiene `n` vertices, `m` aristas, el peso de cada arista $(u, v)$ esta acotado por una constante particular para esa arista.
## a)
Lo pruebo por contradicción. Asumo que D(S) tiene un ciclo de peso negativo y que tiene una solución y trato de llegar a un absurdo. 
Sea C el ciclo del grafo como $x_1, x_2, ..., x_k$, tengo que la primer arista del ciclo tiene como peso $x_1 - x_2$, la segunda $x_2 - x_3$ y así. Luego el propio ciclo se "interpreta" como la suma de sus aristas, y tomando la representación de las mismas, pasa que se cancelan todos los términos quedando un 0. Luego, como esta suma debe ser menor o igual a la suma de las constantes $c_{ij}$ para todo i, j en rango, suma que estoy asumiendo que es negativa. El absurdo viene ahí, de llegar a que $\sum_{ij = 0}^{n}C \lt 0$ por hipótesis, y que $0 \leq \sum_{ij = 0}^{n}C$ por desarrollo. 
## b)
$$
d(v_0, v_i) \leq d(v_0, v_j) + w(v_j, v_i)
$$
$$
d(v_0, v_i) - d(v_0, v_j) \leq w(v_j, v_i)
$$
Igualo $x_i = d(v_0, v_i)$ y $x_j = d(v_0, v_j)$ y cumple con la inecuacion de la consigna. 

## c)
Bellman-ford para obtener las distancias mínimas desde $v_0$. Si hay un ciclo negativo, lo devuelve y desde el recupero las inecuaciones contradictorias. 
# Ejercicio 16 🧱 
![[Screenshot 2025-11-05 at 14.53.12.png]]

# Ejercicio 17 🧱
![[Screenshot 2025-10-28 at 14.57.35.png]]
# Ejercicio 18 🧱
![[Screenshot 2025-10-28 at 14.57.43.png]]
![[Screenshot 2025-10-28 at 14.57.50.png]]
# Ejercicio 19 🧱
![[Screenshot 2025-10-28 at 14.58.09.png]]
![[Screenshot 2025-10-28 at 14.58.20.png]]
# Ejercicio 20 ✅+-
![[Screenshot 2025-10-28 at 14.58.27.png]]
Asumiendo que M ya es cuadrada, simétrica y positiva(las corroboraciones de eso se las dejo a algoritmos de ALC), verifico que en la diagonal tenga solo 0's. Y que para todo elemento no nulo de la matriz, $M[i][j] \leq M[i][k] + M[k][j]$(desigualdad triangular).  
# Ejercicio 21 ✅
![[Screenshot 2025-10-28 at 14.58.35.png]]
- Floyd-Warshall en D
- Creo un vector `mVec` de aristas
- Itero sobre las aristas (v, w) de D:
	- Reviso si para cada par de nodos (s, t) de D se cumple que $FW[s][t] == FW[s][v] + c(v, w) + FW[w][t]$, si es el caso, $mVec[vw]++$
- Devuelvo el máximo del vector `mVec`.
# Ejercicio 22 ✅
![[Screenshot 2025-10-28 at 14.58.41.png]]
- Floyd-Warshall para la estructura de distancias mínimas. 
- Creo un arreglo de "cubiertos" de tamanio |V|.
- Itero sobre las aristas.
- Tomo la arista (u, v) y calculo d = $dist[u][v]$
- Itero sobre los vertices, si el vértice x cumple con que $dist[u][x]$ = d, entonces marco cubiertos[x] = true
- Al final, si hay algún false, entonces el grafo no es geodésico. 

# Ejercicio 23 🧱 pero visto
![[Screenshot 2025-10-28 at 14.58.49.png]]

# Ejercicio 24 🧱
![[Screenshot 2025-10-28 at 14.59.01.png]]

# Ejercicio 25 🧱
![[Screenshot 2025-10-28 at 14.59.07.png]]
![[Screenshot 2025-10-28 at 14.59.13.png]]

# Ejercicio 26
![[Screenshot 2025-10-28 at 14.59.21.png]]
## a)
Ralo: BFS con lista de adyacencia. $O(n + m)$
Denso: BFS con matriz de adyacencia. $O(m^2)$
## b)
Ralo: BFS con lista de adyacencia, corriéndolo desde todos los vertices. $O(n . (n + m))$
Denso: Floyd-Warshall. $O(n^3)$
## c)
Ralo: Dijkstra con cola de prioridad. $O((n + m) . log(n))$
Denso: Dijkstra trivial.
## d)
Ralo: Dijkstra con cola de prioridad, corriéndolo desde todos los vertices. $O(n . ((n + m) . log(n)))$
Denso: Floyd-Warshall. $O(n^3)$
## e)
Ralo: Bellman-Ford. $O(n^2)$
Denso: Floyd-Warshall, revisando los valores de la diagonal. $O(n^3)$
## f)
Ralo: Kruskal o Prim. $O(m . log(n))$
Denso: Prim con matriz de adyacencia. $O(n^2)$
## g)
Ralo: Kruskal o Prim
Denso: Prim con matriz de adyacencia
# Ejercicio 27
![[Screenshot 2025-10-28 at 14.59.29.png]]
![[Screenshot 2025-10-28 at 14.59.36.png]]
## a)
Idea similar al ejercicio 2/b del taller 3. 
La relajación es de la siguiente forma:
$$
d[v] = min(d[v], max(d(u), s(u \rightarrow v)) + t(u \rightarrow v))
$$ 

## b)

## c)

