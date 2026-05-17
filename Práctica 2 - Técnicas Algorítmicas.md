## Ejercicio 1 - SumaSubconjuntosBT
Soluciones candidatas: {0,0,0}, {0,0,1}, {0,1,0}, {1,0,0}, {1,1,0}, {1,0,1}, {0,1,1,}, {1,1,1}
Soluciones validas: {1,0,1}, {0,1,0}
Soluciones parciales: {0}, {1}, {1,0}, {0,1},

f) La complejidad es O($2^n$).


## Ejercicio 2 - MagiCuadrados
a) Habría que generar $n^2!$ cuadrados.
b) 

## Ejercicio 3 - MaxiSubconjunto
### a)
```c
vector<int> res;
int k;
vector<vector<int>> matrix;
vector<int> best;
int besti;

void solve(int i, int j)
{
	if(res.size() >  k) return;
	
	if(res.size() == k) 
	{
		if(res.sum() > besti)
		{
			besti = res.sum();
			best = res;
		}
		return;
	}
	
	res.push_back(matrix[i][j]);
	solve(i+1, j+1);
	res.pop();
	solve(i+1, j+1);
}
```


### b)
La complejidad temporal es `O(`$n^2$`)` y la espacial `O(k)`.

### c)
La poda de optimalidad que propongo es chequear el tamaño de la solución parcial que se tenga en cada llamada recursiva, si es mayor que el k dado, se poda esa rama. 

## Ejercicio 4 - RutaMinima
### a)
Lo leí escrito pq no entendía la formula.

### b) 
La espacial es O(n) y la temporal O(n!*n). 

### c)
Una poda seria que la solución parcial actual sea peor (osea, que su suma sea mayor), a la mejor solución hallada hasta ese momento. 

## Ejercicio 5 - Palabras en cadena
### a)
$$
f(cadena, acc, i) =
\begin{cases}
true & \text{si } palabra(acc) \land i == cadena.size() \\
false & \text{si } !palabra(acc) \land i == cadena.size() \\
f(cadena, [], i++) & \text{si } !palabra(acc) \\
f(cadena, acc.push(cadena[i]), i++) \lor f(cadena, [], i++) & \text{otherwise} 
\end{cases}
$$

### b)
O(|c| * $2^n$)
### c)
inducción sobre la longitud de la cadena
La clave esta en hacer bien la firma de la funcion


## Ejercicio 7 - Dobra 
### a)
candidata: "aebc"
parcial: "aec..."

### b)
$$
f(palabra) =
\begin{cases}
true & \text{si } palabra(acc) \land i == cadena.size() \\
\end{cases}
$$

## Ejercicio 9 - KingArmy
fibonacci

## Ejercicio 10 - Vacations

[(compe), (gym, compe), (gym), ()]