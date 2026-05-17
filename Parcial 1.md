# Ejercicios con solución en clase

## Ejercicio 4 - RutaMinima
## Ejercicio 5 - Palabras en cadena

## Ejercicio 6 - Arboles binarios de búsqueda óptimos

## Ejercicio 7 - Dobra

## Ejercicio 8 - Cadenas de adición

## Ejercicio 9 - KingArmy

## Ejercicio 10 - Vacations
$$
f(i, ultAct) =
\begin{cases}
0 & \text{si } i = |acts| \\
min(1+f(i+1, DESC), f(i+1, GYM)) & \text{si } GYM \in acts[i] \land ultAct != GYM \\
min(1+f(i+1, DESC), f(i+1, COMP)) & \text{si } COMP \in acts[i] \land ultAct != COMP \\
0 & \text{si } i = |acts| \\
 & \text{en otro caso} 
\end{cases}
$$
se generaliza y queda mejor con la que dan en el slide, pero lo entendí.

## Ejercicio 13 - AstroTrade
### a)
Me lo creo.

### b)
$$
f(p, c, j) =
\begin{cases}
-\infty & \text{si } c < 0 \lor c > j \\
0 & \text{si } j = |p|-1 \\
max(p[j] + f(p, c-1, j+1), p[j] - f(p, c+1, j+1), f(p, c, j+1)) & \text{en otro caso} 
\end{cases}
$$
La llamada inicial seria f(dias, 0, 0); 

### d)
```c
vector<vector<int>> memo[c][j];
vector<int> p; // esto me lo da el ejercicio, no suma a la complejidad espacial

int solve(int c, int j)
{
	if(memo[c][j] != -1) return memo[c][j]
	
	if(c < 0 || c > j) return -inf;
	
	if(j == p.size()-1 && c == 0) return 0;
	if(j == p.size()-1 && c > 0) return p[j];
	
	memo[c][j] = max(p[j] + solve(c-1, j+1), p[j] - solve(c+1, j+1), solve(c, j+1));
	
	return memo[c][j];
}
```

## Ejercicio 14 - Fire
Para la parte de la complejidad "nlogn", ordeno de manera creciente "d". 

$$
f(t, d, p, acc, idx) =
\begin{cases}
0 & \text{si } idx >= |d|  \\
f(t, d, p, acc, idx+1) & \text{si } acc + t[idx] > d[idx] \\
max(p[idx] + f(t, d, p, acc+t[idx], idx+1), f(t, d, p, acc, idx+1)) & \text{en otro caso} 
\end{cases}
$$

## Ejercicio 17 - PilaCauta
### b)
$$
f(s, w, acc, idx) =
\begin{cases}
0 & \text{si } idx <= 0  \\
f(s, w, acc, idx-1) & \text{si } acc > s[idx] \\
max(1+f(s, w, acc+w[idx], idx+1), f(s, w, acc, idx+1)) & \text{en otro caso} 
\end{cases}
$$
la primer llamada seria f(s, w, 0, |w|-1);

### c)
Espacial: O(n)
Temporal: O(|w| * $max_s \in$ s )

## Ejercicio 20 - CaesarsLegions
### a)
$$
f(t, n_P, n_D, k_P, k_D) =
\begin{cases}
1 & \text{si } t = 0  \\
f(t-1, n_P, n_D-1, MP, k_D-1)  & \text{si } k_P = 0 \\
f(t-1, n_P, n_D-1, k_P, k_D-1)  & \text{si } n_P = 0 \\
f(t-1, n_P-1, n_D, k_P-1, MD)  & \text{si } k_D = 0 \\
f(t-1, n_P-1, n_D, k_P-1, k_D)  & \text{si } n_D = 0 \\
f(t-1, n_P-1, n_D, k_P-1, k_D) + f(t-1, n_P, n_D-1, k_P, k_D-1) & \text{en otro caso} 
\end{cases}
$$

### b)
$$
f(n_P, n_D, k, ultTropa) =
\begin{cases}
1 & \text{si } n_P + n_D = 0 \\
f(n_P, n_D-1, 1, D)  & \text{si } ultTropa = P \land k = MP \\
f(n_P-1, n_D, 1, P)  & \text{si } ultTropa = D \land k = MD \\
f(n_P-1, n_D, k+1, P) + f(n_P, n_D-1, 1, D)  & \text{si } ultTropa = P  \\
f(n_P-1, n_D, 1, P) + f(n_P, n_D-1, k+1, D)  & \text{si } ultTropa = D  \\
\end{cases}
$$

### c)
$$
f(n_P, n_D, ultTropa) =
\begin{cases}
1 & \text{si } n_P + n_D = 0 \\
f(n_P, n_D-1, 1, D)  & \text{si } ultTropa = P \land k = MP \\
f(n_P-1, n_D, 1, P)  & \text{si } ultTropa = D \land k = MD \\
f(n_P-1, n_D, k+1, P) + f(n_P, n_D-1, 1, D)  & \text{si } ultTropa = P  \\
f(n_P-1, n_D, 1, P) + f(n_P, n_D-1, k+1, D)  & \text{si } ultTropa = D  \\
\end{cases}
$$

## Ejercicio 21 - Farmer


## Ejercicio 24 - Lagunas 

$$
f(i, k) =
\begin{cases}
0 & \text{si } i >= |terreno|  \\
max(f(i+1, k), f(i, k+1), f(i+k, k+1) + G - \sum_{j=i+1}^{i+k+1}terrero[j]) & \text{en otro caso} 
\end{cases}
$$
Esto tiene O($n^2$) estados y una sumatoria O(n) por estado. Total O($n^3$).

## Ejercicio 25 - Mi Buenos Aires Crecido
```c
vector<int> ancho;
vector<int> alto;

int solve(int i, int ult)
{
	if(memo[i][ult] != -1) return memo[i][ult];

	if(i == ancho.size()) return 0;
	
	if(alto[i] > alto[ult])
	{
		memo[i][ult] = max(ancho[i] + solve(i+1, i), solve(i+1, ult));
	}
	else 
	{
		memo[i][ult] = solve(i+1, ult);
	}
	return memo[i][ult];
}
```

$$
f(i, ult) =
\begin{cases}
0 & \text{si } i >= |ancho|  \\
f(i+1, ult) & \text{si } alto[i] <= alto[ult]  \\
max(f(i+1, i) + ancho[i], f(i+1, ult)) & \text{en otro caso} 
\end{cases}
$$
Con dinámica es O($n^2$), sin dinámica, como la cantidad de llamados es O($2^n$), queda esa.


## Ejercicio 26 - Guirnaldas
## Ejercicio 29 - Deadlines
```c

sort(D);

int t = 0;
vector<int> res = {};
for(int n : D)
{
	if(n+1 <= t) { res.push_back(n); t++; }
}

return res;

```


## Ejercicio 30 - RutaEficiente
```c
int M; // kms de Mar del Plata
int C; // kms que hace el coche con el tanque lleno
vector<int> paradas; // vector de cada una de las estaciones de servicio
vector<int> res; // paradas hechas
int kms = C - paradas[0]; // kilometros que le quedan de autonomia al coche

for(int i = 1; i < paradas.size(); i++)
{
	if(paradas[i]-paradas[i-1] > kms)
	{
		kms = C;
		res.push_back(paradas[i]);
	}
	else
	{
		kms -= paradas[i]-paradas[i-1];
	}
}
```
## Ejercicio 31 - ProductoEscalar
```c
sort(w);
sort_inv(v)
int res = 0;

for(int i = 0; i < |v|; i++)
{
	res += w[i]*v[i];
}
```


## Ejercicio Extra - Maximin


