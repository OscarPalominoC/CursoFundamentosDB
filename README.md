# Curso de Fundamentos de Bases de Datos

![Logo](https://static.platzi.com/media/achievements/badge-fundamentos-de-bases-de-datos-cc5eff2a-a7e0-4110-af5d-a47b628611da.png)

**Instructor**: Israel Vázquez Morales

## Reto

### Platzi Blog

A través de la creación de un sistema de blogs obtendrás las habilidades necesarias para realizar un CRUD (Create, Read, Update, Delete) para aplicarlo en base de datos relacionales como no relacionales.

## Archivos

* [Slides](/files/fundamentos-de-bases-de-datos.pdf)

## Indice

1. [Bienvenida conceptos básicos y contexto histórico de las Bases de Datos](#bienvenida-conceptos-básicos-y-contexto-histórico-de-las-bases-de-datos)
    * [Bienvenida conceptos básicos y contexto histórico de las Bases de Datos](#bienvenida-conceptos-básicos-y-contexto-histórico-de-las-bases-de-datos-1)
2. [Introducción a las bases de datos relacionales](#introducción-a-las-bases-de-datos-relacionales)
    * [Historia de las RDB](#historia-de-las-rdb)
    * [Entidades y atributos](#entidades-y-atributos)
    * [Entidades de Platzi Blog](#entidades-de-platzi-blog)
    * [Relaciones](#relaciones)
    * [Múltiples muchos](#múltiples-muchos)
    * [Diagrama ER](#diagrama-er)
    * [Diagrama Físico: tipos de datos y constraints](#diagrama-físico-tipos-de-datos-y-constraints)
    * [Diagrama Físico: normalización](#diagrama-físico-normalización)
    * [Diagrama Físico: normalizando Platziblog](#diagrama-físico-normalizando-platziblog)
    * [Formas normales en DB relacionales](#formas-normales-en-db-relacionales)
3. [RDBMS (MySQL) o cómo hacer lo anterior de manera práctica](#rdbms-mysql-o-cómo-hacer-lo-anterior-de-manera-práctica)
    * [RDB ¿Qué?](#rdb-que)
    * [Clientes gráficos](#clientes-gráficos)
    * [Servicios administrados](#servicios-administrados)
4. [SQL hasta en la sopa](#sql-hasta-en-la-sopa)
    * [Historia de SQL](#historia-de-sql)
    * [DDL create](#ddl-create)
    * [CREATE VIEW y DDL ALTER](#create-view-y-ddl-alter)
    * [DDL drop](#ddl-drop)
    * [DML](#dml-1)
    * [¿Qué tan standard es SQL?](#qué-tan-standard-es-sql)
    * [Creando Platziblog: tablas independientes](#creando-platziblog-tablas-independientes)
    * [Creando Platziblog: tablas dependientes](#creando-platziblog-tablas-dependientes)
    * [Creando Platziblog: tablas transitivas](#creando-platziblog-tablas-transitivas)
5. [Consultas a una base de datos](#consultas-a-una-base-de-datos)
	* [¿Por qué las consultas son tan importantes?](#por-qué-las-consultas-son-tan-importantes)
	* [Estructura básica de un Query](#estructura-básica-de-un-query)
	* [SELECT](#select)
	* [FROM](#from)
	* [Utilizando la sentencia FROM](#utilizando-la-sentencia-from)
	* [WHERE](#where
	* [Utilizando la sentencia WHERE nulo y no nulo](#utilizando-la-sentencia-where-nulo-y-no-nulo)
	* [GROUP BY](#group-by)
	* [ORDER BY y HAVING](#order-by-y-having)
	* [El interminable agujero de conejo (Nested queries)](#El-interminable-agujero-de-conejo-nested-queries)

---

# Bienvenida conceptos básicos y contexto histórico de las Bases de Datos

## Bienvenida conceptos básicos y contexto histórico de las Bases de Datos

Tu profesor será Israel Vázquez, senior web developer en San Francisco, seminarista de bases de datos y entusiasta data engineering.

El almacenamiento en la nube tiene un gran pro comparada con los otros métodos de almacenamiento ya que es accesible desde cualquier parte del mundo. Además es centralizada y puede ser usada por varias personas al mismo tiempo.

Las bases de datos entran cuando hacemos la transición a medios digitales.

### Tipos de bases de datos:

* **Relacionales**: En la industria hay varias compañías dedicadas a ser manejadoras de bases de datos relacionales como SQL Server, Oracle, MariaDB, entre otras.

![Relacionales](/images/relational-databases.PNG)

* **No relacionales**: Todavía están avanzando y existen ejemplos muy distintos como cassandra, elasticsearch, neo4j, MongoDB, entre otras.

![No relacionales](/images/non-relational-databases.PNG)

### Servicios:

* **Auto administrados**: Es la base de datos que instalas tú y te encargas de actualizaciones, mantenimiento, etc.
* **Administrados**: Servicios que ofrecen las nubes modernas como Azure y no debes preocuparte por mantenimiento o actualizaciones.

# Introducción a las bases de datos relacionales

## Historia de las RDB

Las bases de datos surgen de la necesidad de conservar la información más allá de lo que existe en la memoria RAM.

Las bases de datos basadas en archivos eran datos guardados en texto plano, fáciles de guardar pero muy difíciles de consultar y por la necesidad de mejorar esto nacen las bases de datos relacionales. Su inventor Edgar Codd dejó ciertas reglas para asegurarse de que toda la filosofía de las bases de datos no se perdiera, estandarizando el proceso.

[Codd's 12 rules](https://www.w3resource.com/sql/sql-basic/codd-12-rule-relation.php)

Las Reglas y mandamientos de Edgar Frank Ted Codd

### Regla 0: Regla de fundación.
1. Cualquier sistema que se proclame como relacional, debe ser capaz de gestionar sus bases de datos enteramente mediante sus capacidades relacionales.

### Regla 1: Regla de la información.
1. Todos los datos deben estar almacenados en las tablas
1. Esas tablas deben cumplir las premisas del modelo relacional
1. No puede haber información a la que accedemos por otra vía

### Regla 2: Regla del acceso garantizado.
1. Cualquier dato es accesible sabiendo la clave de su fila y el nombre de su columna o atributo
1. Si a un dato no podemos acceder de esta forma, no estamos usando un modelo relacional

### Regla 3: Regla del tratamiento sistemático de valores nulos.
1. Esos valores pueden dar significado a la columna que los contiene
1. El SGBD debe tener la capacidad de manejar valores nulos
1. El SGBD reconocerá este valor diferenciándolo de cualquier otro
1. El SGBD deberá aplicársele la lógica apropiada
1. Es un valor independiente del tipo de datos de la columna

### Regla 4: Catálogo dinámico en línea basado en el modelo relacional.
1. El catálogo en línea es el diccionario de datos
1. El diccionario de datos se debe de poder consultar usando las mismas técnicas que para los datos
1. Los metadatos, por tanto, se organizan también en tablas relacionales
1. Si SELECT es una instrucción que consulta datos, también será la que consulta los metadatos

### Regla 5: Regla comprensiva del sublenguaje de los datos completo.
1. Al menos tiene que existir un lenguaje capaz de hacer todas las funciones del SGBD
1. No puede haber funciones fuera de ese lenguaje
1. Puede haber otros lenguajes en el SGBD para hacer ciertas tareas
1. Pero esas tareas también se deben poder hacer con el “lenguaje completo”

### Regla 6: Regla de actualización de vistas.
1. Las vistas tienen que mostrar información actualizada
1. No puede haber diferencias entre los datos de las vistas y los datos de las tablas base

### Regla 7: Alto nivel de inserción, actualización, y cancelación.
1. La idea es que el lenguaje que maneja la base de datos sea muy humano
1. Eso implica que las operaciones del lenguaje de manipulación de los datos (DML) trabajen con conjuntos de filas a la vez
1. Para modificar, eliminar o añadir datos, no hará falta programar de la forma en la que lo hacen los lenguajes de tercera generación como C o Java

### Regla 8: Independencia física de los datos.
1. Cambios en la física de la BD no afecta a las aplicaciones ni a los esquemas lógicos
1. El acceso a las tablas (elemento lógico) no cambia porque la física de la base de datos cambie

### Regla 9: Independencias lógicas de los datos.
1. Cambios en el esquema lógico (tablas) de la BD no afectan al resto de esquemas
1. Si cambiamos nombres de tabla, o de columna o modificamos información de las filas, las aplicaciones (esquema externo) no se ven afectadas
1. Es más difícil de conseguir

### Regla 10: Independencia de la integridad.
1. Las reglas de integridad (restricciones) deben de ser gestionadas y almacenadas por el SGBD

### Regla 11: Independencia de la distribución.
1. Que la base de datos se almacene o gestione de forma distribuida en varios servidores, no afecta al uso de esta ni a la programación de las aplicaciones de usuario
1. El esquema lógico es el mismo independientemente de si la BD es distribuida o no

### Regla 12: La regla de la no subversión.
1. La base de datos no permitirá que exista un lenguaje o forma de acceso, que permita saltarse las reglas anteriores

## Entidades y atributos

Una entidad es algo similar a un objeto (programación orientada a objetos) y representa algo en el mundo real, incluso algo abstracto. Tienen atributos que son las cosas que los hacen ser una entidad y por convención se ponen en plural.

Los **atributos compuestos** son aquellos que tienen atributos ellos mismos.

Los **atributos llave** son aquellos que identifican a la entidad y no pueden ser repetidos. Existen:

* **Naturales**: son inherentes al objeto como el número de serie
* **Clave artificial**: no es inherente al objeto y se asigna de manera arbitraria.

**Entidades fuertes**: son entidades que pueden sobrevivir por sí solas.

![Entidad y atributos](/images/entidad-atributos.PNG)

**Entidades débiles**: no pueden existir sin una entidad fuerte y se representan con un cuadrado con doble línea.

* **Identidades débiles por identidad**: no se diferencian entre sí más que por la clave de su identidad fuerte.
![Identidad debil identidad](/images/entidades-debiles-identidad.PNG)
* **Identidades débiles por existencia**: se les asigna una clave propia.
![Identidad debil existencia](/images/entidades-debiles-existencia.PNG)

## Entidades de Platzi Blog

Nuestro proyecto será un manejador de Blogpost. Es un contexto familiar y nos representará retos muy interesantes.
* Primer paso: Identificar las entidades
* Segundo paso: Pensar en los atributos

**Mi proyecto**

Gestor de cuentas de amazon, netflix, hbo, en la que el cliente adquiere la cuenta, se guarda su información y sele avisa al propietario cuándo tiene que volver a pagar.

**Entidades y atributos**

users
* id
* name
* nickname
* password
* email

customer
* id
* name
* email
* phone
* address

streaming_companies
* id
* name

accounts_type
* id
* streaming_companies_id
* streams

sales
* id
* accounts_type_id
* customer_id
* prize
* purchase_date
* expiration_date
* Notes

## Relaciones

Las relaciones nos permiten ligar o unir nuestras diferentes entidades y se representan con rombos. Por convención se definen a través de verbos.

Las relaciones, representadas por un rombo, sirven para crear relaciones entre entidades. Por convención las relaciones son verbos que conectan entidades. Existen entidades multivaluadas o compuestas que tienen vida propia y se relacionan con otras entidades, por lo que se pueden normalizar (concepto que se explicará luego)

Las relaciones tienen una propiedad llamada cardinalidad y tiene que ver con números. Cuántos de un lado pertenecen a cuántos del otro lado:

* Cardinalidad: 1 a 1
* Cardinalidad: 0 a 1
* Cardinalidad: 1 a N
* Cardinalidad: 0 a N

![Relaciones](/images/relaciones.png)

## Múltiples muchos

También conocida como “Muchos a Muchos”. Es el tipo de cardinalidad en el que muchas entidades de un tipo, pertenecen a muchas entidades de otro, la cual debe ser normalizada y relacionada a partir de llaves foráneas.

## Diagrama ER

Un diagrama es como un mapa y nos ayuda a entender cuáles son las entidades con las que vamos a trabajar, cuáles son sus relaciones y qué papel van a jugar en las aplicaciones de la base de datos.

[Cardinalidades](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model#Cardinalities)

Los diagramas entidad-relación (ER) son fundamentales para modelar bases de datos tanto simples como complejas, pero las notaciones y figuras empleadas se pueden prestar a confusión. 

[Notación y símbolos de diagramas entidad-relación](https://www.lucidchart.com/pages/es/simbolos-de-diagramas-entidad-relacion)

![Diagrama ER](/images/diagrama-er.PNG)

## Diagrama Físico: tipos de datos y constraints

Para llevar a la práctica un diagrama debemos ir más allá y darle detalle con parámetros como:

Tipos de dato:

* **Texto**: CHAR(n), VARCHAR(n), TEXT
* **Números**: INTEGER, BIGINT, SMALLINT, DECIMAL(n,s), NUMERIC(n,s)
* **Fecha/hora**: DATE, TIME, DATETIME, TIMESTAMP
* **Lógicos**: BOOLEAN

Constraints (Restricciones)

* **NOT NULL**: Se asegura que la columna no tenga valores nulos
* **UNIQUE**: Se asegura que cada valor en la columna no se repita
* **PRIMARY KEY**: Es una combinación de NOT NULL y UNIQUE
* **FOREIGN KEY**: Identifica de manera única una tupla en otra tabla
* **CHECK**: Se asegura que el valor en la columna cumpla una condición dada
* **DEFAULT**: Coloca un valor por defecto cuando no hay un valor especificado
* **INDEX**: Se crea por columna para permitir búsquedas más rápidas

## Diagrama Físico: normalización

La normalización como su nombre lo indica nos ayuda a dejar todo de una forma normal. Esto obedece a las 12 reglas de Codd y nos permiten separar componentes en la base de datos:

**Sin normalizar**

![Sin normalizar](/images/sin-normalizar.PNG)

* **Primera forma normal (1FN)**: Atributos atómicos (Sin campos repetidos)
![1ra forma normal](/images/1ra-forma-normal.PNG)
* **Segunda forma normal (2FN)**: Cumple 1FN y cada campo de la tabla debe depender de una clave única.
![2da forma normal](/images/2da-forma-normal.PNG)
* **Tercera forma normal (3FN)**: Cumple 1FN y 2FN y los campos que NO son clave, NO deben tener dependencias.
![3ra forma normal](/images/3ra-forma-normal.PNG)
* **Cuarta forma normal (4FN)**: Cumple 1FN, 2FN, 3FN y los campos multivaluados se identifican por una clave única.
![4ta forma normal](/images/4ta-forma-normal.PNG)

[Las 12 (+1) Leyes de Codd](https://platzi.com/tutoriales/1566-bd/4120-las-12-1-leyes-de-codd/)

## Diagrama Físico: normalizando Platziblog

![Diagrama físico Platziblog](/images/diagrama-fisico-platziblog.PNG)

### ER Proyecto: Account Management

![Account](/images/er-account-management.PNG)

## Formas normales en DB relacionales

La normalización en las bases de datos relacionales es uno de esos temas que, por un lado es sumamente importante y por el otro suena algo esotérico. Vamos a tratar de entender las formas normales (FN) de una manera simple para que puedas aplicarlas en tus proyectos profesionales.

### Primera Forma Normal (1FN)
Esta FN nos ayuda a eliminar los valores repetidos y no atómicos dentro de una base de datos.

Formalmente, una tabla está en primera forma normal si:

* Todos los atributos son atómicos. Un atributo es atómico si los elementos del dominio son simples e indivisibles.
* No debe existir variación en el número de columnas.
* Los campos no clave deben identificarse por la clave (dependencia funcional).
* Debe existir una independencia del orden tanto de las filas como de las columnas; es decir, si los datos cambian de orden no deben cambiar sus significados.

Se traduce básicamente a que si tenemos campos compuestos como por ejemplo “nombre_completo” que en realidad contiene varios datos distintos, en este caso podría ser “nombre”, “apellido_paterno”, “apellido_materno”, etc.

También debemos asegurarnos que las columnas son las mismas para todos los registros, que no haya registros con columnas de más o de menos.

Todos los campos que no se consideran clave deben depender de manera única por el o los campos que si son clave.

Los campos deben ser tales que si reordenamos los registros o reordenamos las columnas, cada dato no pierda el significado.

![1FN](/images/1ra-forma-normal.PNG)

### Segunda Forma Normal (2FN)
Esta FN nos ayuda a diferenciar los datos en diversas entidades.

Formalmente, una tabla está en segunda forma normal si:

* Está en 1FN
* Sí los atributos que no forman parte de ninguna clave dependen de forma completa de la clave principal. Es decir, que no existen dependencias parciales.
* Todos los atributos que no son clave principal deben depender únicamente de la clave principal.

Lo anterior quiere decir que sí tenemos datos que pertenecen a diversas entidades, cada entidad debe tener un campo clave separado. Por ejemplo:

![1FN](/images/1ra-forma-normal.PNG)

En la tabla anterior tenemos por lo menos dos entidades que debemos separar para que cada uno dependa de manera única de su campo llave o ID. En este caso las entidades son alumnos por un lado y materias por el otro. En el ejemplo anterior, quedaría de la siguiente manera:

![2FN](/images/2da-forma-normal.PNG)

### Tercera Forma Normal (3FN)
Esta FN nos ayuda a separar conceptualmente las entidades que no son dependientes.

Formalmente, una tabla está en tercera forma normal si:

* Se encuentra en 2FN
* No existe ninguna dependencia funcional transitiva en los atributos que no son clave

Esta FN se traduce en que aquellos datos que no pertenecen a la entidad deben tener una independencia de las demás y debe tener un campo clave propio. Continuando con el ejemplo anterior, al aplicar la 3FN separamos la tabla alumnos ya que contiene datos de los cursos en ella quedando de la siguiente manera.

![3FN](/images/3ra-forma-normal.PNG)

Captura de Pantalla 2019-04-30 a la(s) 17.27.52.png

### Cuarta Forma Normal (4FN)
Esta FN nos trata de atomizar los datos multivaluados de manera que no tengamos datos repetidos entre rows.

Formalmente, una tabla está en cuarta forma normal si:

* Se encuentra en 3FN
* Los campos multivaluados se identifican por una clave única

Esta FN trata de eliminar registros duplicados en una entidad, es decir que cada registro tenga un contenido único y de necesitar repetir la data en los resultados se realiza a través de claves foráneas.

Aplicado al ejemplo anterior la tabla materia se independiza y se relaciona con el alumno a través de una tabla transitiva o pivote, de tal manera que si cambiamos el nombre de la materia solamente hay que cambiarla una vez y se propagara a cualquier referencia que haya de ella.

![4FN](/images/4ta-forma-normal.PNG)

De esta manera, aunque parezca que la información se multiplicó, en realidad la descompusimos o normalizamos de manera que a un sistema le sea fácil de reconocer y mantener la consistencia de los datos.

Algunos autores precisan una 5FN que hace referencia a que después de realizar esta normalización a través de uniones (JOIN) permita regresar a la data original de la cual partió.

# RDBMS (MySQL) o cómo hacer lo anterior de manera práctica

## RDB ¿Qué?

RDBMS significa Relational Database Management System o sistema manejador de bases de datos relacionales. Es un programa que se encarga de seguir las reglas de Codd y se puede utilizar de manera programática.

**RDB (relational database)**

La diferencia entre ambos es que las BBDD son un conjunto de datos pertenecientes ( o al menos en teoría) a un mismo tipo de contexto, que guarda los datos de forma persistente para un posterior uso, y el Sistema de gestión de BBDD o sistema manejador, es el que nos permite acceder a ella, es un software, herramienta que sirve de conexión entre las BBDD y el usuario (nos presenta una interfaz para poder gestionarla, manejarla).

**RDBMS**

* MySQL
* PostgreSQL
* Etc

Todas toman un lenguaje base, pero cada uno lo apropia, imponiéndole diferentes reglas y características.

## Clientes gráficos

En MySQL Workbench, abrimos la conexión establecida para la DB que queremos trabajar, en la parte de abajo del panel de la izquierda, clickeamos en Schemas y seguimos los siguientes pasos:
1. Clic derecho en el área blanca y creamos un Schema.
2. Le damos el nombre al schema y seleccionamos el Charset.
3. Clickeamos en `Apply`.
4. Nos aparecera el siguiente recuadro, lo que básicamente quiere decir es que utilizará SQL para crear la base de datos `platziblog` utilizando el charset `utf8`.
![Apply SQL](/images/apply-sql.png)
5. Clic en `Apply` y luego en `Finish`.

## Servicios administrados

Hoy en día muchas empresas ya no tienen instalados en sus servidores los RDBMS sino que los contratan a otras personas. Estos servicios administrados cloud te permiten concentrarte en la base de datos y no en su administración y actualización.

# SQL hasta en la sopa

## Historia de SQL

SQL significa *Structured Query Language* y tiene una estructura clara y fija. Su objetivo es hacer un solo lenguaje para consultar cualquier manejador de bases de datos volviéndose un gran estándar.

Ahora existe el NOSQL o *Not Only Structured Query Language* que significa que no sólo se utiliza SQLen las bases de datos no relacionales.

SQL es un lenguaje de acceso a bases de datos que explota la flexibilidad y potencia de los sistemas relacionales y permite así gran variedad de operaciones.

* SQL es un estándar aceptado por ANSI (Instituto Nacional Estadounidense de Estándares)
* PL/SQL es un lenguaje de programación de la base de datos de Oracle, el nombre viene de Procedural Language/Structured Query Language
* T-SQL es un lenguaje de programación de la base de datos de Microsoft SQL Server y el nombre viene de TRANSACT-SQL

## DDL create

SQL tiene dos grandes sublenguajes:
DDL o Data Definition Language que nos ayuda a crear la estructura de una base de datos. Existen 3 grandes comandos:

* **Create**: Nos ayuda a crear bases de datos, tablas, vistas, índices, etc.
* **Alter**: Ayuda a alterar o modificar entidades.
* **Drop**: Nos ayuda a borrar. Hay que tener cuidado al utilizarlo.

**3 objetos que manipularemos con el lenguaje DDL:**

* Database o bases de datos
* Table o tablas. Son la traducción a SQL de las entidades
* View o vistas: Se ofrece la proyección de los datos de la base de datos de forma entendible.

What is DDL, DML, DCL, and TCL?

![SQL Commands](/images/sql-commands.png)

### DDL

DDL is short name of Data Definition Language, which deals with database schemas and descriptions, of how the data should reside in the database.

* CREATE - to create a database and its objects like (table, index, views, store procedure, function, and triggers)
* ALTER - alters the structure of the existing database
* DROP - delete objects from the database
* TRUNCATE - remove all records from a table, including all spaces allocated for the records are removed
* COMMENT - add comments to the data dictionary
* RENAME - rename an object

### DML

DML is short name of Data Manipulation Language which deals with data manipulation and includes most common SQL statements such SELECT, INSERT, UPDATE, DELETE, etc., and it is used to store, modify, retrieve, delete and update data in a database.

* SELECT - retrieve data from a database
* INSERT - insert data into a table
* UPDATE - updates existing data within a table
* DELETE - Delete all records from a database table
* MERGE - UPSERT operation (insert or update)
* CALL - call a PL/SQL or Java subprogram
* EXPLAIN PLAN - interpretation of the data access path
* LOCK TABLE - concurrency Control

### DCL

DCL is short name of Data Control Language which includes commands such as GRANT and mostly concerned with rights, permissions and other controls of the database system.

* GRANT - allow users access privileges to the database
* REVOKE - withdraw users access privileges given by using the GRANT command

### TCL

TCL is short name of Transaction Control Language which deals with a transaction within a database.

* COMMIT - commits a Transaction
* ROLLBACK - rollback a transaction in case of any error occurs
* SAVEPOINT - to rollback the transaction making points within groups
* SET TRANSACTION - specify characteristics of the transaction

[Data definition language](https://en.wikipedia.org/wiki/Data_definition_language)

### Crear una Database

Crear una base de datos es relativamente sencillo, simplemente usamos: 

```sql
CREATE DATABASE test_db;
USE test_db;
```

### Crear una Tabla
```sql
CREATE TABLE people (
person_id int,
last_name varchar(255),
first_name varchar(255),
address varchar(255),
city varchar(255)
);
```
Las tablas son un poco más complicadas de crear, puesto que tiene campos que pueden ser de diferentes tipos y también pueden tener constraints, o llaves primarias o secundarias.

Con Workbench, es muy fácil crear tablas de forma visual y el impacto que reflejaría en la DB es muy fuerte porque no se crearían tablas con comandos.

![Creando tabla people con workbench](/images/manejador-visual-tabla.PNG)

Cuando le demos clic en Apply, nos aparecerá una ventana con el código SQL con el que creará la tabla, ahora, si estamos de acuerdo le damos clic en Apply y la tabla se creará.

```sql
CREATE TABLE `platziblog`.`people` (
  `person_id` INT NOT NULL AUTO_INCREMENT,
  `last_name` VARCHAR(255) NULL,
  `first_name` VARCHAR(255) NULL,
  `address` VARCHAR(255) NULL,
  `city` VARCHAR(255) NULL,
  PRIMARY KEY (`person_id`));
```
Se añadieron visualmente los siguientes resultados:

![Tabla People](/images/tabla-people.PNG)

## CREATE VIEW y DDL ALTER

Las vista se usan como una capa de seguridad dentro de las organizaciones. por ejemplo: una tabla trabajador tiene todos los datos de una persona (numero de identificación, numero telefonico, dirección, y otros datos que pueden ser sensibles), el administrador de la base de datos lo que hace es crear vistas solo con los datos que son relevantes para consultas en las distintas areas de la empresas sin exponer información de mas.
```sql
CREATE VIEW v_brasil_customers AS
SELECT customer_name,
contact_name
FROM customers
WHERE country = "Brasil";
```

La vista creada para el proyecto fue la siguiente:

```sql
CREATE VIEW platzi_people_barrancabermeja AS
SELECT * FROM platziblog.people
WHERE city = "Barrancabermeja";
```

Esto crea una vista, entonces, al desplegar el dropdown menu de las vistas y darle clic derecho y luego clic a `Select Rows - Limit 1000` devolvió los siguientes resultados:

![Vista people Barrancabermeja](/images/vista-people-barrancabermeja.PNG)

### Alter Table

```sql
ALTER TABLE people
ADD date_of_birth date;

ALTER TABLE people
ALTER COLUMN date_of_birth year;

ALTER TABLE people
DROP COLUMN date_of_birth;
```
Alter nos permite modificar nuestra tabla. Se puede ejecutar desde la línea de comandos o desde el manejador gráfico que nos proveé MySQL Workbench, simplemente le damos clic derecho a la tabla que queremos modificar, luego le damos clic a `Alter Table...` y con esto podemos modificarla gráficamente.

**Añadimos la columna `date_of_birth`:**

```sql
ALTER TABLE `platziblog`.`people` 
ADD COLUMN `date_of_birth` DATETIME NULL AFTER `city`;
```

**Modificamos la columna `date_of_birth`:**
```sql
ALTER TABLE `platziblog`.`people` 
CHANGE COLUMN `date_of_birth` `date_of_birth` YEAR(4) NULL DEFAULT NULL ;
```

**Borramos la columna `date_of_birth`:**
```sql
ALTER TABLE `platziblog`.`people` 
DROP COLUMN `date_of_birth`;
```

## DDL drop

`Drop` es la secuencia más peligrosa cuando no se tiene experiencia o conocimientos manejando bases de datos, pues si no se declara específicamente que es lo que se desea borrar, puede o borrar una tabla o una base de datos completamente.

```sql
DROP TABLE people;

DROP DATABASE test_db;
```
En el manejador visual de Workbench, simplemente le damos clic derecho a la tabla que queremos borrar, y luego a la opción `Drop Table...`, confirmamos si queremos borrar la tabla, existen tres opciones, Borrar Ahora, cancelar o Revisar código. Por buenas prácticas lo mejor siempre es revisar antes de ejecutar el código.

![Drop table](/images/drop-table.PNG)

La más peligrosa es `DROP SCHEMA` o `DROP DATABASE`, puesto que esta borraría toda la base de datos. En el editor visual siempre va a haber una confirmación puesto que es una sentencia peligrosa, en la consola puede que no pida confirmación sino que se ejecute inmediatamente.

![Drop schema](/images/drop-schema.PNG)

## DML

Data Manipulation Language - Lenguaje de Manipulación de Datos. Lidia con la manipulación de datos e incluye las sentencias SQL más comunes como SELECT, INSERT, UPDATE, DELETE, etc., y es usada para almacenar, modificar, seleccionar, borrar y actualizar datos en una base de datos.

* SELECT - selecciona o recupera los datos de una base de datos.
```sql
SELECT fist_name, last_name
FROM people;
```
* INSERT - inserta datos en una DB
```sql
INSERT INTO people (last_name,
first_name, address, city)
VALUES ('Hernández', 'Laura',
'Calle 21', 'Monterrey');
```
* UPDATE - actualiza datos en una DB existente
```sql
UPDATE people
SET last_name = 'Chávez', city= 'Mérida'
WHERE person_id = 1;

UPDATE people
SET first_name = 'Juan'
WHERE city = 'Mérida';

UPDATE people
SET first_name = 'Juan';
```
* DELETE - borra todos los registros de una DB
```sql
DELETE FROM people
WHERE person_id = 1;

DELETE FROM people;
```
* MERGE - UPSERT esta operación inserta o actualiza datos
* CALL - llama a un PL/SQL o un subprograma de Java
* EXPLAIN PLAN - interpreta la ruta de acceso de los datos
* LOCK TABLE - Control de concurrencia

## ¿Qué tan standard es SQL?

La utilidad más grande de SQL fue unificar la forma en la que pensamos y hacemos preguntas a un repositorio de datos. Ahora que nacen nuevas bases de datos igualmente siguen tomando elementos de SQL.

* SQL unifico la manera en que sea hacen preguntas a un repositorio de datos.
* Se convirtio en un standard util a la hora de usar bases de datos.
* Existen otros manejadores de datos como Oracle o PostgreSQL.
* Sin embargo, si escribimos en lenguaje SQL todos los manejadores funcionaran de manera similar.

>Ejemplo de la clase.
```sql
Estructura básica de un Query
SELECT city, count(*) AS total
FROM people
WHERE active = true
GROUP BY city
ORDER BY total DESC
HAVING total >= 2;
```

>Tabla creada en clase.
El instructor utilizó este mismo código para una DB en postgresql en la nube para demostrar que las mismas sentencias que se utilizan en MySQL pueden ser utilizadas en otros manejadores de tipo relacional.
```sql
CREATE TABLE people(
person_id int,
last_name varchar(255),
first_name varchar(255),
address varchar(255),
city varchar(255)
);

INSERT INTO people (last_name, first_name, address, city)
VALUES('Palomino Cardenas', 'Oscar Eduardo', 'Calle Increible', 'Barrancabermeja');

DROP TABLE people;
```

## Creando Platziblog: tablas independientes

* Una buena práctica es comenzar creando las entidades que no tienen una llave foránea.
* Generalmente en los nombres de bases de datos se evita usar eñes o acentos para evitar problemas en los manejadores de las bases de datos.

![Diagrama Físico Platziblog](/images/diagrama-fisico-platziblog.PNG)

## Creando Platziblog: tablas dependientes

El comando *“cascade”* sirve para que cada que se haga un update en la tabla principal, se refleje también en la tabla en la que estamos creando la relación.

**Las Foreing Key options son las siguientes:**

* On update: Significa qué pasará con las relaciones cuando una de estas sea modificada en sus campos relacionados, Por ejemplo, pueden utilizarse los valores:
    * Cascade: Si el id de un usuario pasa de 11 a 12, entonces la relacion se actualizará y el post buscará el id nuevo en lugar de quedarse sin usuario.
    * Restrict: Si el id de un usuario pasa de 11 a 12, no lo permitirá hasta que no sean actualizados antes todos los post relacionados.
    * set null Si el id de un usuario pasa de 11 a 12, entonces los post solo no estará relacionados con nada.
    * No action: Si el id de un usuario pasa de 11 a 12, no se hará nada. Solo se romperá la relación.
* On delete
    * Cascade: Si un usuario es eliminado entonces se borrarán todos los post relacionados.
    * Eestrict: No se podrá eliminar un usuario hasta que sean eliminados todos su post relacionados.
    * Set null: Si un usuario es eliminado, entonces los post solo no estará relacionados con nada.
    * No action: Si un usuario es eliminado, no se hará nada. Solo se romperá la relación.

En esta clase, primero se define el nombre de las columnas, incluyendo a las que serán las llaves foráneas.

![Columnas](/images/columnas-posts.PNG)

Creamos la tabla para poder trabajar en ella, se le da clic en apply y luego, nos vamos a la pestaña `Foreign keys` y seleccionamos las llaves foráneas.

Las referenciamos y seleccionamos las opciones respecto a las llaves foráneas.

![Foránea user](/images/referencia-userid.PNG)

![Foránea category](/images/referencia-categoryid.PNG)

Este es el código que se generó al darle Apply.

```sql
ALTER TABLE `platziblog`.`posts` 
ADD INDEX `post_users_idx` (`user_id` ASC) VISIBLE,
ADD INDEX `post_categories_idx` (`category_id` ASC) VISIBLE;
;
ALTER TABLE `platziblog`.`posts` 
ADD CONSTRAINT `post_users`
  FOREIGN KEY (`user_id`)
  REFERENCES `platziblog`.`users` (`id`)
  ON DELETE NO ACTION
  ON UPDATE CASCADE,
ADD CONSTRAINT `post_categories`
  FOREIGN KEY (`category_id`)
  REFERENCES `platziblog`.`categories` (`id`)
  ON DELETE NO ACTION
  ON UPDATE CASCADE;
```

Y así es como se visualiza la tabla en el manejador visual después de hacer estos cambios.

![Post columns](/images/posts-columns.PNG)

## Creando Platziblog: tablas transitivas

* Las tablas transitivas sirven como puente para unir dos tablas. No tienen contenido semántico.
* Reverse Engineer nos reproduce el esquema del cual nos basamos para crear nuestras tablas. Es útil cuando llegas a un nuevo trabajo y quieres entender cuál fue la mentalidad que tuvieron al momento de crear las bases de datos.

Creamos la tabla comments con la siguiente estructura:

![Post](/images/comments-columns.PNG)

Referenciamos las llaves foráneas y posteriormente, creamos una tabla transitiva, se llama así porque sirve como pivote para unir 2 tablas, pero semánticamente no tiene sentido, no tiene información propia pero sirve para ligar.

![Transitiva](/images/tabla-transitiva.PNG)

# Consultas a una base de datos

## ¿Por qué las consultas son tan importantes?

Las consultas o queries a una base de datos son una parte fundamental ya que esto podría salvar un negocio o empresa.

Alrededor de las consultas a las bases de datos se han creado varias especialidades como ETL o transformación de datos, business intelligence e incluso machine learning.

## Estructura básica de un Query

```sql
SELECT city, count(*) AS total
FROM people
WHERE active = true
GROUP BY city
ORDER BY total DESC
HAVING total >= 2;
```
Sentencias SQL utilizadas en esta clase.
```sql
SELECT	* 
FROM	posts
WHERE YEAR(fecha_publicacion) > 2024;

SELECT	* 
FROM	posts
WHERE YEAR(fecha_publicacion) < 2024;
```

## SELECT

SELECT se encarga de proyectar o mostrar datos.

* El nombre de las columnas o campos que estamos consultando puede ser cambiado utilizando AS después del nombr* del campo y poniendo el nuevo que queremos tener:
```sql
SELECT titulo AS encabezado
FROM posts;
```
* Existe una función de SELECT para poder contar la cantidad de registros. Esa información (un número) será el resultado del query:
```sql
SELECT COUNT(*)
FROM posts;
```

## FROM

FROM indica de dónde se deben traer los datos y puede ayudar a hacer sentencias y filtros complejos cuando se quieren unir tablas. La sentencia compañera que nos ayuda con este proceso es JOIN.

Los diagramas de Venn son círculos que se tocan en algún punto para ver dónde está la intersección de conjuntos. Ayudan mucho para poder formular la sentencia JOIN de la manera adecuada dependiendo del query que se quiere hacer.

![Join](/images/sqljoin.jpeg)

## Utilizando la sentencia FROM

La siguiente sentencia, trae a todos los usuarios de la DB y une su información con la información de los posts, es decir, que en la DB veremos todos los posts con el usuario que lo creo.
```SQL
SELECT *
FROM	usuarios
LEFT JOIN posts
ON usuarios.id = posts.usuario_id;
```

La siguiente sentencia, trae a todos los usuarios que NO tienen posts.
```sql
SELECT *
FROM	usuarios
LEFT JOIN posts
ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NULL;
```

La siguiente sentencia trae a todos los usuarios que SI tienen posts.
```sql
SELECT *
FROM	usuarios
LEFT JOIN posts
ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NOT NULL;
```

La siguiente sentencia trae a todos los posts, incluído a los que no tienen usuario asociado.
```sql
SELECT *
FROM	usuarios
RIGHT JOIN posts
ON usuarios.id = posts.usuario_id;
```

La siguiente sentencia trae a todos los post que NO poseen usuario asociado.
```sql
SELECT *
FROM	usuarios
RIGHT JOIN posts
ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NULL;
```

La siguiente sentencia trae a todos los post que SI poseen usuario asociado.
```sql
SELECT *
FROM	usuarios
RIGHT JOIN posts
ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NOT NULL;
```

La siguiente sentencia, trae a todos los datos que tengan el usuario id relacionado en el atributo `ON`. Es decir, que estén relacionados por ambos lados.
```sql
SELECT *
FROM	usuarios
INNER JOIN posts
ON usuarios.id = posts.usuario_id;
```

La siguiente sentencia no es completamente estandar en SQL, y es la UNIÓN de las 2 tablas utilizando el atributo `FULL OUTER JOIN`.
```sql
SELECT *
FROM	usuarios
FULL OUTER JOIN posts
ON usuarios.id = posts.usuario_id;
```

La forma de hacer esto en SQL es haciendo una unión compuesta de ambas tablas. Esto trae al universo de las tablas, la totalidad de la información.
```sql
SELECT *
FROM	usuarios
	LEFT JOIN posts ON usuarios.id = posts.usuario_id
UNION
SELECT *
FROM	usuarios
	RIGHT JOIN posts ON usuarios.id = posts.usuario_id;
```

La siguiente sentencia trae al universo de los datos, exceptuando la información que comparten. Es decir, los usuarios que NO tienen posts, y los posts que NO tienen usuario asignado.
```sql
SELECT *
FROM	usuarios
	LEFT JOIN posts ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NULL
UNION
SELECT *
FROM	usuarios
	RIGHT JOIN posts ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NULL;
```

La siguiente sentencia trae al universo de los datos, exceptuando la información que comparten. Es decir, los usuarios que SI tienen posts, y los posts que SI tienen usuario asignado. Es otra forma de hacer un INNER JOIN más elaborado.
```sql
SELECT *
FROM	usuarios
	LEFT JOIN posts ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NOT NULL
UNION
SELECT *
FROM	usuarios
	RIGHT JOIN posts ON usuarios.id = posts.usuario_id
WHERE posts.usuario_id IS NOT NULL;
```

## WHERE

WHERE es la sentencia que nos ayuda a filtrar tuplas o registros dependiendo de las características que elegimos.

* La propiedad **LIKE** nos ayuda a traer registros de los cuales conocemos sólo una parte de la información.
* La propiedad **BETWEEN** nos sirve para arrojar registros que estén en el medio de dos. Por ejemplo los registros con id entre 20 y 30.

La siguiente sentencia nos trae todos los posts con el id menor a 50.
```sql
SELECT *
FROM posts
WHERE id < 50;
```

La siguiente sentencia nos trae todos los posts con el id mayor igual a 50.
```sql
SELECT *
FROM posts
WHERE id >= 50;
```

La siguiente sentencia nos trae todos los posts con el estado es activo.
```sql
SELECT *
FROM posts
WHERE estatus = 'activo';
```

La siguiente sentencia nos trae todos los posts con el estado es inactivo.
```sql
SELECT *
FROM posts
WHERE estatus = 'inactivo';

SELECT *
FROM posts
WHERE estatus != 'activo';
```

### Propiedad LIKE

Esta propiedad se utiliza con cadenas de texto, específicamente cuando no se tiene conocimiento del contenido exacto, entonces, se puede filtrar por una fracción del contenido.

```sql
SELECT *
FROM posts
WHERE titulo LIKE '%escandalo%';
```

Los signos de porcentaje indican la posibilidad de que hayan caracteres tanto antes como después de la palabra que queremos buscar. Si no tuviera el porcentaje de la izquierda, buscaría todos los títulos que empiecen con `escandalo`, si no tuviera el porcentaje de la derecha, buscaría todos los títulos que terminen con `escandalo`.

### Propiedad BETWEEN

Esta propiedad se utiliza con valores numéricos y con fechas.

```sql
SELECT *
FROM posts
WHERE fecha_publicacion BETWEEN '2023-01-01' AND '2025-12-31';

SELECT *
FROM posts
WHERE id BETWEEN 50 AND 60;
```

## Utilizando la sentencia WHERE nulo y no nulo

El valor nulo en una tabla generalmente es su valor por defecto cuando nadie le asignó algo diferente. La sintaxis para hacer búsquedas de datos nulos es `IS NULL`. La sintaxis para buscar datos que no son nulos es `IS NOT NULL`.

## GROUP BY

GROUP BY tiene que ver con agrupación. Indica a la base de datos qué criterios debe tener en cuenta para agrupar.

Aparte de la función COUNT, podemos encontrar las siguientes funciones de agregado:
* **AVG** Calcula el promedio
* **COUNT** Cuenta los registros de un campo
* **SUM** Suma los valores de un campo
* **MAX** Devuelve el maximo de un campo
* **MIN** Devuelve el mínimo de un campo

GROUP BY nos permite hacer consultas mucho mas organizadas, de manera que la consulta se ejecuta dividida por los diferentes valores que posee la columna, de esta manera podemos determinar no solo el número de valores diferentes que puede tener un atributo, sino muchos otros parámetros como la cantidad de los mismos (con COUNT(*)).

La siguiente sentencia agrupa el total de los posts por el nickname de los usuarios.
```sql
SELECT COUNT(*) AS total_posts, u.nickname
FROM posts as p
INNER JOIN usuarios AS u
ON u.id = p.usuario_id
GROUP BY u.nickname;
```
![Total posts](/images/group-by-totalposts.PNG)

La siguiente sentencia agrupa el total de los posts por su estado.
```sql
SELECT COUNT(*) AS total_posts, estatus
FROM posts
GROUP BY estatus;
```
![Posts por estatus](/images/group-by-estatus.PNG)

La siguiente sentencia agrupa el total de los posts por año, y lo ordena de forma ascendente por el año.
```sql
SELECT YEAR(fecha_publicacion) AS year_pub, COUNT(*) AS total_posts
FROM posts
GROUP BY year_pub
ORDER BY year_pub ASC;
```
![Total posts year](/images/group-by-year.PNG)

La siguiente sentencia agrupa el total de los posts por mes, sin tener en cuenta el año.
```sql
SELECT MONTHNAME(fecha_publicacion) AS month_pub, COUNT(*) AS total_posts
FROM posts
GROUP BY month_pub;
```
![Total posts by month](/images/group-by-month.PNG)

La siguiente sentencia agrupa el total de los posts por mes y año y lo ordena de manera ascendente por el año.
```sql
SELECT MONTHNAME(fecha_publicacion) AS post_month, YEAR(fecha_publicacion) AS post_year, COUNT(*) AS total_posts
FROM posts
GROUP BY post_year, post_month
ORDER BY post_year;
```
![Total post by month and year](/images/group-by-year-month.PNG)

La siguiente sentencia agrupa el total de los posts por año, usuario y estado y lo ordena de manera ascendente.
```sql
SELECT YEAR(fecha_publicacion) AS post_year, usuarios.nickname, estatus, COUNT(*) AS total_posts
FROM posts
LEFT JOIN usuarios
ON posts.usuario_id = usuarios.id
GROUP BY post_year, estatus
ORDER BY post_year ASC;
```
![total post by year, user and status](/images/group-by-year-user-status.PNG)

## ORDER BY y HAVING

La sentencia **ORDER BY** tiene que ver con el ordenamiento de los datos dependiendo de los criterios que quieras usar.

* **ASC** sirve para ordenar de forma ascendente.
* **DESC** sirve para ordenar de forma descendente.
* **LIMIT** se usa para limitar la cantidad de resultados que arroja el query.

**HAVING** tiene una similitud muy grande con **WHERE**, sin embargo el uso de ellos depende del orden. Cuando se quiere seleccionar tuplas agrupadas únicamente se puede hacer con **HAVING**.

## El interminable agujero de conejo (Nested queries)

Los Nested queries significan que dentro de un query podemos hacer otro query. Esto sirve para hacer join de tablas, estando una en memoria. También teniendo un query como condicional del otro.

Este proceso puede ser tan profundo como quieras, teniendo infinitos queries anidados.
Se le conoce como un producto cartesiano ya que se multiplican todos los registros de una tabla con todos los del nuevo query. Esto provoca que el query sea difícil de procesar por lo pesado que puede resultar.

* Las consultas anidadas son la mejor opción cuando los valores dependen de otras tablas, y estas no se encuentran relacionadas entre si.
* Las consultas anidadas son la mejor opción para casos de INSERT, DELETE, UPDATE, cuya condición dependa del esenario explicado en el punto anterior
* Los JOINS son la mejor opción para casos de SELECT
