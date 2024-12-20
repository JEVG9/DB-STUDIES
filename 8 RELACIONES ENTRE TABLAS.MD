# RELACIONES ENTRE TABLAS


En __SQL__, las relaciones entre tablas son un concepto fundamental para organizar y gestionar datos relacionados en bases de datos relacionales. Estas relaciones permiten vincular información de diferentes tablas mediante claves (primarias y foráneas) para evitar la redundancia y mantener la consistencia de los datos.

## RELACION 1:1

Esta relacion indica que cada registro en una tabla esta asociado
a un unico registro en otra tabla y viceversa.

Si tenemos una tabla llamada `personas` y `pasaportes`, cada persona tine un
solo pasaporte asociado y viceversa. Esto se lograria indicando una clave
primaria.

### Ejemplo:

En el siguiente ejemplo se muestra como seria 
una query con lo descrito anteriormente.

```SQL
CREATE TABLE personas (
    id INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE pasaportes (
    id INT PRIMARY KEY,
    id_persona INT UNIQUE,
    numero VARCHAR(20),
    FOREIGN KEY (id_persona) REFERENCES personas(id)
);
```

`id_persona` es una clave foránea (foreign key) que establece una relación con la columna `id` en la tabla `personas`.
Esto asegura que solo se puedan agregar valores en `id_persona` que ya existan en la columna `id` de la tabla personas.
Esta restricción mantiene la integridad referencial entre las tablas. Si intentas insertar un valor en `id_persona` que no exista en `personas.id`, obtendrás un error.

Supongamos que agregamos los siguientes datos:

Insertar en personas:
```SQL
INSERT INTO personas (id, nombre) VALUES (1, 'Juan Pérez');
INSERT INTO personas (id, nombre) VALUES (2, 'María López');
```

Insertar en pasaportes:
```SQL
INSERT INTO pasaportes (id, id_persona, numero) VALUES (1, 1, 'ABC123');
INSERT INTO pasaportes (id, id_persona, numero) VALUES (2, 2, 'DEF456');
```
Resultado:
En la tabla personas, tenemos dos personas: Juan Pérez y María López.
En la tabla pasaportes, el pasaporte con número ABC123 pertenece a Juan Pérez, y el pasaporte con número DEF456 pertenece a María López.

## RELACION 1:N

En esta relación, un registro en la tabla "*padre*" puede estar relacionado con múltiples registros en la tabla "*hija*". Sin embargo, cada registro de la tabla "*hija*" solo está asociado con un registro de la tabla "*padre*".

### Ejemplo:

Una tabla `departamentos` y una tabla `empleados`, donde un departamento puede tener muchos empleados, pero un empleado pertenece a un solo departamento.

```SQL
CREATE TABLE departamentos (
    id INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    id_departamento INT,
    FOREIGN KEY (id_departamento) REFERENCES departamentos(id)
);
```

En este ejemplo se ven como se crean dos
tablas `departamentos` y `empleados` donde cada empleado en `empleados` tendra 
asignada como referencia `id` de departamentsos como `id_departamento`. Lo que indicara que cada empleado tendra asociado un id referente al departamento al que pertenece.

Insertar datos en departamentos:
```SQL
INSERT INTO departamentos (id, nombre) VALUES (1, 'Ventas');
INSERT INTO departamentos (id, nombre) VALUES (2, 'Recursos Humanos');
INSERT INTO departamentos (id, nombre) VALUES (3, 'Marketing');
```

Insertar datos en empleados:
```SQL
INSERT INTO empleados (id, nombre, id_departamento) VALUES (1, 'Juan Pérez', 1);
INSERT INTO empleados (id, nombre, id_departamento) VALUES (2, 'Ana Gómez', 2);
INSERT INTO empleados (id, nombre, id_departamento) VALUES (3, 'Carlos Díaz', 1);
```

## RELACION N:M

Esta relacon indica que una cantidad `n` de elementos estan relacionados con `m` elementos y viceversa.

Este tipo de relacion se maneja de manera general con tablas intermedias que son las que guardan las relaciones, de esta manera se hace mas simple el uso de este tipo de referenciacion.

### Ejemplo:

Una tabla `estudiantes` y una tabla `cursos`, donde un estudiante puede inscribirse en varios `cursos`, y un curso puede tener varios estudiantes.

Usando una tabla intermedia que contenga las claves foráneas de ambas tablas relacionadas.
```SQL
CREATE TABLE estudiantes (
    id INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE cursos (
    id INT PRIMARY KEY,
    nombre VARCHAR(50)
);

CREATE TABLE inscripciones (
    id_estudiante INT,
    id_curso INT,
    PRIMARY KEY (id_estudiante, id_curso),
    FOREIGN KEY (id_estudiante) REFERENCES estudiantes(id),
    FOREIGN KEY (id_curso) REFERENCES cursos(id)
);
```

En el ejemplo anterior las tablas principales
son `estudiantes` y `cursos` y la tabla
intermedia es `inscripciones`.

La tabla `inscripciones` es la tabla que se
utiliza para gestionar la relacion de N:M, y se
usaria tal que asi:

Insertar datos en estudiantes:

```SQL
INSERT INTO estudiantes (id, nombre) VALUES (1, 'Juan Pérez');
INSERT INTO estudiantes (id, nombre) VALUES (2, 'Ana Gómez');
INSERT INTO estudiantes (id, nombre) VALUES (3, 'Carlos Díaz');
```

Insertar datos en cursos:


```SQL
INSERT INTO cursos (id, nombre) VALUES (1, 'Matemáticas');
INSERT INTO cursos (id, nombre) VALUES (2, 'Física');
INSERT INTO cursos (id, nombre) VALUES (3, 'Programación');
```

Insertar datos en inscripciones:

```SQL
INSERT INTO inscripciones (id_estudiante, id_curso) VALUES (1, 1); -- Juan en Matemáticas
INSERT INTO inscripciones (id_estudiante, id_curso) VALUES (1, 2); -- Juan en Física
INSERT INTO inscripciones (id_estudiante, id_curso) VALUES (2, 3); -- Ana en Programación
INSERT INTO inscripciones (id_estudiante, id_curso) VALUES (3, 1); -- Carlos en Matemáticas
INSERT INTO inscripciones (id_estudiante, id_curso) VALUES (3, 3); -- Carlos en Programación
```

## ESTRUCTURAS DE CONSULTAS CON LAS RELACIONES ENTRE TABLAS

Lo siguiente son ejemplos muy basicos y generales de casos de consultas con las diferentes relaciones entre tablas.

### 1:1

**Resumen**: Cada fila en la tabla A está asociada con exactamente una fila en la tabla B, y viceversa.

_`JOIN` se usa para combinar las dos tablas mediante la clave primaria y foránea compartida._

```SQL
SELECT A.columna1, A.columna2, B.columna1, B.columna2
FROM TablaA A
JOIN TablaB B ON A.id = B.id;
```
### 1:N

**Resumen**: Una fila en la tabla A puede estar asociada con múltiples filas en la tabla B.

```SQL
SELECT A.columna1, B.columna1, B.columna2
FROM TablaA A
JOIN TablaB B ON A.id = B.id_tablaA;
```

### N:M

**Resumen**: Varias filas en la tabla A pueden estar asociadas con varias filas en la tabla B, y viceversa. Una tabla intermedia (de unión) gestiona estas relaciones.

```SQL
SELECT A.columna1, B.columna1
FROM TablaA A
JOIN TablaIntermedia C ON A.id = C.id_tablaA
JOIN TablaB B ON B.id = C.id_tablaB;
```

Estos son selecciones simples, pero todas las demas operaciones son posibles en cuanto a las relaciones entre tablas.

## AUTOREFERENCIA

En una propia tabla se puede tener una relacion propia con ella misma, esto puede
servir para simplificar relaciones sin agregar mas tablas.

Las autorreferencias son útiles para modelar estructuras jerárquicas o dependencias dentro de los datos, como árboles, gráficos o relaciones entre entidades del mismo tipo

Este seria un ejemplo:
```SQL
CREATE TABLE empleados (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    id_jefe INT,
    FOREIGN KEY (id_jefe) REFERENCES empleados(id)
);
```

En este caso cada empleado tiene un jefe asignado, pero tambien da cabida a que un empleado sea el jefe de otro, y pues tambien referenciandose a si mismo seria el jefe como tal.