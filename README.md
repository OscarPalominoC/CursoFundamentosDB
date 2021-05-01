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

