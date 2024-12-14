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
##
##
