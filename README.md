# api_request
Desarrollo desafío fio API Request
<h2>Descripción:</h2>
En el siguiente repositorio se encuentra el desarrollo del desafio de la API_Request del curso de spring de alura_cursos.
<h2>Recomendaciones:</h2>
A pesar de adjuntar el archivo de la base de datos, se recomienda cambiar las condiciones del código para que se ejecute correctamente según el administrador de base de datos de su preferencia, para ello debe cambiar el archivo "application.properties" de la siguiente forma:

spring.application.name=api
spring.datasource.url=jdbc:mysql://localhost:3306/Nombre_de_la_base_de_datos
spring.datasource.username=usuario_de_la_base_de_datos
spring.datasource.password=contraseña_de_la_base_de_datos

También se recomienda crear la base de datos con las siguientes características:

CREATE DATABASE Nombre_de_la_base_de_datos;
use Nombre_de_la_base_de_datos;
create table topicos(

    id bigint not null auto_increment,
    mensaje varchar(500) not null,
    nombre_curso varchar(200) not null,
    titulo varchar(300) not null,
	activo tinyint,
     
    primary key(id)
);
update topicos set activo = 1;
create table usuarios(

    id bigint not null auto_increment,
    login varchar(100) not null,
    clave varchar(400) not null,

    primary key(id)
);

INSERT INTO usuarios (login, clave)
VALUES ("master", "$2a$12$D2iw6kpv3tZxRb265YJYHOqLoLprxFOZBlxj7IyRlqXLi3F.TrubK");

Al correr estos comandos en el orden especificado, el programa correrá correctamente.

<h2>Oportunidades de mejora:</h2>
Si bien es cierto que el código tiene la posibilidad de realizar la creación de la base y sus tablas con ayuda de las migraciones, por la inexperiencia frente al uso de estas, se decidió hacerlo manualmente con ayuda del gestor de bases de datos.

Se lograron observar problemas de compilación en el código despúes de que se usaba un token por un tiempo prolongado, para "solventarlo" se tuvo que borrar la base de datos y crearla nuevamente, con ello se restauraba el programa pero a cambio se perdia la información.

Por último si tiene la oportunidad de corregirme, no dude en comunicarse conmigo, estare atento.
