# ADMINISTRACION DE DB

## CREATE DATABASE

### Sintaxis

```SQL
CREATE DATABASE <db name>;
```

El comando `CREATE DATABASE` se utiliza en __SQL__ para crear una nueva base de datos en el sistema de gestión de bases de datos (**DBMS**). Este comando permite definir un espacio donde se almacenarán las tablas, vistas, procedimientos y demás objetos necesarios para gestionar datos.

### Crear una base de datos con configuración adicional

Algunos sistemas de gestión de bases de datos (como **MySQL**) permiten incluir configuraciones adicionales como el conjunto de caracteres (`character set`) y el tipo de ordenamiento (collation).

#### Ejemplo:

Crear una base de datos llamada mi_empresa con configuración específica:

```SQL
CREATE DATABASE mi_empresa
CHARACTER SET utf8mb4
COLLATE utf8mb4_general_ci;
```

**Explicación**:
- `CHARACTER SET utf8mb4`: Define el conjunto de caracteres (útil para almacenar emojis, caracteres especiales, etc.).
- `COLLATE utf8mb4_general_ci`: Especifica el ordenamiento de los datos. ci significa case-insensitive (no distingue entre mayúsculas y minúsculas).

### Comprobar el uso de una base de datos
\
Antes de empezar a trabajar en la base de datos (crear tablas, insertar datos, etc.), es necesario seleccionarla con el comando `USE`:

```SQL  
USE mi_empresa;
```

Este comando establece la base de datos mi_empresa como la base de datos actual.

### Manejo de errores
Si intentas crear una base de datos que ya existe, recibirás un error:

```SQL
CREATE DATABASE mi_empresa;
```

**Error**:

```
ERROR 1007 (HY000): Can't create database 'mi_empresa'; database exists
```
*Solución*:
Usar la cláusula `IF NOT EXISTS` para evitar errores si la base de datos ya existe:

```SQL
CREATE DATABASE IF NOT EXISTS mi_empresa;
```

### Eliminar una base de datos
Si necesitas eliminar una base de datos creada, usa el comando `DROP DATABASE`:

```SQL
DROP DATABASE mi_empresa;
```
**Precaución**: Este comando eliminará toda la base de datos y sus datos, y no se puede deshacer.

## DROP

### Sintaxis

```SQL
DROP <object to delete>;
```

El comando `DROP` se usa para eliminar los siguientes objetos:

- DATABASE: Elimina una db tal que `DROP DATABASE nombre_base_de_datos;`
- TABLE: Elimina una tabla tal que `DROP TABLE nombre_tabla;`
- VIEW:Elimina una db tal que `DROP VIEW nombre_vista;`
- INDEX:Elimina una db tal que `DROP INDEX nombre_indice ON nombre_tabla;`

**Una recomendacion es usar el comando `IF EXIST` para evitar errores.**

## SHOW DATABASES

### Sintaxis
```SQL
SHOW DATABASES;
```

Este comando es muy simple y se basa unicamente en mostrar todas las bases de datos en el sistema, asi se puede ver cuantas bases estan activas.