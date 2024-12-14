# ESCRITURA DE DATOS

## INSERT INTO
### Sintaxis:

```SQL
INSERT INTO <table> (col1,...,colN)
VALUES (val1,...,valN);

or

INSERT INTO <table> (col1,...,colN)
<SELECT QUERY)>
ˋˋˋ

Este comando se usa para poder agregar datos a las filas indicadas,
El comando se puede usar agregando valores directamente usando
el elemento ˋVALUEˋ para indicar los valores con parentesis y comas.

Las querys tambien pueden servir para agregar elementos con este
comando, usando ˋSELECTˋ y la respectiva query que incluso puede
ser combinada con todas las demas combinaciones para hacer querys.

#### Ejemplo con ˋVALUEˋ:

ˋˋˋSQL
INSERT INTO users (name,age)
VALUES 
    ('Carlos',40),
    ('Neko',19);
ˋˋˋ

Este ejemplo agrega a la tabla ˋusersˋ 4 datos en 2 columnas
de datos ˋnameˋ y ˋageˋ respectivamente en cada uno.

#### Otro ejemplo pero con ˋSELECTˋ:

ˋˋˋSQL
INSERT INTO users(name,age)
SELECT name,age
FROM employees
WHERE age>30;
ˋˋˋ
En este ultimo ejemplo se agregan los datos ˋageˋ y ˋnameˋ de la
tabla ˋemployeesˋ que tengan mas de ˋ30ˋ como edad a la tabla ˋusersˋ

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
