n := |V| := cantidad de nodos del grafo G
m := |E| := cantidad de aristas del grafo G
N(v) := vecindario del nodo v
d(v) := |N(v)| = grado del nodo v

## Demos sobre grafos
### Ejercicio 1
Probar que en todo grupo de dos o mas personas hay por lo menos dos de ellas que tienen la misma cantidad e amigos en el grupo.

Grafo = grupo de personas donde cada nodo representa una persona, y una arista una amistad. 

`#`amigos(p) = $|N_G(p)| = d_G(p)$
$\forall G \  /  \ |v(G)| \geq 2$ $\Rightarrow$ $\exists u,v \in V(G) / d_G(u) = d_G(v)$
Sea $v \in V(G), \ 0 \leq d(v) \leq n-1$, 

Lo pruebo por el absurdo.
Asumo que los n nodos del grafo tienen grado distinto, por ende $\forall v, w \in G \ / \ v \neq w \land d(v) \neq d(w)$.
Como el rango de posibles grados "g" para un nodo es $0 \leq g \leq n-1$, le voy colocando valores distintos a los n nodos del grafo, el absurdo llega cuando resulta que tengo un nodo que tiene grado 0, y otro n-1, cosa que, valga la redundancia, es **absurdo**!.

Todo grafo se mueve en estos escenarios:
- $0 \leq d(v) \leq n-2$
- $1 \leq d(v) \leq n-1$
Esto anterior sale de ver que si $\exists v \in V(G) / d_G(v) = 0 \Rightarrow \nexists u \in V(G) \ / \ d_G(u) = n-1$  

### Ejercicio 2 
Sean P y Q dos caminos distintos de un grafo G que unen un vertice v con otro w. Demostrar en forma directa que G tiene un ciclo cuyas aristas pertenecen a P o Q.
