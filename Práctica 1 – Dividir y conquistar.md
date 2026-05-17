## Ejercicio 1
```
def merge_sort(arr):
	if len ( arr ) <= 1:
		return arr

	medio = len ( arr ) // 2
	mitad_izq = merge_sort(arr [:medio])
	mitad_der = merge_sort(arr[medio:])
	
	return merge(mitad_izq, mitad_der)
```
```
def merge(izq, der):
	mergeados = []
	i = j = 0

	while i < len(izq) and j < len(der):
		if izq[i] < der[j]:
			me rg e ad os . append ( izq [ i ])
			i += 1
		else:
			mergeados.append(der[j])
			j += 1
	mergeados.extend(izq[i:])
	mergeados.extend(der[j:])
	return mergeados
```

#### 1. 
Lineas `divide`: 
	`medio = len ( arr ) // 2`
	
Lineas `conquer`: 
	`mitad_izq = merge_sort(arr [:medio])`
	`mitad_der = merge_sort(arr[medio:])`
	
Lineas `combine`: 
	`return merge(mitad_izq, mitad_der)`
#### 2. 
Se divide en **2** subproblemas.

#### 3. 
Los problemas son de tamaño **n/2**.

#### 4.
El costo es **O(n)**.

#### 5. 
$$
T(n) =
\begin{cases}
\Theta(1) & \text{si } n \leq 1 \\
2T\!\left(\tfrac{n}{2}\right) + \Theta(n) & \text{si } n > 1
\end{cases}
$$

#### 6. 
La complejidad es  ***O(nlogn)*.


## Ejercicio 2
```
 def busqueda_binaria(arr, objetivo, izq=0, der=len(arr)-1):
	if izq > der:
		return False #Elemento no encontrado

	medio = (izq+der) // 2
	if arr[medio] == objetivo:
		return medio
	elif arr[medio] > objetivo:
		return busqueda_binaria(arr, objetivo, izq, medio-1)
	else:
		return busqueda_binaria(arr, objetivo, medio+1 ,der)
```
#### 1. 
Lineas `divide`: 
	`medio = (izq+der) // 2`
	`elif arr[medio] > objetivo:`
Lineas `conquer`: 
	`return busqueda_binaria(arr, objetivo, izq, medio-1)`
	`return busqueda_binaria(arr, objetivo, medio+1 ,der)`
Lineas `combine`: 
	No hay.
#### 2. 
Se divide en **1** subproblemas.

#### 3. 
Los problemas son de tamaño **n/2**.

#### 4.
El costo es *O(1)**.

#### 5. 
$$
T(n) =
\begin{cases}
\Theta(1) & \text{si } n \leq 1 \\
1T\!\left(\tfrac{n}{2}\right) + \Theta(1) & \text{si } n > 1
\end{cases}
$$

#### 6. 
La complejidad es **O(logn)**.

## Ejercicio 3

