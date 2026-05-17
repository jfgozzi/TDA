# Ejercicio 1 ✅
![[Screenshot 2025-10-05 at 10.52.34.png]]
Como pide inducción, asumo que P (proposición) para todo grafo de n-1 aristas vale que:
$$
\underset{v \in V(D)}{\sum} d_{in}(v) = \underset{v \in V(D)}{\sum} d_{out}(v) = n-1
$$
Y pruebo que vale para n.
### Caso base: P(0)
Con 0 aristas, como ningún nodo tiene aristas de entrada ni de salida, entonces:
$$
0 =\underset{v \in V(D)}{\sum} d_{in}(v) = \underset{v \in V(D)}{\sum} d_{out}(v) = 0 
$$
Se cumple el caso base.
### Hipótesis inductiva
$$
P(n-1): |E(D)| = n-1 = \underset{v \in V(D)}{\sum} d_{in}(v) = \underset{v \in V(D)}{\sum} d_{out}(v)
$$

### Paso inductivo: P(n)
Quiero ver que vale para P(n)
$$
P(n): |E(D)| = n = 1+n-1 \underset{HI}{=} 1 + \underset{v \in V(D)}{\sum} d_{in}(v) \underset{HI}{=} 1+\underset{v \in V(D)}{\sum} d_{out}(v)
$$
Luego, valen las igualdades.

# Ejercicio 2 ✅
![[Screenshot 2025-10-06 at 10.27.34.png]]
Lo pruebo por el absurdo.
Asumo que los n nodos del grafo tienen grado distinto, por ende $\forall v, w \in G \ / \ v \neq w \land d(v) \neq d(w)$.
Como el rango de posibles grados "g" para un nodo es $0 \leq g \leq n-1$, le voy colocando valores distintos a los n nodos del grafo, el absurdo llega cuando resulta que tengo un nodo que tiene grado 0, y otro n-1, cosa que, valga la redundancia, es **absurdo**!.

Todo grafo se mueve en estos escenarios:
- $0 \leq d(v) \leq n-2$
- $1 \leq d(v) \leq n-1$
Esto anterior sale de ver que si $\exists v \in V(G) / d_G(v) = 0 \Rightarrow \nexists u \in V(G) \ / \ d_G(u) = n-1$  

# Ejercicio 3 ✅
![[Screenshot 2025-10-05 at 10.52.54.png]]
Planteo que existe un grafo de $n$ vértices, los cuales tienen todos grado de salida distintos. Los mismos pueden ordenarse como $d_{out}(v_1) \lt ... \lt d_{out}(v_n)$. Luego, como son $n$ vértices, el rango de posibles valores de grado de salida va de entre 0 y $n-1$, y aquel que tenga grado de salida $n-1$ va tener grado de entrada 0, ya que va a tener una arista existente $v_i \rightarrow v_j$, impidiendo que haya una  $v_j \rightarrow v_i$. Con esto claro, es viable asegurar que $d_{out}(v_i)=i-1$ y que $d_{in}(v_i) = n-i$, ya que las "aristas de salida" de un nodo siempre van a parar a otro que las a tomar como "de entrada". 
Finalmente, el único grafo que cumple con esto es un grafo que tenga todos sus nodos `universales`, osea un grafo `completo`.
# Ejercicio 4 ✅ ❌ ❌
![[Screenshot 2025-10-05 at 10.53.25.png]]
![[Screenshot 2025-10-05 at 10.53.33.png]]
### a)
Quiero probar que si un grafo tiene `n` vértices y mas de $\frac{(n-1)(n-2)}{2}$ aristas, el grafo es conexo.
#### Caso base
Si n = 1, entonces es imposible que tenga mas de $\frac{(1-1)(1-2)}{2} = \frac{0.-1}{2} = 0$ aristas, por lo que se falsea en antecedente y la implicación es verdadera. 
#### Paso inductivo 
Como hipótesis inductiva planteo que todo grafo de `n` vértices con mas de $\frac{(n-1)(n-2)}{2}$ aristas es conexo. Y quiero ver que se cumple también para grafos de `n+1` vértices y mas de $\frac{(n)(n-1)}{2}$ aristas. 
Sea G es grafo con el que estoy trabajando, para acomodar la hipótesis inductiva al caso que estoy manejando, quito un vértice v junto con todas las aristas que tiene conectadas y veo como queda. Como no es posible que tenga grado 0, ya que falsearía el consecuente, si tiene grado 1 me queda que G/{v} tiene n vértices y $\frac{(n)(n-1)}{2}-1$ aristas, que es mas que $\frac{(n-1)(n-2)}{2}$, por lo que cumple la implicación. 
Luego, haciendo la desigualdad se ve que el grado máximo posible que se puede quitar del grafo para mantenerlo conexo es de `n-2`. Igualmente, tratar de quitar uno con grado `n-1` no hace falta, ya que su mera existencia haría conexo al grafo desde el principio. 

### b)

### c)

# Ejercicio 5 📖 hecho en clase
![[Screenshot 2025-10-05 at 10.53.42.png]]
# Ejercicio 6 ✅
![[Screenshot 2025-10-05 at 10.53.49.png]]
Igual que el ejercicio 2.
# Ejercicio 7 ✅
![[Screenshot 2025-10-05 at 10.53.56.png]]
Contrarrecíproco: $P \Rightarrow Q \text{ es igual a } \neg Q \Rightarrow \neg P$   
Entonces, asumo $\neg Q$, osea que hay un par de caminos que no comparten ningún vértice, estando en un grafo conexo, y quiero probar que al menos uno no tiene la longitud máxima posible.
Supongo que hay dos caminos $P_1$ y $P_2$ disjuntos de longitud l máxima en G. Como G es conexo, existe un camino intermedio entre cualquier par de vértices, por lo que puedo plantear un nuevo camino $P_3$ que va desde el primer vértice de $P_1$ hacia el ultimo de $P_2$ pasando por la mayor cantidad de vértices intermedios de $P_1$ y $P_2$ posibles. En esa tesitura, $P_3$ tendría longitud l + l + $|P_3|- l - l$, donde los primeros dos términos vienen de asumir que $P_3$ pasa por todos los vértices de $P_1$ y $P_2$, y el ultimo de los vértices "únicos" de $P_3$ para conectar los primeros dos caminos, ya que son disjuntos.
Queda entonces que el $P_3$ planteado es mayor en longitud que $P_1$ y $P_2$.

# Ejercicio 8 ✅
![[Screenshot 2025-10-05 at 10.54.04.png]]
### a)
#### $\Longrightarrow)$
Asumo que G es un grafo union y quiero probar que G es disconexo.
Como G es union, existen dos grafos $G_1$ y $G_2$ disjuntos con los que, al hacer una union disjunta, sin agregar aristas, con ellos se obtiene G. Como quiero ver que G es disconexo, veo el caso en el que $G_1$ y $G_2$ sean conexos por separado, ya que si alguno de los dos es de base disconexo, G también lo es por transitividad.
Sea $G_1$ conexo con vértices $\{ v_1, v_2, ..., v_n \}$ y $G_2$ conexo con vértices $\{ w_1, w_2, ..., w_n \}$, en $G_1$ puedo obtener un camino entre cualquier par de vértices ya que hay una arista que conectan los vértices intermedios necesarios para ello. Si luego le agrego los vértices de $G_2$, si bien para cualquier par de vértices de $G_2$ hay un camino posible, entre un $v_i$ y $w_i$ arbitrarios no va a haber un camino posible, ya que únicamente agregue vértices y no aristas, y como todos los vértices eran disjuntos, no hay "reutilizacion" de aristas, por lo que concluyo en que G es disconexo.

#### $\Longleftarrow)$ 
Asumo que G es disconexo y quiero probar que G es grafo union. Todo el siguiente planteo viene de que no se dice nada de la "conexitud" de los $G_1$ y $G_2$.
Como G es disconexo, puedo reescribirlo como la union disjunta de las componentes conexas que lo conforman (las que sean), quedando como $G = g_1 \cup g_2 \cup \ ... \ \cup g_n$. Luego planteo dos subgrafos de G como $G_1 = g_1 \cup g_2 \cup \ ... \ \cup g_{k-1}$ y $G_2 = g_k \cup g_2 \cup \ ... \ \cup g_n$ como dos agrupaciones de dichas componentes conexas. De esta forma consigo ver que G queda representado como la union disjunta de dos subgrafos disjuntos.

### b)
#### $\Longrightarrow)$
Asumo que G es un grafo junta, y quiero probar que $\overline{G}$ es un grafo union. 
Como G es un grafo junta, se que $G = G_1 + G_2$, tengo entonces que todo vértice de $G_1$ tiene un camino posible hacia cualquier otro de $G_2$, no es necesariamente conexo, pero esa condición si se cumple. Luego, a $\overline{G}$ le ocurre que tiene dos, por lo menos, componentes conexas claras, lo que defini  como $G_1$ y $G_2$, ya que ahora no hay aristas que conecten ningún vértice de uno con otro del otro. En este contexto, lo que quiero probar lo probé antes en el ítem $G\ disconexo \Longrightarrow \ G \ grafo \ union$.
#### $\Longleftarrow)$ ver como cerrarla
Asumo que $\overline{G}$ es un grafo union, y quiero probar que G es un grafo junta.
Que $\overline{G}$ sea union significa que $\overline{G} = \overline{G_1} \cup \overline{G_2}$, siendo esos subgrafos conjuntos de por lo menos una componente conexa del $\overline{G}$. Luego entonces, en G esos subgrafos ya no lo son, ya que se agregan todas las aristas posibles entre los vértices de ambos 
### c)
#### $\Longrightarrow)$

$G \ grafo \ junta \Longrightarrow \overline{G} \ grafo \ union \Longrightarrow \overline{G} \ grafo \ disconexo$ 
#### $\Longleftarrow)$ 
$\overline{G} \ grafo \ disconexo \Longrightarrow \overline{G} \ grafo \ union \Longrightarrow G  \ grafo \ junta$ 


# Ejercicio 9 ✅
![[Screenshot 2025-10-05 at 10.54.11.png]]
Sea P(n) lo que quiero probar:
### Caso base
P(2) = $G_2$ es el grafo completo con dos vértices. Como es completo y tiene dos vértices, el grado máximo es 1 y ambos vértices lo tienen. 

### Paso inductivo
Sea la hipótesis inductiva la siguiente:
$\forall m \lt n$ vale que $G_m = \overline{G_{m-1} \cup K_1}$ tiene un único par de vértices de igual grado.
Quiero probar que $G_n = \overline{G_{n-1} \cup K_1}$ tiene un único par de vértices de igual grado. 
Viendo como es que quedan los grados de los vértices al agregar un nuevo vértice y hacer su conjugado se ve que $\overline{d(v_i \cup K_1)} = n-1 -d(v_i)+1 = n - d(v_i)$, como estoy buscando que vértices comparten grado, veo que $\overline{d(v_i \cup K_1)} = \overline{d(2_i \cup K_1)} \Longleftrightarrow n-1-d(v_i)+1 = n-1-d(w_i)+1 \Longleftrightarrow d(v_i) = d(w_i)$, lo que se cumple únicamente si $v = w$ o si su grado era el mismo antes del conjugado.

# Ejercicio 10 ✅
![[Screenshot 2025-10-05 at 10.54.24.png]]
Quiero probar que todo grafo de `2n` vértices y mas de $n^2$ aristas tiene un triangulo. 
(HI): Asumo que todo grafo de `2n` vértices y mas de $n^2$ aristas tiene un triangulo.
(qvq): todo grafo de `2n+2` vértices y mas de $(n+1)^2$ aristas tiene un triangulo.

Caso base:
Para n=2 se cumple que, con 4 vértices y mas de 4 aristas haya un triangulo. 

Paso inductivo:
Como tengo un grafo de 2n+2 vértices en este grafo G, la idea seria quitar dos para acomodarlo a la hipótesis inductiva. Sea G' el grafo que queda de G luego de tomar una arista (x,y) y quitar los vértices x e y, y todas sus aristas incidentes. Luego, G' tiene 2n vértices y para que cumpla con la cantidad de aristas mínima para cumplir con la HI, $n^2 + 2n + 2 - d(x) - d(y) \gt n^2 \longrightarrow 2n+2 \gt d(x) + d(y)$, la suma de los grados de los vértices que saque no puede ser mayor que $2n+2$, si la desigualdad se cumple, se cumple la hipótesis y queda probada la implicación. Si no se cumple, entonces significa que de G al quitar a `x` e `y` quite por lo menos $n^2+1$ aristas, dejando por lo menos 2n+1 aristas en un grafo de 2n vértices. Luego, por "principio del palomar", $N(x)\  \cap \ N(y) \neq \emptyset$, por lo que, tiene que existir un vértice z tal que exista una arista (x,z) y (y,z), y como en G, (x,y) ya era una arista, significa que ya existía un triangulo en G con 2n+2 y mas de $(n+1)^2$ aristas. 
# Ejercicio 11 ✅
![[Screenshot 2025-10-05 at 10.54.31.png]]
Hago inducción sobre la longitud `l` de la caminata.

Caso base: `l = 1`
Si la caminata es de longitud 1, entonces es un loop en el mismo vértice, por lo que se cumple que haya un ciclo impar.

HI: Si G tiene una caminata de longitud l impar que empieza y termina en el mismo vértice, entonces hay un ciclo simple impar. 

Paso inductivo:
Considero un grafo G con una caminata de longitud l' mayor que l, e impar.
Si en G la caminata no repite vértices, entonces se concluye que G tiene un ciclo impar, por lo que queda probado.
En otro caso, si la caminata repite un vértice, llamado `v`, entonces resulta que G tiene dos caminatas que van y vuelven de `v`, por lo que si o si uno de ellos es impar y de longitud menor que l. Por lo que también queda probado. 
# Ejercicio 12 ✅ 
![[Screenshot 2025-10-05 at 10.54.39.png]]
## $\Longrightarrow$ 
Por el contrarrecíproco, $G\ no\ es\ bipartito \land no\ es\ ciclo\ impar \Longrightarrow \exists v \in V\  / \ G-v\ no\ es\ bipartito$  
Si es un ciclo par, es posible encontrar una biparticion de G, tomando por un lado los vértices pares, y por otro los impares. Esto rompe con el antecedente de la implicación.

Si directamente no es un ciclo, uso el teorema que dice que `un grafo no es bipartito si y solo si tiene un ciclo impar`, lo que también se puede leer como `un grafo es bipartito si y solo si no tiene un ciclo impar`. 
Dentro de este caso, se me separan otros dos:
- Si tengo un ciclo impar con cosas afuera, simplemente tomo como vértice a quitar de G uno de esos que estén afuera, dejando el ciclo impar intacto y probando que G-v no es bipartito.
- Si tengo un ciclo impar con aristas internas extra, sin nada afuera. Tomo una de las aristas internas de G para formar otros dos ciclos mas chicos, donde como la cantidad de vértices de G es impar, obligatoriamente uno de estos dos ciclos mas chicos es impar, concluyendo que quitando un vértice de la partición par, G-v tampoco es bipartito. 
## $\Longleftarrow$ 
De forma directa.
Si G es un ciclo impar, entonces quitando cualquier vértice de G me va a quedar un grafo que puedo interpretar como un camino simple que va de $v_1$ a $v_{n-1}$, con el que ademas puedo agrupar los vértices impares y los pares por separado, biparticionando el grafo resultante. Por lo que queda que G-v es bipartito.

Si G es bipartito pero no un ciclo par, por el teorema anterior, si es bipartito, tiene por lo menos un ciclo par, por lo que tomo cualquier vértice v que no forme parte de alguno de los ciclos pares que hacen bipartito a G, lo quito de G, y como el ciclo par selecionado esta inalterado, G-v es bipartito.
# Ejercicio 13 ✅
![[Screenshot 2025-10-05 at 10.54.47.png]]
Caso base:
Para n=2 tenes únicamente dos vértices conectados por una única arista, si quitas cualquiera de los dos queda un grafo único solo, que se puede decir que es conexo.

Hipótesis inductiva:
Para todo $G_n \ / \ G_n\ conexo \text{, hay al menos dos vetices que cumplen con la consigna}$. 

Quiero probar que vale para $G_{n+1}$.
Como estoy asumiendo que G es conexo, si tiene n+1 vértices, entonces por lo menos tiene n aristas. Busco sacar un vértice para acomodar el grafo a la hipótesis. 
Si saco un vértice de grado 1 la "conexitud" no se rompe, ya que es como si estuviera sacando una hoja de un árbol de recursion, no estaría articulando nada.
Si saco un vértice de grado mayor a 1 puede que si parta a G en dos o mas componentes conexas. En ese caso, cada componente conexa sumándole el vértice v que saque antes, tiene 2 o mas vértices y es en esencia un grafo conexo de tamaño menor que n, por lo que entra dentro de la hipótesis inductiva, luego, puedo tomar el vértice, lo llamo $v_1$, que no sea el v que saque antes para quitárselo a G desde el principio así no rompo la conexitud del grafo en general. Luego puedo hacer el mismo razonamiento en otra de las componentes conexas que hayan quedado, obteniendo un $v_2$ que cumpla con lo mismo que $v_1$. Así obtuve dos vectores tales que $G_{n+1} / {v_1}$ es conexo y  $G_{n+1} / {v_2}$, luego como encontré los dos vértices, se cumple P(n+1). 
# Ejercicio 14 ❌
![[Screenshot 2025-10-05 at 10.55.02.png]]
![[Screenshot 2025-10-05 at 10.55.14.png]]


# Ejercicio 15 ❌ pero es fácil
![[Screenshot 2025-10-05 at 10.55.24.png]]
Siendo `n` la cantidad de vértices, y `m` la cantidad de aristas, tengo que 
# Ejercicio 16 ❌
![[Screenshot 2025-10-05 at 10.55.41.png]]
![[Screenshot 2025-10-05 at 10.55.49.png]]
### a)
ok
### b)


# Ejercicio 17 maso
![[Screenshot 2025-10-05 at 10.55.57.png]]
### a)
Como todos los vértices tienen grado de salida mayor que 0, en criollo seria que todos los vértices apuntan hacia otro, y como pueden haber como mínimo tantas aristas como vértices, a la fuerza va a pasar que se forme un camino dirigido que empiece en un vértice `v` y termine en el mismo.
Planteo el caso de que cada vértice tenga grado 1 y que todos apuntan a uno distinto, es decir, que para todo i en rango, $d_{in}(v_i) = 1$ y $d_{out}(v_i) = 1$. El inconveniente con esto llega cuando analizas en detalle el grafo, ya que planteando la secuencia, o camino, del grafo queda algo como esto:
$$
v_1 \underset{arista \ 1}{\rightarrow} v_2 \underset{arista \ 2}{\rightarrow} v_3 \underset{arista \ 3}{\rightarrow} ... \underset{arista \ n-1}{\rightarrow} v_n \underset{arista \ n}{\rightarrow} v_1
$$
El hecho de que todos tengan grado de salida por lo menos 1, hace que hayan por lo menos n aristas dirigidas en el grafo, aristas que "contribuyen" al grado de entrada de otro vértice. Entonces, si hay n aristas, por lo menos, para n vértices, aun en el caso mas borde de que todos los vértices tengan grado de entrada 1, se termina formando un ciclo. 

### b)
- Usar la implementación de grafo como lista de adyacencias, elegir uno y comenzar el recorrido.
- Llevo ademas en una lista de n de largo inicializada en 0's o false's, control de por cuales vértices ya pase.
- Itero sobre los vecindarios, selecciono el primero, o cualquiera en realidad, y paso a ver su vecindario, que se que existe porque todos tienen grado de salida mayor a 0.
- Eventualmente me cruzo con un vértice por el que ya pase, ya que la cantidad de vertices es finita. 

### c)
Como uso lista de adyacencia, construirla ya lleva O(n+m)
Luego se recorren todos los nodos una sola vez, pasando por todas las aristas tambien una sola vez.

### d)
#### $\Longrightarrow$
Quiero probar que un dígrafo D es aciclico implica que D es trivial (tiene un vértice solo) o tiene un vértice cuyo grado de salida es 0.
Que sea aciclico, por inciso a), significa que tiene por lo menos un vértice cuyo grado de salida es 0, por lo que al quitarlo de D, como no estoy agregando una arista nueva que pueda formar un ciclo antes inexistente, sino que por el contrario estoy quitando, si D es aciclico, D/{v} también lo es.
Si D es trivial, es valga la redundancia, trivial ver que es aciclico, no tiene aristas (asumiendo que no hay loops).


Caso $d_{out}(v) = 0$:

#### $\Longleftarrow$
Asumo que D es trivial o tiene u vértice cuyo grado de salida es 0, y quiero demostrar que D es aciclico.

Caso D trivial:
Como tiene un único vértice y asumo también que no tiene loops, es simple ver que es aciclico.

Caso $d_{out}(v) = 0$
Como estoy asumiendo que $\exists v \in D \ / \ d_{out}(v) = 0 \land D-\{v\}\text{ es aciclico}$, D también termina siendo aciclico, ya que , partiendo de $D-\{v\}$ aciclico, agregarle un vértices nuevo que tenga grado de salida 0 por inciso a) no hace que se forme ningún ciclo que no estuviera antes.  
### e)


### f)

# Ejercicio 18 ❌
![[Screenshot 2025-10-05 at 10.56.14.png]]
![[Screenshot 2025-10-05 at 10.56.25.png]]
# Ejercicio 19 ❌ volver 
![[Screenshot 2025-10-05 at 10.56.40.png]]
![[Screenshot 2025-10-05 at 10.56.49.png]]
# Ejercicio 20 ❌
![[Screenshot 2025-10-05 at 10.56.57.png]]
# Ejercicio 21 ❌
![[Screenshot 2025-10-05 at 10.57.10.png]]
![[Screenshot 2025-10-05 at 10.57.18.png]]
# Ejercicio 22 ❌
![[Screenshot 2025-10-05 at 10.57.27.png]]
![[Screenshot 2025-10-05 at 10.57.34.png]]
