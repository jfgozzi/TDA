# Ejercicio 1 ✅
![[Screenshot 2025-10-18 at 17.03.43.png]]
## a)
Lo que dice es que si existe una arista `vw` en el conjunto de aristas que queda de tomar el conjunto total de aristas de G restandole las aristas de T, los vértices `v` y `w` o están a una distancia par de la raíz, o están a una distancia impar, entonces el único ciclo en el grafo $T \cup \{ vw \}$ es de longitud impar.

Me lo creo. Si `v` y `w` están a una distancia par de `r`, entonces agregar la arista $\{ vw \}$ a T crea un ciclo impar (siendo par la distancia, tiene forma de 2x para algún x, entonces la longitud del ciclo va a ser la suma de dos distancias pares, mas 1). Y si `v` y `w` están a una distancia impar, entonces agregar la arista $\{ vw \}$ a T también crea un ciclo impar (la suma de dos números impares siempre es par, luego al sumarle 1 por la arista $\{ vw \}$ termina quedando impar).
## b)
Lo que dice es que si toda arista que queda de restar al conjunto de todas las aristas de G, el conjunto de aristas de T, une un vértice de V con otro de W, entonces (V, W) es una biparticion de G, y por lo tanto G es bipartito.

Me lo creo, T ya es bipartito por naturaleza, no hay aristas entre "hermanos", "abuelo-nieto", etc. Si ademas me das que las aristas que no entraron al árbol también cumplen con que conectan vértices de los conjuntos, entonces nunca se rompe la bipartitud.
## c)
- Tengo el grafo base
- Hago DFS para conseguir el arbol, y con una modificacion al propio algoritmo separo en grupos "par" e "impar" a los vértices que estén a la distancia respecto a la raíz que corresponda. Tambien separo en otro conjunto las aristas que van entrando al arbol.
- Ya con el arbol, obtengo el conjunto de aristas que no entraron al arbol. Lo llamo `rezagadas`.
- Recorro el conjunto `rezagadas` chequeando que los vértices que están conectados por dicha arista pertenezcan a grupos distintos (de las distancias respecto a la raíz del arbol), si alguna cumple con que sus vertices están en el mismo conjunto, entonces directamente devuelvo el ciclo impar de G que contiene esa arista. Mientras no pase eso, itero sobre las `rezagadas`, cuando me quede sin aristas, entonces resulta que G era bipartito, por lo que retorno cualquiera de los conjuntos de vertices que separe en el DFS.
## d)
Generalizando lo anterior, simplemente luego de cada DFS veo si queda algún vértice sin visitar. De ser así, el grafo no es conexo, por lo que haciendo eso me aseguro que se vean todas las componentes conexas. Si alguna de ellas tiene un ciclo impar, G directamente no es bipartito e igual que antes, reconstruyo el ciclo impar a partir de la arista que cumple con esa condición. 

# Ejercicio 2 ✅
![[Screenshot 2025-10-18 at 17.04.44.png]]
## a)
### $\Longrightarrow$
Asumo que `vw` es un puente de G y quiero probar que `vw` no pertenece a ningún ciclo de G. 
Como `vw` es una arista puente, puedo decir que `v` esta en una componente conexa V, y `w` en otra W. Tambien puedo decir que como G es conexo, todo camino que conecte un vértice de V con otro de W pasa por la arista `vw`. 
Voy a asumir que `vw` esta en un ciclo y voy a llegar a una contradicción. Como `vw` pertenece a un ciclo, puedo decir que hay un camino simple que empieza en `v`, usa la arista `vw` y termina tambien en `v`. Por lo dicho antes, si el camino empieza en el vértice `v`, puedo decir que empieza en la componente conexa V, luego dicho camino pasa a `w`, que esta en la componente conexa W, y eventualmente vuelve a `v`, cosa que quiere decir que existe una arista en dicho camino distinta de `vw` que conecta algún vértice con `v`, pero que en algún momento hace que el recorrido del camino pase de la componente conexa W a la componente V, cosa que genera conflicto con lo que asumí al principio, eso de que `vw` es una arista puente de G. En este planteo existe por lo menos una mas.
### $\Longleftarrow$
Asumo que `vw` no pertenece a ningún ciclo de G y quiero probar que `vw` es un puente de G.
Que `vw` no pertenezca a ningún ciclo significa que no hay ningún camino simple que empiece en `v`, siga por `w` y que pase (o no) por otros vertices hasta volver a llegar a `v`. 
Que `vw` no pertenezca a ningún ciclo tambien hace que estrictamente la remoción de dicha arista elimine cualquier conexión entre el vértice `v` y el `w`, haciendo que G se parta en 2 componentes conexas,
## b)
Asumo que $vw \in E(G) / E(T)$ y quiero probar que `v` es un ancestro de `w` en T o viceversa.
Como para que una arista este en el conjunto $E(G) / E(T)$ tiene que pasar que durante el DFS, al revisar el vecindario de un vértice se encuentre con otro que ya haya visitado antes. Entonces, que `vw` este ahí, significa que mientras que revisaba el vecindario de `v`, se vio que `w` ya había sido recorrido por el algoritmo (o al revés), por lo que en el arbol, al haber sido descubierto antes, `w` queda por encima de `v`.
## c)
Tengo que `vw` aparece en el arbol.
### $\Longrightarrow$
Asumo que `vw` es puente y quiero probar que `v` es padre de `w` en T y que ninguna arista $G / \{ vw\}$ une a un descendiente de `w` (o a `w`) con un ancestro de v (o a `v`).
Tengo que `vw` en G es un puente y que en el arbol DFS el nivel de `v` es menor (o igual, yo asumo que menor) que el de `w`, por lo que seria ancestro a la fuerza, mas específicamente padre, ya que la arista `vw` existe.
Ademas, el asumir que `vw` es una arista ya rompe con cualquier posibilidad de que exista una arista que conecte un ancestro de `v` con un descendiente de `w`, no puede pasar eso a la vez de que `vw` sea puente.
### $\Longleftarrow$
Asumo que `v` es padre de `w` en T y que ninguna arista $G / \{ vw\}$ une a un descendiente de `w` (o a `w`) con un ancestro de v (o a `v`), y quiero probar que `vw` es puente.
Lo que estoy asumiendo sobre $G / \{ vw\}$ hace que estrictamente `vw` sea un puente. Fuerza a que todo camino entre vertices ancestros de `v` en T y descendientes de `w` en T pase por la arista `vw`, cumpliendo con la definición de puente.
## d)
Formula para ver cuantas backedges cubren la arista que va entre un vértice y su padre:
$$
cubren(v) = backEdgesConExtremoInferiorEn(v) - backEdgesConExtremoSuperiorEn(v) + \sum_{w\in hijos(v)}cubren(w)
$$
Algoritmo visto en clase. Los puentes son aquellos vertices que su "cubren" es 0. Si G no fuera conexo, se restan la cantidad de componentes conexas a la cantidad de puentes conseguida antes.

# Ejercicio 3 🤨
![[Screenshot 2025-10-18 at 17.04.57.png]]
![[Screenshot 2025-10-18 at 17.05.06.png]]
## a)
Ok.
## b) preguntar
### I) $\Longrightarrow$ II)
Que G admita una orientación fuertemente conexa significa que en D, para todo par de vértices `v, w` existe un camino dirigido que va de uno al otro. 
Asumo que G tiene puentes.
Como G tiene un puente, quiere decir que la remoción de dicha arista parte al grafo en 2 componentes conexas, sin embargo al aplicarle una dirección al grafo en ese contexto, va a pasar que no van a haber caminos dirigidos entre los vertices de las dos "componentes conexas", como hay solo una arista que esta conectando dichas componentes, al aplicarle dirección solo hay caminos que van de un lado para el otro, pero no viceversa, lo que contradice el hecho de que G admita una orientación fuertemente conexa.


### II) $\Longrightarrow$ III) PREGUNTAR


### III) $\Longrightarrow$ IV)
trivial (?
### IV) $\Longrightarrow$ I) PREGUNTAR 
## c) revisar
- Hacer DFS en un vértice arbitrario
- Para cada vértice `v` que este mirando el DFS, al momento de revisar su vecindario, si el vértice `w` de dicho vecindario ya fue visitado, a esa arista se le da la orientación $w \rightarrow v$, si es un vértice no visitado, se le da $v \rightarrow w$. 

# Ejercicio 4 ✅
![[Screenshot 2025-10-18 at 17.05.17.png]]
- El grafo (ciudad) es conexo de base, y se quiere mantener así.
La idea seria dejar bidireccional únicamente las aristas que son puentes, el resto con el algoritmo del 3c le doy una orientación al resto de aristas. 
- Identificar aristas puente. `O(n+m)`
- Armar un subgrafo $G / \text{aristas puente}$
- Sobre el nuevo grafo anterior, como es conexo, correr el algoritmo del ejercicio 3c para darles una orientación.
- Luego mergear las aristas puente bidireccionales y el grafo disconexo orientado.
# Ejercicio 5 ✅
![[Screenshot 2025-10-18 at 17.05.27.png]]
Que un grafo G sea `v-geodesico` significa que la distancia entre el vértice v y un vértice `w` de G arbitrario es la misma que tienen en el arbol BFS de G.
La demo principal es trivial respecto a como funciona BFS.
# Ejercicio 6 ✅ A MEDIAS
![[Screenshot 2025-10-18 at 17.05.37.png]]
- Primero con una modificacion de BFS obtengo la distancia mínima que hay de `v` a todos los vertices del grafo. 
- Luego empiezo a construir el arbol, me voy quedando con las aristas que cumplan que la distancia mínima entre el vértice `v`  cada uno de los otros vertices del grafo sea igual a la suma de la distancia mínima de `v` con otro vértice `x`, mas el peso de la arista elegida, que va del vértice elegido hacia `x` y forma parte del camino mínimo entre `v` y dicho vértice, asegurando lo de ser v-geodésico.

# Ejercicio 7 ❌
![[Screenshot 2025-10-18 at 17.05.47.png]]
![[Screenshot 2025-10-18 at 17.05.55.png]]
## a)
## b)
## c)
## d)
# Ejercicio 8 ✅
![[Screenshot 2025-10-18 at 17.06.07.png]]
Modelado: Se crea un grafo donde cada vértice representa uno de los huecos de la matriz, los vertices adyacentes a cada vértice son los huecos que justamente son adyacentes a uno en la matriz. Pero ademas, para cada vértice al que se pueda mover, hay k nodos que representa cada uno de los posibles resultados del estado $v_{i+1} = (v_i + z)\  mod\  k$, por lo que hay O(nmk) vertices.
Luego, corriendo BFS para encontrar el camino mas corto que obtenga lo buscado.
# Ejercicio 9 ❌
![[Screenshot 2025-10-18 at 17.06.16.png]]

# Ejercicio 10 ❌ 
![[Screenshot 2025-10-18 at 17.06.28.png]]
Modelo: Cada nodo es una habitación, y cada arista dirigida (u, w) conecta la habitación u con la habitación w ya que los interruptores de u encienden y apagan las luces de w. (?
# Ejercicio 11 ✅
![[Screenshot 2025-10-18 at 17.06.39.png]]
### Modelo
Grafo completo donde cada nodo representa uno de los conjuntos, todos los nodos están conectados con todos por aristas ponderadas con el resultado de la distancia entre las secuencias que representan.
Armar dicho grafo cuesta `O(k)` por computar cada distancia/arista, y hay O($\frac{n.(n-1)}{2}$) = O($n^2$) aristas, por lo que queda un total de O($kn^2$) armar el grafo.
Luego quedaría obtener el arbol generador mínimo del grafo armado, con Prim en O($n^2$) lo obtengo.
Complejidad final: O($kn^2 + n^2 = kn^2$).
# Ejercicio 12 ✅
![[Screenshot 2025-10-18 at 17.07.02.png]]
![[Screenshot 2025-10-27 at 10.42.53.png]]
## a)
Tengo que buscar el la ponderación mínima k que pueda remover de G tal que G / {aristas de k o menos peso} siga siendo conexo.  
- Ordeno de forma creciente las aristas por peso
- Usando búsqueda binaria, voy obteniendo un peso k
- Elimino de G las aristas con ese peso y corro DFS para ver si es conexo
	- Si lo es, separo ese valor k como posible resultado, y sigo la búsqueda binaria con la mitad derecha del arreglo
	- Si no lo es, busco en la izquierda.

Otra idea mejor, creo.
- Le cambio de signo a todas las aristas
- Corro Prim, o Kruskal para obtener el AGM de eso, y veo el peso de la arista mas grande.
- Le cambio el signo a dicho peso y concluyo que ese es el ancho de banda.
## b)
Parecido al inciso a), solo que para cada "i" del vector resultado, lo que hago es reemplazar esa cantidad de aristas, comenzando siempre por las de menor peso de G, y corro el mismo algoritmo del inciso a), ligeramente adaptado para soportar aristas de peso infinito.
# Ejercicio 13 🧱
![[Screenshot 2025-10-18 at 17.07.13.png]]
## $\Longrightarrow )$ 
Asumo que T es un arbol maximin de G, y quiero probar que T es un AGM de G.
Que T sea un arbol maximin significa que para todo par de vertices de T, la arista de menor peso del camino que los conecta es la mas grande posible de las que podrían haber sido partiendo del grafo G. 
Asumo que el consecuente es falso y trato de llegar a una contradicción.
Como T no es un arbol generador máximo de G, quiere decir que existe otro arbol T' que si que es arbol generador máximo de G. Tomando dicho T' tengo que para todo par de vertices, la suma de los pesos de dichas aristas es la máxima posible tomando como base el grafo G. 
Como T y T' tienen los mismos vertices, tomo un par arbitrario de vertices y comparo los caminos entre ellos en los dos arboles.

Tomo el T' que mas aristas en común tenga con T, asumo tambien que existe una arista $e \in T$ tal que e ∉ T', y tambien existe una arista e' tal que $e' \in T'$ y e' ∉ T. Dichas aristas conectan los dos mismos vertices en ambos arboles.

## $\Longleftarrow )$ 
Asumo que T es un AGM de G, y quiero probar que T es un arbol maximin de G.



# Ejercicio 14 🧱 
![[Screenshot 2025-10-18 at 17.07.30.png]]
## a)

## b)
Asumo que los pesos del grafo G son todos distintos, y quiero probar que G tiene un único arbol generador mínimo.
Como G tiene todos los pesos distintos, en cada iteración del algoritmo de armado de AGM que se este usando se va a estar agarrando la arista mínima que conecte un vértice no visto aun, ya que como no hay coincidencias de pesos, no hay selección de aristas en base a prioridades, por lo que la elección queda reducida al peso mas chico que haya, cosa que ya Prim o Kruskal hacen de base.
# Ejercicio 15 ❌
![[Screenshot 2025-10-18 at 17.07.38.png]]
## $\Longrightarrow )$ 


## $\Longleftarrow )$ 

# Ejercicio 16 ❌
![[Screenshot 2025-10-18 at 17.07.51.png]]
# Ejercicio 17 ❌
![[Screenshot 2025-10-18 at 17.08.01.png]]
![[Screenshot 2025-10-18 at 17.08.13.png]]
## a)
## b)
## c)
## d)
## e)
# Ejercicio 18 ❌
![[Screenshot 2025-10-18 at 17.08.24.png]]
## a)
## b)
## c)
# Ejercicio 19 ❌
![[Screenshot 2025-10-18 at 17.08.32.png]]
# Ejercicio 20 ❌
![[Screenshot 2025-10-18 at 17.08.39.png]]
## a)
## b)
## c)