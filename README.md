<h1>api_requestapi_request</h1>
Desarrollo desafío fio API Request

[TOCM]

#Descripción:
En el siguiente repositorio se encuentra el desarrollo del desafio de la API_Request del curso de spring de alura_cursos.
#Recomendaciones:
A pesar de adjuntar el archivo de la base de datos, se recomienda cambiar las condiciones del código para que se ejecute correctamente según el administrador de base de datos de su preferencia, para ello debe cambiar el archivo "application.properties" de la siguiente forma:

```html
spring.application.name=api
spring.datasource.url=jdbc:mysql://localhost:3306/Nombre_de_la_base_de_datos
spring.datasource.username=usuario_de_la_base_de_datos
spring.datasource.password=contraseña_de_la_base_de_datos
```

También se recomienda creár la base de datos de la siguiente forma:

1.Crear base de datos:
```
CREATE DATABASE Nombre_de_la_base_de_datos;
```
2.En algunos gestores de bases de datos solicita que se indique con código que base de datos usar, para el caso de mysql el comando es el siguiente:
```
use Nombre_de_la_base_de_datos;
```
3.Crear tabla para los topicos:
```
create table topicos(
    id bigint not null auto_increment,
    mensaje varchar(500) not null,
    nombre_curso varchar(200) not null,
    titulo varchar(300) not null,
	activo tinyint,	
    primary key(id));
```
4.insertar el estado (1) en la columna activo para indicar que los registros no han sido eliminados logicamente:
```
update topicos set activo = 1;
```
5.Crear tabla de usuarios:
```
create table usuarios(
	id bigint not null auto_increment,
    login varchar(100) not null,
    clave varchar(400) not null,

    primary key(id));
```
6.Insertar en la tabla el nombre del usuario y su contraseña:
```
INSERT INTO usuarios (login, clave)
VALUES ("master", "$2a$12$D2iw6kpv3tZxRb265YJYHOqLoLprxFOZBlxj7IyRlqXLi3F.TrubK");
```
cabe resaltar que la contraseña esta generada con el siguiente encriptador Hash.

`<link>` : <https://bcrypt-generator.com/#google_vignette>

Al correr estos comandos en el orden especificado, el programa correrá correctamente.

#Usos:
##Consultas Insomnia
###Login:
Al usar la siguiente **URL ** junto con el metodo **POST** se pordrá loguear el usuario.
```
http://localhost:8080/login
```
La siguiente sintaxis, es la forma adecuada para registrar el usuario y así poder obtener el **token** para poder realizar las demás request. Cabe resaltar que la contraseña usada para el login no esta decodificada como en la tabla **usuarios** de la base de datos, más sin embargo ambas deben coincidir al hacer la decodificación.  
```
{
	"login" : "master",
	"clave" : "123456"
}
```

####¡¡¡IMPORTANTE!!!
Para las siguientes request es importante tener el **token** generado o de lo contrario arrojara un error **403**, así como tambien agregar en cada metodo el tipo de autorización **Bearer Token** y copiar en el espacio del **TOKEN** el texto generado al momento de logearse.

###Registrar:
Al usar la siguiente **URL ** junto con el metodo **POST** se pordrá registrar el topico.
```
http://localhost:8080/topicos
```
Junto con la siguiente sintaxis (Es **IMPORTANTE** que se registren todos los campos, de lo contrario arrojara un error **403**):
```
{
	"mensaje" : "Hola",
	"nombreCurso" : "saludos",
	"titulo" : "saludo general"
}
```

###Listar:
Al usar la siguiente **URL ** junto con el metodo **GET** se pordrá obtener un listado con los topicos registrados.
```
http://localhost:8080/topicos
```

###Actualizar:
Al usar la siguiente **URL ** junto con el metodo **PUT** se pordrá obtener un listado con los topicos registrados.
```
http://localhost:8080/topicos
```

###Borar:
Al usar la siguiente **URL ** junto con el id del topico y el metodo  **DELETE** se pordrá obtener un listado con los topicos registrados.
```
http://localhost:8080/topicos/id_del_topico_a_borrar
```
Cabe resaltar que solo se hará un borrado **logico**, por lo tanto los topicos registrados aún serán visibles en la base de datos con el diferencial que su estado activo será (0), pero no se podrán observar al moemnto de listarlos.
![image](https://github.com/Sergio-Arevalo/api_request/assets/157325483/d8ce6d63-7bca-4432-bcaf-ad5f77c693e5)


#Oportunidades de mejora:
* Si bien es cierto que el código tiene la posibilidad de realizar la creación de la base y sus tablas con ayuda de las migraciones, por la inexperiencia frente al uso de estas, se decidió hacerlo manualmente con ayuda del gestor de bases de datos.

* Se lograron observar problemas de compilación en el código despúes de que se usaba un token por un tiempo prolongado, para "solventarlo" se tuvo que borrar la base de datos y crearla nuevamente, con ello se restauraba el programa pero a cambio se perdia la información.

* Por último si tiene la oportunidad de corregirme, no dude en comunicarse conmigo, estare atento.
