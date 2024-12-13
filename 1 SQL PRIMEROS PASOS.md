# BASES DE DATOS SQL


* El nombre de __SQL__ significa structured query lenguage.


Como se menciono anteriormente, SQL es un tipo de base datos que se enfoca en la estructuracion de los datos mediante relaciones de tablas.

Es un tipo de base de datos que en realidad es un estandar ya ampliamente usado dada su historia de existencia y uso.

## Repaso

Las DBs SQL estan estandarizadas lo que hace que las diferentes bases de datos solo tengan pequenas diferencias en como se llaman, como se ejecutan, etc pero en cuanto a como se programan no es diferente.

## Entidad

Las bases de datos sirven para representar datos, como tal de manera mas estructuradas objetos de bases de datos, donde cada objeto representa algun tipo de dato.

## Tipos de datos

| **Categoría**         | **Tipo de Dato**                | **Descripción**                                                                 |
|------------------------|---------------------------------|---------------------------------------------------------------------------------|
| **Numéricos**          | `TINYINT`                      | Enteros pequeños (1 byte).                                                    |
|                        | `SMALLINT`                    | Enteros más grandes (2 bytes).                                                |
|                        | `INT` / `INTEGER`             | Enteros estándar (4 bytes).                                                   |
|                        | `BIGINT`                      | Enteros grandes (8 bytes).                                                    |
|                        | `DECIMAL` / `NUMERIC`         | Alta precisión, ideal para datos financieros.                                 |
|                        | `FLOAT`                       | Número de punto flotante de precisión baja.                                   |
|                        | `DOUBLE` / `REAL`             | Punto flotante con mayor precisión.                                           |
| **Caracteres**         | `CHAR(n)`                     | Cadena de longitud fija de `n` caracteres.                                    |
|                        | `VARCHAR(n)`                  | Cadena de longitud variable de hasta `n` caracteres.                         |
|                        | `TEXT`                        | Texto largo, como descripciones o comentarios.                                |
| **Fecha y Hora**       | `DATE`                        | Fecha en formato `AAAA-MM-DD`.                                                |
|                        | `YEAR`                        | Solo el año.                                                                  |
|                        | `TIME`                        | Hora en formato `HH:MM:SS`.                                                   |
|                        | `DATETIME`                   | Fecha y hora exactas.                                                         |
|                        | `TIMESTAMP`                  | Fecha y hora con información de zona horaria.                                 |
| **Booleanos**          | `BOOLEAN`                    | Valores lógicos (`TRUE` o `FALSE`).                                           |
| **Binarios**           | `BLOB`                       | Datos binarios, como imágenes o archivos.                                     |
| **JSON y XML**         | `JSON`                       | Almacena datos en formato JSON.                                               |
|                        | `XML`                        | Almacena datos en formato XML.                                                |
| **Otros**              | `ENUM`                       | Lista de valores predefinidos; la columna debe contener uno de estos valores. |
|                        | `SET`                        | Lista de valores predefinidos; permite múltiples selecciones.                 |
|                        | `GEOMETRY`                   | Datos espaciales, como puntos, líneas o polígonos.                            |
---------------------------

Cada motor de base de datos especifica las limitaciones de cada tipo de dato, como tal cada tipo de dato puede variar en nombre y limitaciones pero en general son tipos de datos que se comportan igual.

Este preparativo se hace en torno a MySQL, usando ademas su workbench, por lo que los tipos de datos de MySQL son:

| **Categoría**         | **Tipo de Dato**           | **Descripción**                                                                 |
|------------------------|----------------------------|---------------------------------------------------------------------------------|
| **Numéricos**          | `TINYINT`                 | Entero pequeño (1 byte), rango: -128 a 127 (sin signo: 0 a 255).               |
|                        | `SMALLINT`               | Entero más grande (2 bytes), rango: -32,768 a 32,767 (sin signo: 0 a 65,535).  |
|                        | `MEDIUMINT`              | Entero medio (3 bytes), rango: -8,388,608 a 8,388,607 (sin signo: 0 a 16M).    |
|                        | `INT` / `INTEGER`        | Entero estándar (4 bytes), rango: -2B a 2B (sin signo: 0 a 4B).                |
|                        | `BIGINT`                 | Entero grande (8 bytes), rango: -9Q a 9Q (sin signo: 0 a 18Q).                 |
|                        | `DECIMAL` / `NUMERIC`    | Números exactos de punto fijo. Definido como `DECIMAL(M, D)`.                  |
|                        | `FLOAT`                  | Número de punto flotante de precisión simple.                                  |
|                        | `DOUBLE` / `REAL`        | Punto flotante de doble precisión.                                             |
|                        | `BIT`                    | Valores binarios de longitud fija (1 a 64 bits).                               |
| **Caracteres**         | `CHAR(n)`                | Cadena de texto fija de longitud `n` (1 a 255).                                |
|                        | `VARCHAR(n)`             | Cadena de longitud variable de hasta `n` caracteres (1 a 65,535 dependiendo de la fila). |
|                        | `TINYTEXT`               | Texto muy corto (hasta 255 caracteres).                                        |
|                        | `TEXT`                   | Texto de tamaño mediano (hasta 65,535 caracteres).                             |
|                        | `MEDIUMTEXT`             | Texto grande (hasta 16,777,215 caracteres).                                    |
|                        | `LONGTEXT`               | Texto muy grande (hasta 4,294,967,295 caracteres).                             |
| **Fecha y Hora**       | `DATE`                   | Fecha en formato `AAAA-MM-DD`.                                                 |
|                        | `DATETIME`               | Fecha y hora combinadas, rango amplio.                                         |
|                        | `TIMESTAMP`              | Fecha y hora relativas a UTC.                                                   |
|                        | `TIME`                   | Solo la hora (`HH:MM:SS`).                                                     |
|                        | `YEAR`                   | Solo el año (formato `AAAA`).                                                  |
| **Booleanos**          | `BOOLEAN` / `BOOL`       | Alias de `TINYINT(1)`, valores 0 (falso) o 1 (verdadero).                      |
| **Binarios**           | `BINARY(n)`              | Cadena binaria fija de longitud `n`.                                           |
|                        | `VARBINARY(n)`           | Cadena binaria de longitud variable hasta `n`.                                 |
|                        | `TINYBLOB`               | Datos binarios pequeños (hasta 255 bytes).                                     |
|                        | `BLOB`                   | Datos binarios medianos (hasta 65,535 bytes).                                  |
|                        | `MEDIUMBLOB`             | Datos binarios grandes (hasta 16,777,215 bytes).                               |
|                        | `LONGBLOB`               | Datos binarios muy grandes (hasta 4,294,967,295 bytes).                        |
| **JSON y Espaciales**  | `JSON`                   | Almacena datos en formato JSON (desde MySQL 5.7).                              |
|                        | `GEOMETRY`               | Representación geoespacial genérica.                                           |
|                        | `POINT`                  | Coordenadas geográficas de un punto.                                           |
|                        | `LINESTRING`             | Línea geoespacial (secuencia de puntos).                                       |
|                        | `POLYGON`                | Polígono geoespacial.                                                          |
|                        | `MULTIPOINT`             | Conjunto de puntos geoespaciales.                                              |
|                        | `MULTILINESTRING`        | Conjunto de líneas geoespaciales.                                              |
|                        | `MULTIPOLYGON`           | Conjunto de polígonos geoespaciales.                                           |
|                        | `GEOMETRYCOLLECTION`     | Colección de objetos geoespaciales.                                            |
| **Especiales**         | `ENUM`                   | Lista de valores predefinidos; cada columna toma un valor de esta lista.       |
|                        | `SET`                    | Lista de valores predefinidos; permite múltiples selecciones.                  |

## Tablas

Al momento de crear tablas estas contienen columnas que indicaran que atributos tendran, ej:

```
TABLA: JUGADORES DE LOL
C1: ID
C2: USERNAME
C3: PL
C4: REGION
C5: TEAM
```
En el ejemplo anterior la tabla `JUGADORES DE LOL` se forma por las columas `C1...C5` y cada una contendra los datos referentes.

### Columnas

las columnas que indican el atributo de cada tabla se crean con:

 - nombre
 - tipo de dato
 - caracteristica de esa columna
 - valor por defecto

Al crear la columna se definen los parametros anteriores y sin importar el metodo(query o visual) el resultado sera el mismo.

### Nombre

El nombre de la columna tiene solo esa funcion y caracteristica.

### Tipo de dato

Los tipos de datos seran dependientes del sistema usado y la seleccion del uso que se le vaya a dar.

### Caracteristica

Existen varias caracteristicas que determinaran el comportamiento de la columna:

- `NOT NULL`: La columna debe tener un valor, no puede ser nula.
- `UNIQUE`: Los valores de la columna deben ser únicos dentro de la tabla.
- `PRIMARY KEY`: Identifica un registro de forma única dentro de la tabla.
- `FOREIGN KEY`: Establece una relación con otra tabla, creando una integridad referencial.
- `AUTO_INCREMENT`: Incrementa automáticamente el valor de la columna, útil para claves primarias.
- `INDEX`: Mejora el rendimiento de las consultas al crear un índice en la columna.

## Ejemplo de uso

```SQL
CREATE TABLE usuarios (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    edad INT,
    fecha_nacimiento DATE,
    activo BOOLEAN DEFAULT TRUE
);
```

Este ejemplo crea una tabla de usuarios con las columnas id, nombre, email, edad, fecha de nacimiento, activo. Cada uno de  esos datos esta definido con su tipo de dato y su caracteristica.