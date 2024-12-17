# ADMINISTRACION DE TABLAS

## CREATE TABLE

### Sintaxis
```sql
CREATE TABLE nombre_tabla (
    columna1 tipo_dato restricciones,
    columna2 tipo_dato restricciones,
    ...
);
```

### Explicación
El comando `CREATE TABLE` se utiliza para **crear una nueva tabla** en una base de datos. 
Al definir una tabla, especificas el nombre de las columnas, sus tipos de datos y cualquier 
restricción adicional, como claves primarias, nulos o valores únicos.

### Ejemplo
Crear una tabla llamada `empleados` con columnas `id`, `nombre` y `salario`:
```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    salario DECIMAL(10, 2)
);
```

#### Resultado:
Se crea la tabla `empleados` con las columnas especificadas:
| **id** | **nombre** | **salario** |
|--------|------------|-------------|
|        |            |             |

---

## NOT NULL

### Sintaxis
```sql
columna tipo_dato NOT NULL
```

### Explicación
La restricción `NOT NULL` se utiliza para indicar que una columna **no puede contener valores nulos**. Esto significa que, al insertar o actualizar registros en la tabla, se debe proporcionar obligatoriamente un valor para esa columna.

### Ejemplo
Crear una tabla `usuarios` donde el campo `nombre` no puede ser nulo:
```sql
CREATE TABLE usuarios (
    id INT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL,
    email VARCHAR(100)
);
```
Insertar un registro sin proporcionar `nombre`:
```sql
INSERT INTO usuarios (id, email) VALUES (1, 'correo@ejemplo.com');
```

#### Resultado:
La consulta fallará porque la columna `nombre` no puede ser nula.

**Error:** 
```
Column 'nombre' cannot be null
```

---

## UNIQUE

### Sintaxis
```sql
columna tipo_dato UNIQUE
```

### Explicación
La restricción `UNIQUE` asegura que **todos los valores en una columna sean únicos**, es decir, que no se repitan dentro de la tabla. Una columna marcada como `UNIQUE` puede tener valores `NULL`, pero no se permitirán duplicados para los valores no nulos.

### Ejemplo
Crear una tabla `clientes` donde el campo `email` debe ser único:
```sql
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    email VARCHAR(100) UNIQUE
);
```
Insertar dos registros con el mismo `email`:
```sql
INSERT INTO clientes (id, nombre, email) VALUES (1, 'Ana', 'ana@ejemplo.com');
INSERT INTO clientes (id, nombre, email) VALUES (2, 'Pedro', 'ana@ejemplo.com');
```

#### Resultado:
La segunda consulta fallará porque el `email` debe ser único.

**Error:** 

```
Duplicate entry 'ana@ejemplo.com' for key 'email'
```

---

## PRIMARY KEY

### Sintaxis
```sql
columna tipo_dato PRIMARY KEY
```
O, al definir la clave primaria en varias columnas:
```sql
PRIMARY KEY (columna1, columna2)
```

### Explicación
La restricción `PRIMARY KEY` se utiliza para identificar **de forma única** cada fila de una tabla. Una clave primaria no permite valores duplicados ni nulos. Cada tabla puede tener **solo una clave primaria**, que puede estar compuesta por una o varias columnas.

### Ejemplo 1: Clave primaria en una sola columna
Crear una tabla `empleados` donde `id` sea la clave primaria:
```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    salario DECIMAL(10, 2)
);
```

### Ejemplo 2: Clave primaria compuesta
Crear una tabla `pedidos` donde la clave primaria sea la combinación de `id_cliente` y `id_pedido`:
```sql
CREATE TABLE pedidos (
    id_cliente INT,
    id_pedido INT,
    fecha DATE,
    PRIMARY KEY (id_cliente, id_pedido)
);
```

#### Resultado:
La combinación de `id_cliente` e `id_pedido` no puede repetirse:
| **id_cliente** | **id_pedido** | **fecha**   |
|---------------|--------------|------------|
| 1             | 101          | 2024-06-01 |
| 2             | 102          | 2024-06-02 |

---

## CHECK

### Sintaxis
```sql
columna tipo_dato CHECK (condicion)
```
O en la tabla:
```sql
CHECK (condicion)
```

### Explicación
La restricción `CHECK` se utiliza para **imponer condiciones** en los valores que se insertan en una columna. Si un valor no cumple la condición, se genera un error y la operación falla.

### Ejemplo
Crear una tabla `empleados` donde el `salario` debe ser mayor que 1000:
```sql
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    salario DECIMAL(10, 2) CHECK (salario > 1000)
);
```
Insertar un registro con un salario menor:
```sql
INSERT INTO empleados (id, nombre, salario) VALUES (1, 'Ana', 900);
```

#### Resultado:
La consulta fallará porque el salario no cumple la condición.

**Error:** 

```
Check constraint 'empleados_chk_1' is violated
```

---

## DEFAULT

### Sintaxis
```sql
columna tipo_dato DEFAULT valor
```

### Explicación
La restricción `DEFAULT` se utiliza para asignar un **valor predeterminado** a una columna si no se especifica un valor al insertar una fila. Esto simplifica las inserciones y garantiza valores consistentes.

### Ejemplo
Crear una tabla `usuarios` donde el campo `estado` tenga un valor predeterminado de 'activo':
```sql
CREATE TABLE usuarios (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    estado VARCHAR(20) DEFAULT 'activo'
);
```
Insertar un registro sin proporcionar `estado`:
```sql
INSERT INTO usuarios (id, nombre) VALUES (1, 'Pedro');
```

#### Resultado:
El campo `estado` tomará el valor predeterminado:
| **id** | **nombre** | **estado** |
|--------|------------|------------|
| 1      | Pedro      | activo     |



## AUTO INCREMENT

### Sintaxis
```sql
columna tipo_dato AUTO_INCREMENT
```

### Explicación
`AUTO_INCREMENT` es una restricción que se aplica a una columna para generar automáticamente valores únicos incrementales, normalmente utilizados en columnas de tipo clave primaria. El valor se incrementa en 1 de forma predeterminada, comenzando desde 1 a menos que se especifique otro valor.

### Ejemplo
Crear una tabla `usuarios` donde el `id` se incremente automáticamente:
```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50)
);
```
Insertar registros sin especificar el `id`:
```sql
INSERT INTO usuarios (nombre) VALUES ('Ana');
INSERT INTO usuarios (nombre) VALUES ('Pedro');
```
#### Resultado:
| **id** | **nombre** |
|--------|------------|
| 1      | Ana        |
| 2      | Pedro      |

---

## DROP TABLE

### Sintaxis
```sql
DROP TABLE nombre_tabla;
```

### Explicación
`DROP TABLE` se utiliza para eliminar por completo una tabla existente en la base de datos, junto con sus datos y estructura. Esta operación **no puede deshacerse**, por lo que debe utilizarse con precaución.

### Ejemplo
Eliminar una tabla `usuarios`:
```sql
DROP TABLE usuarios;
```
#### Resultado:
La tabla `usuarios` se elimina por completo, incluyendo todos sus registros.

---

## ALTER TABLE

### Sintaxis
```sql
ALTER TABLE nombre_tabla accion;
```

### Explicación
`ALTER TABLE` permite modificar la estructura de una tabla existente. Las acciones comunes incluyen agregar, eliminar, renombrar o modificar columnas.

### Ejemplo
Agregar una columna `email` a la tabla `usuarios`:
```sql
ALTER TABLE usuarios ADD email VARCHAR(100);
```
Renombrar la tabla `usuarios` a `clientes`:
```sql
ALTER TABLE usuarios RENAME TO clientes;
```

---

## ADD

### Sintaxis
```sql
ALTER TABLE nombre_tabla ADD columna tipo_dato;
```

### Explicación
`ADD` se utiliza con `ALTER TABLE` para agregar nuevas columnas a una tabla existente.

### Ejemplo
Agregar una columna `fecha_creacion` a la tabla `usuarios`:
```sql
ALTER TABLE usuarios ADD fecha_creacion DATE;
```

---

## RENAME COLUMN

### Sintaxis
```sql
ALTER TABLE nombre_tabla RENAME COLUMN nombre_viejo TO nombre_nuevo;
```

### Explicación
`RENAME COLUMN` se utiliza para cambiar el nombre de una columna en una tabla existente.

### Ejemplo
Renombrar la columna `nombre` a `nombre_completo` en la tabla `usuarios`:
```sql
ALTER TABLE usuarios RENAME COLUMN nombre TO nombre_completo;
```

---

## MODIFY COLUMN

### Sintaxis
```sql
ALTER TABLE nombre_tabla MODIFY COLUMN nombre_columna nuevo_tipo_dato;
```

### Explicación
`MODIFY COLUMN` se utiliza con `ALTER TABLE` para cambiar el tipo de dato o las restricciones de una columna existente.

### Ejemplo
Modificar la columna `nombre` en la tabla `usuarios` para permitir más caracteres:
```sql
ALTER TABLE usuarios MODIFY COLUMN nombre VARCHAR(100);
```



