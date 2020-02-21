# Despleguando_aplicacion_Spring_Boot_en_Heroku
Repositorio sobre como desplegar en heroku una aplicación de spring boot en este caso un api rest de Autenticación Basica

Repositorio sobre sobre como desplegar en heroku una aplicación de spring boot en este caso un api rest de Autenticación Basica

Referencia usada para el repositorio => [Ver](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku)

Guia para la asignuatura:
* Sistemas de Gestión Empresarial

Proyecto para despleguar una app Spring Boot en Heroku

***


## Despleguar nuestra app en Heroku
Deberemos tener Heroku funcional en nuestro ordenador junto a una cuenta y sus credenciales para poder hacer el despliegue [Documentación](https://devcenter.heroku.com/)

Una vez este nuestra aplicación de Spring Boot que usa una base de datos postgresql en el repositorio (Debera estar la aplicación en la raíz del repositorio) crearemos nuestra aplicación de Heroku con el comando

```
heroku create
```

Una vez creada la aplicación de Heroku vamos a añadirle una base de datos, en este caso de postgresql para ello debemos ejecutar el comando
```
heroku addons:create heroku-postgresql
```

Una vez creada la base de datos de postgresql podemos obtener información de ella con estos dos comandos
```
heroku config
heroku pg
```

Tras generar la base de datos Heroku por defecto nos genera en la aplicación tres variables de entorno globales que nos haran falta para nuestro application.properties del proyecto para indicar que base de datos de postgresql usar
```
SPRING_DATASOURCE_URL
SPRING_DATASOURCE_USERNAME
SPRING_DATASOURCE_PASSWORD
```

Modificaremos el application.properties para que quede de esta manera
```
# Postgresql
spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
spring.datasource.initialization-mode=always
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
```

Al finalizar los cambios prepararemos todo para el despliegue de la aplicación aplicando los cambios a git (add, commit y push si el repositorio esta en remoto en Github por ejemplo)

Tras tener los cambios aplicados en el repositorio procederemos a desplegar la aplicación en Heroku con el comando
```
git push heroku master
```

Tras esto en la consola nos saldra un mensaje como este `https://myapp/ deployed to Heroku` la url indicada es la url de tu aplicación despleguada en Heroku

Para acceder a tu aplicación despleguada puedes acceder mediante la url o con el comando de Heroku
```
heroku open
```

Para finalizar tambien podemos ver los logs de la aplicaicón en nuestra consola mediante el comando
```
heroku logs --tail
```

***


## Otro ejemplo para despleguar nuestra app
* Con Docker => [Ver](https://github.com/DanielSantanoF/Dockerizacion_de_una_aplicacion_de_Spring_Boot_orientada_a_produccion)
