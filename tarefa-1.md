# Tarefa 1
<!--DDL-> https://github.com/ToniChoren/BasesDeDatos/blob/master/ApuntesDDL/README.md
   DML -> https://github.com/ToniChoren/BasesDeDatos/blob/master/ApuntesDML/README.md -->
# Apuntes DDL


# Indice

1. [Introducción DDL](#1-Introducción-DDL)
2. [Creación de bases de datos](#2-Creación-de-bases-de-datos)
3. [Creación de bases de datos](#3-Creacion-de-tablas)
4. [Tipos de datos](#4-Tipos-de-datos)
5. [Dominios](#5-Dominios)
6. [Consultar el diccionario de datos](#6-Consultar-el-diccionario-de-datos)
7. [Borrar tuplas](#7-Borrar-tablas)
8. [Modificar tablas](#8-Modifica-tablas)

	8.1 [Cambiar de nombre a una tabla](#8.1)
	
	8.2 [Borrar contenido a una tabla](#8.2)	
	
	8.3 [Añadir columnas](#8.3)
	
	8.4 [Borrar columnas](#8.4)
	
	8.5 [Modificar columnas](#8.5)	
	
	8.6 [Renombrar una columna](#8.6)
	
	8.7 [Valor por defecto](#8.7)
	
9. [Restricciones](#-Restricciones)

	9.1 [Prohibir nulos](#9.1)
	
	9.2 [Valores únicos](#9.2)
	
	9.3 [Clave Primaria](#9.3)
	
	9.4 [Valores Foránea](#9.4)
	
	9.5 [Restricciones de vaoración](#9.5)

***


### 1 Introducción DDL

El DDL es la parte del lenguaje SQL que realiza la función de definición de datos del SGBD. Fundamentalmente se encarga de la creación, modificación y eliminación de los objetos de la base de datos (es decir de los metadatos). Por supuesto es el encargado de la creación de las tablas.

 Cada usuario de una base de datos posee un esquema. El esquema suele tener el mismo nombre que el usuario y sirve para almacenar los objetos de esquema, es decir los objetos que posee el usuario. 

Esos objetos pueden ser: tablas, vistas, índices y otras objetos relacionados con la definición de la base de datos. Los objetos son manipulados y creados por los usuarios. En principio sólo los administradores y los usuarios propietarios pueden acceder a cada objeto, salvo que se modifiquen los privilegios del objeto para permitir el acceso a otros usuarios. 

Hay que tener en cuenta que ninguna instrucción DDL puede ser anulada por una instrucción ROLLBACK (la instrucción ROLLBACK está relacionada con el uso de transacciones que se comentarán más adelante) por lo que hay que tener mucha precaución a la hora de utilizarlas. Es decir, las instrucciones DDL generan acciones que no se pueden deshacer (salvo que dispongamos de alguna copia de seguridad).

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 2 Creación de bases de datos

El comando SQL de creación de una base de datos es CREATE DATABASE. Este comando crea una base de datos con el nombre que se indique. Ejemplo:
~~~SQL
CREATE DATABASE prueba;
~~~

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 3 Creacion de tablas

El nombre de las tablas deben cumplir las siguientes reglas: 

- Deben comenzar con una letra 
-  No deben tener más de 30 caracteres 
- Sólo se permiten utilizar letras del alfabeto (inglés), números o el signo de subrayado (también el signo $ y #, pero esos se utilizan de manera especial por lo que no son recomendados) 
- No puede haber dos tablas con el mismo nombre para el mismo esquema (pueden coincidir los nombres si están en distintos esquemas)  
- No puede coincidir con el nombre de una palabra reservada SQL (por ejemplo no se puede llamar SELECT a una tabla)

**CREATE TABLE**
 Es la orden SQL que permite crear una tabla:

~~~SQL
CREATE TABLE nombreTabla(
Dato1 INTEGER [NOT NULL] PRYMARY KEY,
Dato2 VARCHAR(30),
Dato1 CHAR(10)
);
~~~

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 4 Tipos de datos
A la hora de crear tablas, hay que indicar el tipo de datos de cada campo. Necesitamos pues conocer los distintos tipos de datos. Estos son:

|Descripción | Tipo Dato|
|---------------|----------|
| Texto anchura fija  |  CHARACTER(n) ò CHAR(n)|
|  Texto de anchura variable  |    VARCHAR (n)            |
|Enteros pequeños (2 bytes)|SMALLINT |
|Enteros normales (4 bytes)|INTEGER o INT|
|Enteros largos (8 bytes)|BIGUINT|
|Decimal de coma variable|FLOAT|
|Decimal de coma variable|DOUBLE|
|Fechas|DATE|
|Lógicos|BOOLEAN o BOOL|
|Monedas 8 bytes|MONEY|

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 5 Dominios
Se trata de CREATE DOMAIN:

Ejemplo: 

~~~SQL
CREATE DOMAIN Tdireccion AS VARCHAR(3); 
~~~

Gracias a esa instrucción podemos crear la siguiente tabla:
~~~SQL
 CREATE TABLE personal(
  codPers SMALLINT, 
  nombre VARCHAR(30), 
  direccion Tdireccion 
  );
~~~

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 6 Consultar el diccionario de datos

El diccionario de datos es accesible mediante el esquema  de información (INFORMATION_SCHEMA), un esquema especial que contiene el conjunto de vistas con el que se pueden consultar metadatos de la base de
datos.
 En concreto la vista INFORMATION_SCHEMA.TABLES obtiene una vista de
las tablas creadas. Es decir:
~~~SQL
SELECT * FROM INFORMATION_SCHEMA.TABLES
~~~

### 7 Borrar tablas
La orden __DROP TABLE__ seguida del nombre de una tabla, permite eliminar la tabla en cuestión.
Normalmente, el borrado de una tabla es irreversible, y no hay ninguna petición de confirmación, por lo que conviene ser muy cuidadoso con esta operación.

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 8 Modifica tablas

__1. Cambiar de nombre a una tabla__ <a name="8.1"> </a>
~~~SQL
ALTER TABLE nombreViejo RENAME TO nombreNuevo;
~~~

__2. Borrar contenido de tablas__ <a name="8.2"> </a>

Se dispone de una orden no estándar para eliminar definitivamente los datos de una tabla; es la orden __TRUNCATE TABLE__ seguida del nombre de la tabla a borrar. Hace que se elimine el contenido de la tabla, pero no la estructura de la tabla en sí. Incluso borra del archivo de datos el espacio ocupado por la tabla.

__3. Añadir columnas__ <a name="8.3"> </a>

Permite añadir nuevas columnas a la tabla. Se deben indicar su tipo de datos y sus propiedades si es necesario (al estilo de CREATE TABLE). Las nuevas columnas se añaden al final, no se puede indicar otra posición (hay que recordar que el orden de las columnas no importa).
~~~SQL
ALTER TABLE facturas ADD (fecha DATE);
~~~


__4. Borrar columnas__ <a name="8.4"> </a>

Elimina la columna indicada de manera irreversible e incluyendo los datos que contenía. No se puede eliminar la única columna de una tabla que sólo tiene esa columna (habrá que usar DROP TABLE). 
~~~SQL
ALTER TABLE facturas DROP (fecha);
~~~
__5. Modificar columnas__ <a name="8.5"> </a>

Permite cambiar el tipo de datos y propiedades de una determinada columna. Sintaxis:
~~~SQL
ALTER TABLE facturas MODIFY(fecha TIMESTAMP);
~~~


__6. Renombrar una columna__ <a name="8.6"> </a>

Esto permite cambiar el nombre de una columna. 
Sintaxis 
~~~SQL
ALTER TABLE nombreTabla 
RENAME COLUMN nombreAntiguo TO nombreNuevo 
~~~
Ejemplo:
~~~SQL
 ALTER TABLE facturas RENAME COLUMN fecha TO fechaYhora;
~~~
__7. Valor por defecto__ <a name="8.7"> </a>

A cada columna se le puede asignar un valor por defecto durante su creación mediante la propiedad __DEFAULT.__ Se puede poner esta propiedad durante la creación o modificación de la tabla, añadiendo la palabra __DEFAULT__ tras el tipo de datos del campo y colocando detrás el valor que se desea por defecto.

Ejemplo:
~~~SQL 
  CREATE TABLE articulo (cod NUMBER(7), nombre VARCHAR2(25), precio NUMBER(11,2) DEFAULT 3.5); 
~~~
La palabra DEFAULT se puede añadir durante la creación o la modificación de la tabla (comando ALTER TABLE)

[⬆⬆ INDICE ⬆⬆](#INDICE)

***

### 9 Restricciones

Una restricción es una condición de obligado cumplimiento para una o más columnas de la tabla. No se puede repetir.
Se aconseja la siguiente regla a la hora de poner nombre a las restricciones:  
- Tres letras para el nombre de la tabla 
- Carácter de subrayado  
- Tres letras con la columna afectada por la restricción 
- Carácter de subrayado 
- Dos letras con la abreviatura del tipo de restricción. La abreviatura puede ser: 
	- __NN__. NOT NULL.  
	- __PK__. PRIMARY KEY 
	- __UK__. UNIQUE 
	- __FK__. FOREIGN KEY 
	- __CK__. CHECK (validación) 

Por ejemplo para hacer que la clave principal de la tabla Alumnos sea el código del alumno, el nombre de la restricción podría ser:

	alu_cod_pk
			 
__1. Prohibir nulos__ <a name="9.1"> </a>

La restricción NOT NULL permite prohibir los nulos en una determinada tabla. Eso obliga a que la columna tenga que tener obligatoriamente un valor para que sea almacenado el registro. Se puede colocar durante la creación (o modificación) del campo añadiendo la palabra NOT NULL tras el tipo:
~~~SQL 
CREATE TABLE cliente(dni VARCHAR2(9) NOT NULL);
~~~

__2. Valores únicos__ <a name="9.2"> </a>

Las restricciones de tipo UNIQUE obligan a que el contenido de una o más columnas no puedan repetir valores. Nuevamente hay dos formas de colocar esta restricción:

~~~SQL
CREATE TABLE cliente(dni VARCHAR2(9) UNIQUE);
~~~
__3. Clave Primaria__ <a name="9.3"> </a>

La clave primaria de una tabla la forman las columnas que indican a cada registro de la misma. La clave primaria hace que los campos que la forman sean NOT NULL (sin posibilidad de quedar vacíos) y que los valores de los campos sean de tipo UNIQUE (sin posibilidad de repetición). 

Si la clave está formada por un solo campo basta con:
~~~SQL
CREATE TABLE cliente( 
dni VARCHAR(9) PRIMARY KEY, 
nombre VARCHAR(50)
);
~~~
Poniendo un nombre a la restricción:

~~~SQL
CREATE TABLE cliente( dni VARCHAR(9) CONSTRAINT cliente_pk PRIMARY KEY, 
nombre VARCHAR(50)
);
~~~
Si la clave está formada por más de un campo:
~~~SQL
CREATE TABLE alquiler,
dni VARCHAR(9), 
cod_pelicula INTEGER(5), 
CONSTRAINT alquiler_pk 
PRIMARY KEY(dni,cod_pelicula)) ;
~~~

__4. Clave foránea__ <a name="9.4"> </a>

Una clave secundaria o foránea, es uno o más campos de una tabla que están relacionados con la clave principal.

~~~SQL
CREATE TABLE alquiler( 
dni VARCHAR2(9) CONSTRAINT dni_fk REFERENCES clientes, 
cod_pelicula NUMBER(5) CONSTRAINT pelicula_fk REFERENCES peliculas, 
CONSTRAINT alquiler_pk PRIMARY KEY(dni,cod_pelicula) 
);
~~~


La integridad referencial es una herramienta imprescindible de las bases de datos relacionales. Pero provoca varios problemas. Por ejemplo, si borramos un registro en la tabla principal que está relacionado con uno o varios de la secundaria ocurrirá un error, ya que de permitírsenos borrar el registro ocurrirá fallo de integridad (habrá claves secundarios refiriéndose a una clave principal que ya no existe). 

Por ello se nos pueden ofrecer soluciones a añadir tras la cláusula REFERENCES. 
Son:
- __ON DELETE SET NULL.__ Coloca nulos todas las claves secundarias relacionadas con la borrada. 
- __ON DELETE CASCADE.__ Borra todos los registros cuya clave secundaria es igual que la clave del registro borrado. 
- __ON DELETE SET DEFAULT.__ Coloca en el registro relacionado el valor por defecto en la columna relacionada
- __ON DELETE NOTHING.__ No hace nada.

En el caso explicado se aplicarían las cláusulas cuando se eliminen filas de la clave principal relacionada con la clave secundaria. En esas cuatro cláusulas se podría sustituir la palabra __DELETE__ por la palabra __UPDATE,__ haciendo que el funcionamiento se refiera a cuando se modifica un registro de la tabla principal; en muchas bases de datos se admite el uso tanto de ON DELETE como de ON UPDATE.

Ejemplo
~~~SQL
CREATE TABLE alquiler(dni VARCHAR(9), 
cod_pelicula NUMBER(5), 
CONSTRAINT alquiler_pk PRIMARY KEY(dni,cod_pelicula), 
CONSTRAINT dni_fk FOREIGN KEY (dni) REFERENCES clientes(dni) 
ON DELETE SET NULL, 
CONSTRAINT pelicula_fk FOREIGN KEY (cod_pelicula) 
REFERENCES peliculas(cod) 
ON DELETE CASCADE );
~~~

__5. Restricción de validación__ <a name="9.5"> </a>

Son restricciones que dictan una condición que deben cumplir los contenidos de una columna. Una misma columna puede tener múltiples CHECKS en su definición (se pondrían varios CONSTRAINT seguidos, sin comas)

~~~SQL
CREATE TABLE ingresos(
cod INTEGER(5) PRIMARY KEY, 
concepto VARCHAR(40) NOT NULL, 
importe MONEY(11,2) CONSTRAINT importe_min 
CHECK (importe>0) 
CONSTRAINT importe_max 
CHECK (importe<8000) );
~~~

[⬆⬆ INDICE ⬆⬆](#INDICE)

***
# Apuntes DML


# Indice

1. [Introducción DML](#1)
2. [Insercción de datos(INSERT)](#2)
3. [Actualizacion de registros(UPDATE)](#3)
4. [Borrado de registros(DELETE)](#4)
	
***

# 1 Introducción DML <a name="1"></a>

Es una de las partes fundamentales del lenguaje SQL. El DML (Data Manipulation Language) __lo forman las instrucciones capaces de modificar los datos de las tablas.__ Al conjunto de instrucciones DML que se ejecutan consecutivamente, se las llama transacciones y se pueden anular todas ellas o aceptar, ya que una instrucción DML no es realmente efectuada hasta que no se acepta (COMMIT)

___

# 2 Insercción de datos(INSERT) <a name="2"></a>

La adición de datos a una tabla se realiza mediante la instrucción INSERT. 

  Su sintaxis fundamental es:
  
 ~~~SQL
  INSERT INTO tabla [(listaDeCampos)]
  VALUES (valor1 [,valor2 ...])
~~~
Ejemplo:

 ~~~SQL
  INSERT INTO informatica
  VALUES 
  ('valor1','valor2', 'valor3', ),
  ('valor1','valor2', 'valor3', ),
  ('valor1','valor2', 'valor3', );
~~~

___

# 3 Actualizacion de registros(UPDATE) <a name="3"></a>

La modificación de los datos de los registros lo implementa la instrucción UPDATE. 
Sintaxis:

 ~~~SQL
UPDATE clientes
SET name='Ourense',
WHERE provincia='Orense';
~~~
El primer dato actualiza la provincia de los clientes de Orense para que aparezca
como Ourense. 

___

# 4 Borrado de registros(DELETE) <a name="4"></a>

Se realiza mediante la instrucción DELETE.

Es más sencilla que las anteriores, elimina los registros de la tabla que cumplan
la condición indicada. Ejemplo:

 ~~~SQL
DELETE FROM empleados
WHERE seccion=23;
 ~~~
 
 [⬆⬆ INDICE ⬆⬆](#Indice)

***








