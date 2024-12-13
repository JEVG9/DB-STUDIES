# MODIFICADORES - PT.2

## Comentarios

### Sintaxis
```SQL
--<comment>
```
Como en cualquier otro lenguaje de programacion, en SQL existen los comentarios para poder servir de guia para el programador.

#### Ejemplo:

Al ejecutar lo siguiente:

```SQL
-- esto es un comentario
```

El sistema no hara mas nada dado que es un comentario.

## NULL
### Sintaxis
```SQL
SELECT <cols> 
FROM <table> 
WHERE coln IS NULL;
```

Este comando retorna los datos que esten relacionados con valores NULL o desconocidos, si en una columna falta un valor (esta marcado como NULL).

#### ejemplo:

Dada una tabla `empleados`:

|**id**	|**name**	|**salary**|
|--|--|--|
|1	|Ana	|3000|
|2	|Juan	|NULL|
|3	|Laura	|2500|

Ejecutando lo siguiente:

```SQL
SELECT name 
FROM empleados 
WHERE salary IS NULL;
```

Tendremos como resultado:

```
|name|
|Juan|
```

## MIN,MAX

### Sintaxis:

```SQL
SELECT MIN(coln), MAX(coln) 
FROM <table>;
```

La sentencia `MIN` retorna el valor mas bajo en la columna seleccionada, por consigueinte `MAX` realiza la accion contraria.

#### Ejemplo:

Dada una tabla `empleados`:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Ejecutando lo siguiente:

```SQL
SELECT MIN(salary), MAX(salary) 
FROM empleados;
```

Tendremos como resultado:

```
|MIN(salary)|MAX(salary)|
|2500	    |4000       |
```

## COUNT
### Sintaxis
```SQL
SELECT COUNT(coln) 
FROM <table>
WHERE <condition>;
```

Cuenta la cantidad de filas, excluyendo NULL.

#### Ejemplo:
Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Luego ejecutamos:
```SQL
SELECT COUNT(salary) 
FROM empleados;
```

El resultado sera:
```
|COUNT(salary)|
|3            |
```

## SUM
### Sintaxis

```SQL
SELECT SUM(col) 
FROM <table>;
```

Calcula la suma total de los valores en una columna numérica.

#### Ejemplo:

Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Luego ejecutamos:
```SQL
SELECT SUM(salary) 
FROM empleados;
```

Resultado:

```
|SUM(salary)|
|9500       |
```

## AVG
### Sintaxis

```SQL
SELECT AVG(columna) 
FROM tabla;
```

Calcula el promedio de los valores de una columna numérica.

#### Ejemplo:

Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Luego ejecutamos:
```SQL
SELECT AVG(salary) 
FROM empleados;
```

Resultado:
```
|AVG(salary)|
|3166.667   |
```

## IN
### Sintaxis
```SQL
SELECT <cols> 
FROM <talbe> 
WHERE <coln> IN (value1,...,valuen);
```

Filtra registros que coinciden con cualquiera de los valores especificados.

#### Ejemplo:

Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Luego ejecutamos:

```SQL
SELECT id 
FROM empleados 
WHERE salary IN (3000, 2500);
```

Resultado:
```
| id   |
|1     |
|2     |
```

Tambien se peude combinar con `NOT` para ejecutar consultas con negaciones, como el siguiente ejemplo usando la misma tabla:

```SQL
SELECT id 
FROM empleados 
WHERE salary NOT IN (3000, 2500);
```

Esto dara como resultado:
```
| id   |
|3     |
```

Ademas de poder ser usado en conjunto con consultas anidadas, un ejemplo generalizado seria:

```SQL
SELECT * FROM Customers
WHERE CustomerID NOT IN (SELECT CustomerID FROM Orders);
```

En este ultimo ejemplo el retorno sera todos los customerID de Customers que no esten en los customerID de las orders.


## BETWEEN
### Sintaxis
```SQL
SELECT <cols> 
FROM <table> 
WHERE <colN> BETWEEN value1 AND value2;
```

Filtra registros dentro de un rango.

No solo se da con valores numericos si no que los valores alfabeticos tambien se pueden operar haciendo asi que retorne los elementos en un rango que se encuentre alfabeticamente entre los valores estipulados.

De igual manera los valores de fechas y otros tipos de datos tambien cumplen con la restriccion de rango.

#### Ejemplo:

Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Luego ejecutamos:
```SQL
SELECT id 
FROM empleados 
WHERE salary BETWEEN 2000 AND 3500;
```

Esto retornara:
```
| id |
|1   |
|2   |
```

## ALIAS
### Sintaxis
```SQL
SELECT columna AS alias 
FROM tabla;
```

Renombra temporalmente una columna o tabla.

#### Ejemplo:
Teniendo:

|**id**	|**salary**|
|--|--|
|1	|3000|
|2	|2500|
|3	|4000|

Ejecutando el siguiente query:
```SQL
SELECT salary AS Salario 
FROM empleados;
```
Resultado:
```
|Salario|
|3000   |
|2500   |
|4000   |
```

## CONCAT
### Sintaxis
```SQL
SELECT CONCAT(colA, <union text>, colB) 
FROM <table>;
```
`CONCAT` se utiliza para combinar valores de varias columnas o cadenas en un solo resultado. Esto es especialmente útil para unir nombres, direcciones, o cualquier tipo de información relacionada. Puedes incluir texto adicional entre los valores combinados.

#### Ejemplo
Teniendo:

|**nombre**	|**apellido**|
|-|-|
|Ana|	López|
|Juan|	Pérez|
|Laura|	García|

Ejecutando:
```SQL
SELECT CONCAT(nombre, ' ', apellido) AS nombre_completo 
FROM empleados;
Resultado:
```
Tendremos como resultado:
```
|nombre_completo|
|Ana López      |
|Juan Pérez     |
|Laura García   |
```

## GROUP BY

### Sintaxis
```SQL
SELECT colN, función_agregada(colN) 
FROM <table> 
GROUP BY colN;
```
`GROUP BY` agrupa filas que tienen el mismo valor en una columna específica y permite realizar operaciones agregadas como `COUNT`, `MAX`, `MIN`, `SUM`, `AVG`, sobre cada grupo. Es indispensable cuando quieres analizar datos agrupados.

#### Ejemplo
Teniendo:

|departamento	|salario|
|-|-|
|Ventas	|3000|
|Ventas	|2500|
|IT	|4000|
|IT	|3500|


Ejecutando el siguiente query:

```SQL
SELECT departamento, SUM(salario) AS total_salarios 
FROM empleados 
GROUP BY departamento;
```

Tendremos el siguiente resultado:
```
|departamento|total_salarios|
|Ventas      |5500          |
|IT          |7500          |
```

## HAVING
### Sintaxis
```SQL
SELECT col, función_agregada(col) 
FROM <table> 
GROUP BY col 
HAVING <condition>;
```
`HAVING` es similar a `WHERE`, pero se utiliza para filtrar los resultados de un `GROUP BY` basándose en las funciones agregadas, como `SUM`, `COUNT`, `AVG`, etc.

#### Ejemplo
Teniendo:

|**departamento**	|**salario**|
|-|-|
|Ventas|	3000|
|Ventas|	2500|
|IT	|4000|
|IT	|3500|

Y ejecutando:
```SQL
SELECT departamento, SUM(salario) AS total_salarios 
FROM empleados 
GROUP BY departamento 
HAVING total_salarios > 6000;
```

Resultado lo siguiente:
```
|departamento|total_salarios|
|------------|--------------|
|IT          |7500          |
```


## CASE
### Sintaxis

```SQL
SELECT col, 
       CASE 
           WHEN <condition> THEN <result> 
           ELSE <another result> 
       END AS <alias> 
FROM <table>;
```

`CASE` permite realizar evaluaciones condicionales en las consultas y devolver valores diferentes según las condiciones especificadas. Es útil para categorizar datos o personalizar resultados.

Con este modificador se usan los siguientes elementos:

 - `WHEN`: Indica la condicion que se evaluara.
 - `THEN`: Se usa luego de indicar la condicion `WHEN` para indicar el resultado esperado. 
 - `ELSE`: Es el elemento que define el  resultado cuando no se cumple ninguna condicion anterior, si se omite el valor default sera `NULL`.
 - `END`: Este elemento marca el fin de la seccion `CASE` y es de uso obligatorio, este tambien puede tener asignaciones con `ALIAS` o incluso condicionales para terminar de usar el bloque resultado del `CASE`.

#### Ejemplo
Teniendo:

|nombre	|salario|
|-|-|
|Ana	|3000|
|Juan	|2500|
|Laura	|4000|

```SQL
SELECT nombre, 
       CASE 
           WHEN salario > 3000 THEN 'Alta' 
           ELSE 'Baja' 
       END AS categoria 
FROM empleados;
```

Resultado:

```
| nombre | categoria |
|Ana     |Baja       |
|Juan    |Baja       |
|Laura   |Alta       |
```


## IFNULL
### Sintaxis
```SQL
SELECT IFNULL(columna, valor_por_defecto) 
FROM tabla;
```
`IFNULL` reemplaza valores `NULL` en una columna por un valor predeterminado. Esto asegura que las consultas no devuelvan valores vacíos y puede ser útil para cálculos o reportes donde los valores `NULL` deben ser tratados.

#### Ejemplo
Teniendo:

|**nombre**	|**salario**|
|-|-|
|Ana	|3000|
|Juan	|NULL|
|Laura	|2500|

Ejecutando: 
```SQL
SELECT nombre, IFNULL(salario, 0) AS salario_revisado 
FROM empleados;
```

Resultado:

```
| nombre | salario_revisado|
|Ana     |3000             |
|Juan    |0                |
|Laura   |2500             |
```