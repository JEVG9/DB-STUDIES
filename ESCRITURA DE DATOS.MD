# ESCRITURA DE DATOS

## INSERT INTO
### Sintaxis:

```SQL
INSERT INTO <table> (col1,...,colN)
VALUES (val1,...,valN);

or

INSERT INTO <table> (col1,...,colN)
<SELECT QUERY>
```

Este comando se usa para poder agregar datos a las filas indicadas,
El comando se puede usar agregando valores directamente usando
el elemento `VALUE` para indicar los valores con parentesis y comas.

Las querys tambien pueden servir para agregar elementos con este
comando, usando `SELECT` y la respectiva query que incluso puede
ser combinada con todas las demas combinaciones para hacer querys.

#### Ejemplo con ˋVALUEˋ:

```
INSERT INTO users (name,age)
VALUES 
    ('Carlos',40),
    ('Neko',19);
```

Este ejemplo agrega a la tabla `users` 4 datos en 2 columnas
de datos `name` y `age` respectivamente en cada uno.

#### Otro ejemplo pero con ˋSELECTˋ:

```SQL
INSERT INTO users(name,age)
SELECT name,age
FROM employees
WHERE age>30;
```

En este ultimo ejemplo se agregan los datos `age` y `name` de la
tabla `employees` que tengan mas de `30` como edad a la tabla `users`

**Los datos ingresados cumpliran y deben cumplir con el tipo de 
datos que se indicaron al momento de crear la tabla originalmente.**

## UPDATE
### Sintaxis
```SQL
UPDATE <table>
SET col1 = val1,...,
colN = valN
WHERE <conditional>;
```
La sentencia `UPDATE` en __SQL__ se utiliza para modificar los valores de una o más columnas en una tabla existente. Permite actualizar uno o varios registros, dependiendo de las condiciones especificadas.

#### Elementos clave:
- `table`: El nombre de la tabla donde se actualizarán los datos.
- `SET`: Especifica las columnas y los nuevos valores que tendrán.
- `WHERE`: Define qué filas se deben actualizar. Si se omite, ¡todas las filas de la tabla serán actualizadas! (***Precaución***).

#### Ejemplo simple:

Tabla empleados:

|**id**	|**nombre**	|**departamento**	|**salario**|
|-|-|-|-|
|1	|Ana	|Ventas	|3500|
|2	|Juan	|Recursos Humanos|	2500|
|3	|Pedro	|Ventas	|2000|
|4	|María	|Recursos Humanos	|1800|

**Actualización**:
Supongamos que queremos aumentar el salario de todos los empleados del departamento de "Ventas" en 500.

```SQL
UPDATE empleados
SET salario = salario + 500
WHERE departamento = 'Ventas';
```
Resultado:
```
|id	|nombre	|departamento	  |salario|
|1	|Ana	|Ventas	          |4000   |
|2	|Juan	|Recursos Humanos |2500   |
|3	|Pedro	|Ventas	          |2500   |
|4	|María	|Recursos Humanos |1800   |
```
### Actualizar múltiples columnas
Puedes modificar varias columnas en una sola sentencia `UPDATE`.

#### Ejemplo:
Supongamos que el empleado con `ID` **3** ha cambiado de departamento a `Recursos Humanos` y su salario ahora es **3000**.

```SQL
UPDATE empleados
SET departamento = 'Recursos Humanos', salario = 3000
WHERE id = 3;
```

Resultado:
```
|id	|nombre	|departamento	    |salario|
|1	|Ana	|Ventas          	|4000   |
|2	|Juan	|Recursos Humanos	|2500   |
|3	|Pedro	|Recursos Humanos	|3000   |
|4	|María	|Recursos Humanos	|1800   |
```

#### Precauciones con UPDATE
Siempre usa `WHERE` si no quieres actualizar toda la tabla.

Si omites el `WHERE`, todas las filas serán modificadas.

```SQL
UPDATE empleados
SET salario = salario + 500;
```

Este comando aumentará el salario de todos los empleados en la tabla.

Revisa antes de ejecutar en producción.

Puedes usar un `SELECT` primero para asegurarte de que las filas afectadas sean las correctas:

```SQL
SELECT * FROM empleados WHERE departamento = 'Ventas';
```

Prueba con transacciones.

En bases de datos que soportan transacciones, puedes usar `BEGIN` y `ROLLBACK` para probar:

```SQL
BEGIN;
UPDATE empleados SET salario = 5000 WHERE id = 1;
ROLLBACK; -- Revierte los cambios
```

### Usos comunes de `UPDATE`
***Corrección de errores en datos***:

Cambiar información incorrecta, como nombres mal escritos.

```SQL
UPDATE empleados SET nombre = 'Ana María' WHERE id = 1;
```

***Revisión de información masiva***:

Aplicar ajustes generales, como incrementos salariales o actualizaciones por cambios organizacionales.

```SQL
UPDATE empleados SET salario = salario * 1.1 WHERE departamento = 'Ventas';
```

***Marcar registros como inactivos o eliminados***:

Utilizando una columna para señalar si un registro sigue activo.

```SQL
UPDATE empleados SET activo = 0 WHERE id = 4;
```

## DELETE

### Sintaxis
```SQL
DELETE FROM nombre_tabla
WHERE condicion;
```

El comando `DELETE` se utiliza en __SQL__ para eliminar filas específicas de una tabla en una base de datos. Es una operación que afecta directamente a los datos y debe usarse con cuidado, especialmente cuando se omite una condición, ya que puede borrar todos los registros.

#### Ejemplo:

Tabla `empleados` antes de eliminar:

|id	|nombre	|departamento|	salario|
|-|-|-|-|
1|	Ana|	Ventas|	3500|
2|	Juan	|Recursos Humanos	|2500|
3	|Pedro	|Ventas	|2000|
4|	María	|Recursos Humanos|	1800|

Ejecutando lo siguiente:

```SQL
DELETE FROM empleados
WHERE id = 3;
```

Tabla `empleados` después de eliminar:
```
|id	|nombre	|departamento	   |salario|
|1	|Ana	|Ventas	           |500    |
|2	|Juan	|Recursos Humanos  |2500   |
|4	|María	|Recursos Humanos  |1800   |
```

#### Consideraciones importantes sobre `DELETE`
**`WHERE` es crucial**:

Si no especificas una condición con `WHERE`, todas las filas de la tabla serán eliminadas.
Ejemplo sin `WHERE`:
```SQL
DELETE FROM empleados;
```
Esto vaciará la tabla empleados.
Recuerda que `DELETE` no afecta la estructura de la tabla:

Los datos se eliminan, pero las columnas, índices y demás estructura de la tabla permanecen intactos.

**Las condiciones pueden ser complejas**:

Puedes usar operadores como `AND`, `OR` y comparaciones para definir qué filas deben eliminarse.

```SQL
DELETE FROM empleados
WHERE departamento = 'Ventas' AND salario < 3000;
```

#### Ejemplo avanzado:

Tabla productos antes de eliminar:

|id	|nombre_producto|	stock	|precio|
|-|-|-|-|
|1	|Laptop|20|	1200|
|2	|Tablet	|50	|600|
|3	|Celular|	10|	800|
|4	|Monitor|	30|	300|


Eliminando productos con un stock menor a 15.

```SQL
DELETE FROM productos
WHERE stock < 15;
```

Tabla productos después de eliminar:
```
|id	|nombre_producto |stock	|precio|
|1	|Laptop	         |20	|1200  |
|2	|Tablet	         |50	|600   |
|4	|Monitor	     |30	|300   |
```
### Cláusulas comunes con `DELETE`
`LIMIT`: Restringe el número de filas que se eliminarán.

```SQL
DELETE FROM empleados
WHERE departamento = 'Ventas'
LIMIT 1;
```

`ORDER BY`: Establece un orden para seleccionar las filas que se eliminarán primero.

```SQL
DELETE FROM empleados
WHERE departamento = 'Ventas'
ORDER BY salario ASC
LIMIT 1;
```
### Diferencias entre `DELETE` y otras operaciones similares

`TRUNCATE`: Elimina todas las filas de una tabla de forma más eficiente y rápida que `DELETE`, pero no permite condiciones ni dispara triggers. Además, reinicia los contadores automáticos como los de columnas `AUTO_INCREMENT`.

```SQL
TRUNCATE TABLE empleados;
```

`DROP`: Elimina toda la tabla, incluyendo su estructura y datos.

```SQL
DROP TABLE empleados;
```

### Precauciones al usar DELETE
**Hacer un respaldo antes de grandes cambios**: Si ocurre un error, los datos eliminados no se podrán recuperar fácilmente.

**Usar una transacción si es posible**: Esto permite deshacer los cambios en caso de un error.
```SQL
START TRANSACTION;
DELETE FROM empleados WHERE departamento = 'Ventas';
ROLLBACK; -- Deshacer los cambios
```

##
##
##
##
##
##
##
##
##
##
