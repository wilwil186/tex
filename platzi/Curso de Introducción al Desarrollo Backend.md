# Te doy la bienvenida al desarrollo backend

el mundo esta lleno de aplicaciones web. ellas nacen en la web.

# Yin y Yang de una aplicación: frontend y backend

la corroceria es el acara visible del auto, y otro componente impotarte
es el motor. ahora piensa en aplicaciones. igual que los carros tienen
lo mismos componente \"relativamente\". en tecnologia la correceria: es
el frontend y el motor es el backend. python es un lenguaje para
onstruir backend. las tecnologias principales del frontend son:

1.  html

2.  css

3.  JavaScript

esos son los basicos. css estilos. JS interacción. html una estrcutura.
cada lenguaje tiene sus derivados piensa como si fuera codigo estrito
por demas personas. en backend se pueden utilizar lenguajes de
progamación como:

1.  JavaScript

2.  php

3.  Java

4.  Go

5.  Rust

6.  Ruby

7.  python

y seguramente hay muchos mas. y cada uno de estos lenguajes tienen sus
derivados.

# Framework vs. librería

¿como se construye un auto? comenzamos por el motor, tenemos que empezar
por un lado. seguramente hay una guia para hacer el motor, a esto en
progamación se le llama libreria. las reglas para contruiir el motor, se
le llama Framework, en español un marco de trabajo. el Framework
usualmente es un conjunto de librerias de paosos y recetas para contruir
un motor.

# Cómo se conecta el frontend con el backend: API y JSON

API Y JASON. una API es solo una sección de motor que permite que el
frontend se comunique con el backend. dos grandes estadares son **SOAP**
o simple obeject access protocol, y **REST** o representational state
transfer. este primer estandar mueve la informacion con **XML**
extensible markup languague parecido a html. soap a quedado un poco en
el olvido :'(. por culpa de JASON por ser superior. un JASON es como un
diccionario de python. los diccionario en python son iguales a los
objetos en JS.

# El lenguaje que habla Internet: HTTP

<https://developer.mozilla.org/es/docs/Web/HTTP/Status>

**cliente**: dispositivos. **servidor**: una computadora del dia
encendida 24/7 protocolo de tranferencia de hipertexto. el cliente hace
la peticion en idioma HTTP. 200 es ok. dentro del rango de los 400 es
que algun recurso no es encontrado. si esta en el ranfo de los 500 hay
un error en el codigo. **tarea investicar los estatus code**

# ¿Cómo es el flujo de desarrollo de una aplicación web?

el lugar en el que comienzas a trabajar es tu editor de texto. git
sistema de control de versiones. browser (navegador). en el servidor se
coloca una aplicación para que este disponible para todos. esto se
denomida deploy(pasar de el entorno de trabajo a un resposorio).
normalmente se hace un push a github antes. desde github se hace
**CI/CD**. este porceso lo que hace es testarlo. y si todo esta ok se
envia a el servidor. el servidor guarda el codigo es un servidor.
normalmente son de paga pero se pueden conseguir algunas de manera
gratuita. la nube es una forma popular de llamar a muchos servidores.

# El hogar de tu código: el servidor

los servidores estan en datacenters.al hecho de guardar una aplicacion
en un servidor se le denomina hosting. hay distintos tipos de hosting.
entendamos 3 conceptos

1.  iass (infrastutura como servivio). es una opción cuando quiereas
    tener control como la cpu la ram y la ssd, esta

    1.  Aws (amazon web services)

    2.  microsoft azure

    3.  digital ocean (economico)

    vas a encontrar dos tipos de iass en internet

    1.  VPS(virtual private server). para rendimiento superior.

    2.  shared hosting. alojamiento compartido. es mas barato.

2.  pass (plataforma como servicio).se encarga de actualizar, tu rela.
    just deploy. opciones:

    1.  google aee engine. servicio de google cload

    2.  firebase. un poco mas complejas.

    3.  heroku.

3.  sass (software como servico). no reinventar la rueda. no code. es
    una aplicacion que un provedor te presta para que puedas hacer
    funcionar tu servicio.

    1.  google docs.

    2.  slack.

    3.  wordpress.

hay que elegir una de ellas cuando se publica tu aplicacion

# Proyecto: diseño y bosquejo de una API

cosas fundamentales twitter, por ejemplo un twit, si fuéramos a crear un
clon de twiter, tengo que ser capaz de crear usuarios de publicar twits
de actualizar usuarios y actualizar twits, de borrar un usuario y de
borrar un twits ademas ver a usuarios y ver twits **API** aplicacion,
program, interface. una api se construye de varias maneras por ejemplo
en python

1.  fastapi

2.  Django

3.  flask

**endpoint/route/path** es simplemente una section de la url de tu
Proyecto. normalmente seria http://twiteer.com/api/\... lo que esta
despues de dominio seria el endpoint

# Proyecto: diseñando los endpoints de los Tweets

los endpoints de los Tweets. las reglas que nos proporcionan **CRUD**
create Read Update Delete. los endpoints para los Tweets serian:

1.  /Tweets -\> show all Tweets

2.  /post -\> publish a Tweet

3.  /Tweets / Tweet.id -\> show a tweet

4.  /Tweets/Tweet.id/update -\> update a Tweets

5.  /Tweets/tweet.id/delete -\> delete a tweet

# proyecto: diseñando los endpoints para los usuarios

hay dos modelos:

1.  Tweets

2.  users

a los modelos se los conoce como tablas en sql. cada uno de estos
modelos contiene registros. los enpoints para los usuarios serian

1.  /users -\> show all users

2.  /signup -\> registrer a user.

3.  / users/user.id -\> show a user.

4.  /user/user.id/update -\> update a user.

5.  /user/user.id/delete -\> delete a user.

cada vez que entremos a un endpoint el servidor nos responde con un
archivo de JASON es proplabe de lusca de la sigueinete manera:\

::: center
\"user.id\": 121\
\"username\" : facmartoni\
\"email\" x@x.com\
:::

lectura recomendada:
<https://elbauldelprogramador.com/buenas-practicas-para-el-diseno-de-una-api-restful-pragmatica/>

# Qué lenguaje y framework escoger para backend

python tiene 3 framework:

1.  Django. es el mas robusto y mas grande, tienes un panel de
    administración bastante completo. si vas a trabajar con muchos
    datos. comunidad enorme.

2.  flask. aplicaciones simples, muy flexive. algo personalizable.

3.  fast api. mucho mas rapida.

JavaScript:

1.  express. simple.

2.  nest. complejidad mayor.

php:

1.  laravel.es el mas facil.

2.  sympony. mas dificil. mas escaleble mas compleja.

java:

1.  spring.

Go:

1.  gin. por excelencia mas popular.

2.  beego. crecimiento.

ruby:

1.  rails
