# MODIFICADORES

En SQL existen diferentes sentencias que modifican el comportamiento de una consulta, de esta manera se especifican que se busca o que accion se efectua.

## DISTINCT

#### sintaxis:
```
SELECT DISTINCT <cols> FROM <table>;
```
El modificador `DISTINCT` se usa para eliminar duplicados en las consultas, ej:


|**CIUDAD** | **PAIS** |
|-------|--------|
|CARTAGENA|COLOMBIA|
|BARRANQUILLA|COLOMBIA|
|MARACAIBO|VENEZUELA|
|DAVID|PANAMA|

Si queremos saber que paises existen en la tabla hacemos:

```
SELECT DISTINCT pais FROM ciudades;
```

esto retornara:

```
|  Pais   |
|COLOMBIA |
|VENEZUELA|
|PANAMA   |
```

## WHERE

#### sintaxis:
```
SELECT <cols>
FROM <table>
WHERE <conditional statement>;
```

Este modificador se encarga de colocar una condicion para poder completar la consulta, ej:

|**name** | **salary** |
|-------|--------|
|jesus|1000|
|neko|2000|
|nekito|3000|
|nekon|4000|

Si aplicamos:

```
SELECT name,salary 
FROM employess
WHERE salary > 2000;
```

Esto retornara lo siguiente:

```
| name  | salary | 
|nekito |3000    |
|nekon  |4000    |
```

**para tener en cuenta, cada query/consulta temrina cuando se escribre el `;` mas no antes**

## ORDER BY
#### sintaxis:
```
SELECT <cols> 
FROM <table> 
ORDER BY <col1> DESC|ASC,...., <coln> DESC|ASC;
```
Este ordena los datos datos de manera ascendente(`ASC`) o descendente(`DESC`), se puede llamar esta sentencia para diferentes datos en una misma consulta, ej:

|**name**	|**salary**|
|----|---|
|Miguel|	3000|
|Carmen	|2500|
|Carlos	|3500|
|Carla|	2500|
|Neko	|4000|

```
SELECT name, salary 
FROM employees 
ORDER BY salary DESC, name ASC;
```
Esto ordenará los resultados por salario de mayor a menor y, si hay empleados con el mismo salario, los ordenará por nombre de A a Z, tal que:

```
|  name	|  salary|
|Neko	|4000    |
|Carlos	|3500    |
|Miguel	|3000    |
|Carla	|2500    |
|Carmen	|2500    |
```



## LIKE

#### sintaxis:
```
SELECT <cols> 
FROM <talbe> 
WHERE <col> LIKE <'patron'>;
```

El modificador `LIKE` se utiliza para buscar un patrón en una columna, generalmente usado con comodines.

### Sintaxis básica:
- `%` representa cualquier número de caracteres (incluyendo ninguno).
- `_` representa un solo carácter.

#### Ejemplo:
|**nombre**  | **ciudad** |
|------------|------------|
|Carlos      |Bogotá      |
|Carmen      |Cali        |
|Carla       |Medellín    |
|Miguel      |Cali        |

Si queremos encontrar todas las personas cuyo nombre empiece con "Car", podemos hacer:

```
SELECT nombre 
FROM personas 
WHERE nombre LIKE 'Car%';
```

esto retorna:

```
|  nombre |
|Carlos	  |
|Carmen	  |
|Carla	  |
```

**`LIKE` solo puede usarse con un condicional `WHERE`**

## AND
### Sintaxis basica:

```
SELECT <cols>
FROM <talbe>
WHERE <condition1> AND <condicion2> AND <conditionn>;
```
El modificador `AND` se utiliza para combinar varias condiciones y asegura que todas las condiciones sean verdaderas para que el registro sea seleccionado. Es decir, todas las condiciones deben cumplirse para que el resultado sea verdadero. 

#### ejemplo:

|**name**|**salary**|**department**|
|----|----|----|
|Miguel|3000|ventas|
|Laurda|2500|marketing|

Si ejecutamos:

```
SELECT name, salary
FROM employees
WHERE salary > 2000 AND department = 'ventas';
```

Nos retornara lo siguiente:

```
| name | salary | department |
|Miguel|3000    |ventas      |
```
## OR
### Sintaxis basica:

```
SELECT <cols>
FROM <talbe>
WHERE <condition1> OR <condicion2> OR <conditionn>;
```

El modificador `OR` se utiliza para combinar varias condiciones, pero basta con que una sola de ellas sea verdadera para que el registro sea seleccionado. Es decir, si cualquiera de las condiciones es verdadera, el registro será incluido.

#### Ejemplo:

|**name**|**salary**|**department**|
|----|----|----|
|Miguel|3000|ventas|
|Laura|1500|marketing|
|neko|1000|ventas|

si ejecutamos:

```
SELECT name, salary
FROM employees
WHERE salary > 2000 OR department = 'ventas';
```

Retornara:

```
| name | salary | department |
|Miguel|3000    |ventas      |
|neko  |1000    |ventas      |
```

## NOT

### Sintaxis basica:

```
SELECT <cols>
FROM <talbe>
WHERE NOT <condition>;
```

El modificador `NOT` se utiliza para negar una condición, es decir, selecciona los registros que no cumplen con la condición especificada. Si una condición es verdadera, NOT la convierte en falsa, y si es falsa, la convierte en verdadera.

#### Ejemplo:
|**name**|**salary**|**department**|
|----|----|----|
|Miguel|3000|ventas|
|Laura|1500|marketing|
|neko|1000|ventas|

Si ejecutamos:

```
SELECT name, salary
FROM employees
WHERE NOT salary > 2000;
```

Esto rotarna:

```
|  name	|  salary |
|Neko	|1500     |
|Carla	|1800     |
```

**Los condicionales `OR`,`AND` y `NOT` deben de ser usados con WHERE**

## LIMIT
### Sintaxis basica:
```
SELECT <cols>
FROM <tables>
LIMIT <number or rows> (OFFSET <initial row>);
```

El modificador `LIMIT` en SQL se utiliza para restringir la cantidad de filas que se devuelven en una consulta. Es especialmente útil cuando queremos limitar los resultados de una consulta, ya sea para obtener una muestra pequeña de datos o para obtener los primeros o últimos registros que cumplen con una condición.

#### Ejemplo:

|**name**	|**salary**|
|----|---|
|Miguel	|3000|
|Carmen	|2500|
|Laura	|4000|
|neko	|4000|
|pochito	|4000|

Si ejecutamos:

```
SELECT name, salary
FROM employees
LIMIT 3;
```

Retornara:

```
| name	| salary |
|Miguel	|3000    |
|Carmen	|2500    |
|Laura	|4000    |
```

Si quisieramos usar un offset, como el sigueinte:

```
SELECT name, salary
FROM employees
LIMIT 2 OFFSET 2;
```

Entonces retornara:
```
| name	| salary |
|Laura	|4000    |
|neko	|4000    |
```
