# Curso de Docker
Instruido por: Guido Vilariño


## 2. Las tres áreas en el desarrollo de software profesional


“Docker te permite construir, distribuir y ejecutar cualquier aplicación en cualquier lado.”

Problemáticas del desarrollo de software

1. **Construir** - Escribir código en la máquina del desarrollador. (Compile, que no compile, arreglar el bug, compartir código, etc. )

	Problemática:

	Entorno de desarrollo (paquetes)
	Dependencias (Frameworks, bibliotecas)
	Versiones de entornos de ejecución (runtime, versión Node)
	Equivalencia de entornos de desarrollo (compartir el código)
	Equivalencia con entornos productivos (pasar a producción)
	Servicios externos (integración con otros servicios ejem: base de datos)

2. **Distribuir** - Llevar la aplicación donde se va a desplegar (Transformarse en un artefacto)

	Problemática:

	Output de build heterogeo (múltiples compilaciones)
	Acceso a servidores productivos (No tenemos acceso al servidor)
	Ejecución nativa vs virtualizada
	Entornos Serverless

3. **Ejecutar** - Implementar la solución en el ambiente de producción (Subir a producción)
	El reto Hacer que funcione como debería funcionar

	**Problemática:**

	Dependencia de aplicación (paquetes, runtime)
	Compatibilidad con el entorno productivo (sistema operativo poco amigable con la solución)
	Disponibilidad de servicios externos (Acceso a los servicios externos)
	Recursos de hardware (Capacidad de ejecución - Menos memoria, procesador más debil)





## 3. Virtualización





## 4. Preparando tu entorno de trabajo

[Documentacion Docker](https://www.docker.com/get-started)


- Docker Desktop
- Docker Hub: Repo publico de lo que construimos con docker, se debe tener cuenta
- Play with docker: entorno gratuito, tiene tiempo limite de uso 4H


**Docker Desktop:**

Docker corre nativamente en linux, en Mac y Windows corre en una maquina virtual que tiene empaquetado docker

```sh
docker --version
docker info
'docker COMMAND --help'
```

Como instalar Docker con WSL 2 en Windows 10:
- https://www.youtube.com/watch?v=5s3cZJ_-68g







## 5. [Bonus] Play with Docker


loggearse en docker hub
abrir play with docker
Sesion en la nube de doker que podemos usar
Add new instance - es una pc entera q nos da docker, alli empieza a correr las 4H

Es una sesion






## 6. Qué es y cómo funciona Docker


Arquitectura de Docker

- DOCKER DAEMON: el corazon es el server de docker o docker daemon, es un servicio del SO
es la parte que interactua con el SO, permite usar los contenedores

- REST API: La forma en que docker daemon expone una interfaz para comunicarse con sigo es por una REST API
Protocolo http

- DOCKER CLI: Encima de la REST API tenemos un CLI que son los comandos que usamos, siempre usamos el cliente
de docker.

Tambien se puede crear una App cliente para comunicarnos con el Docker Daemon - docker tiene paquetes para diferentes
lenguajes de programacion

- CONTAINER: Los contenedores son el corazon de docker, sin containers docker no tiene sentido 

- IMAGE: Las imagenes son artefactos en los que docker empaqueta contenedores (empaquetado de nuestro codigo) y se pueden distribuir

- DATA VOLUMES, permite acceser con seguridad al sistema de archivos de la maquina anfitriona sin comprometer la seguridad

- NEETWORK: Permite a los contenedores comunicarse entre si o con el mundo exterior




## Componentes DENTRO del circulo de Docker:

- Docker daemon: Es el centro de docker, el corazón que gracias a el, podemos comunicarnos con los servicios de docker.
- REST API: Como cualquier otra API, es la que nos permite visualizar docker de forma “gráfica”.
- Cliente de docker: Gracias a este componente, podemos comunicarnos con el corazón de docker (Docker Daemon) que por defecto es la línea de comandos.

## Dentro de la arquitectura de Docker encontramos:

- Contenedores: Es la razón de ser de Docker, es donde podemos encapsular nuestras imagenes para llevarlas a otra computadora, o servidor, etc.
- Imagenes: Son las encapsulaciones de x contenedor. Podemos correr nuestra aplicación en Java por medio de una imagen, podemos utilizar Ubuntu para correr nuestro proyecto, etc.
- Volumenes de datos: Podemos acceder con seguridad al sistema de archivos de nuestra máquina.
- Redes: Son las que permiten la comunicación entre contenedores.






## 7. Primeros pasos: hola mundo

docker run hello-world

Lo que hace este contenedor es mostrar un mensaje en pantalla:

Hello from Docker!
This message shows that your installation appears to be working correctly.



WSL 2
- https://docs.docker.com/docker-for-windows/wsl/
- https://collectednotes.com/barckcode/docker-cheat-sheet

WSL 2 with Docker getting started 	
- https://www.youtube.com/watch?v=5RQbdMn04Oc

Desarrollando en Windows con WSL2 	
- https://www.youtube.com/watch?v=A0eqZujVfYU

Containers 							
- https://www.youtube.com/watch?v=0oEsMwSxBsk

Kubernetes y orquestar contenedores	
- https://www.youtube.com/watch?v=3RTvoI-A7UQ





## 8. Conceptos fundamentales de Docker: contenedores


### **Que es un contenedor ?**

Es una agrupación de procesos. que corren nativamente en la maquina en la maquina anfitriona y estan aislados del resto del sistema

Es una entidad lógica, no como una VM que es una agrupacion de una maquina fisica "aunque logica|virtualizada" que tiene sus abstracciones de memoria y CPU.

El contenedor esta limitada en cuanto a que cosas puede ver de la PC anfitriona, tiene un acceso limitado que nosotros le otorgamos a nuestra maquina.

No tienen forma de consumir más recursos que los que se les permite. Si esta restringido en memoria ram por ejemplo, es la única que pueden usar.

A fines prácticos los podemos imaginar cómo maquinas virtuales, pero NO lo son. Máquinas virtuales livianas.
Docker corre de forma nativa solo en Linux.

Sector del disco: Cuando un contenedor es ejecutado, el daemon de docker le dice, a partir de acá para arriba este disco es tuyo, pero no puedes subir mas arriba.

Docker hace que los procesos adentro de un contenedor este aislados del resto del sistema, no le permite ver más allá.

Cada contenedor tiene un ID único, también tiene un nombre.






## 9. Comprendiendo el estado de Docker


Comandos:

|  Uso | comando  |
|---|---|
| Corro el contenedor hello-world  | `docker run hello-world` |
| Muestra los contenedores activos	|	`docker ps` |
| Muestra todos los contenedores incluiso apagados o q terminaron su ciclo de vida	|	`docker ps -a` |
| Detalle completo de un contenedor	| `docker inspect <containe ID> `	|
| Igual que el anterior pero invocado con el nombre	| `docker inspect <name>`	|
| Le asigno un nombre custom “hello-platzi”	|	`docker run --name hello-platzi hello-world` |
| Cambio el nombre de hello-platzi a hola-platzi  | `docker rename hello-platzi hola-platzi`  |
| Borrar un contenedor  |  `docker rm <ID o nombre>` |
| Borra todos lo contenedores que esten parados | `docker container prune`  |
| Otra forma de ver los contenedores | `docker container ls -a` |
| Eliminar contenedor | `docker rm hello-platzi` |

CONTAINER ID se genera automaticamente por Docker
> No se permite tener 2 container con el mismo nombre en nuestra instalacion usar docker rename


# Comando básicos para la administración de imagenes y contenedores en docker.

## Contenedores

### Lifecycle

* `docker create` *Crea un contenedor pero no lo comienza*
* `docker rename` *Permite renombrar al contenedor*.
* `docker run` *Crea y comienza un contenedor en una operación*.
* `docker rm` *Elima un contenedor*.
* `docker update` *Actualiza los recursos limitados de un contenedor*.

### Iniciar y detener

* `docker start` *comienza un contenedor si se cayó o salió*.
* `docker stop` *detiene un contenedor*.
* `docker restart` *detiene y comienza un contenedor*.
* `docker pause` *pausa un contenedor corriendo, "lo congela"*. 
* `docker unpause` *quita la pausa de un contenedor corriendo*.
* `docker wait` *bloquea hasta que un contenedor corriendo se detiene*.
* `docker kill` *envía una SIGKILL a un contenedor corriendo*.
* `docker attach` *se conecta a un contenedor corriendo*.

### Informativos

* `docker ps` *muestra los contenedores corriendo*.
* `docker ps -a`   *muestra todos los contenedores corriendo y detenidos*.
* `docker logs` *obtiene logs de un container*.
* `docker inspect` *observa toda la info en un contenedor* _incluyendo variables de entorno_.
* `docker events` *obtiene eventos de un contenedor*.
* `docker port` *muestra el puerto publico de un contenedor*.
* `docker top` *muestra los procesos corriendo en un contenedor*.
* `docker stats` *muestra las estadisticas de recursos usados por contenedor*.
* `docker diff` *muestra los archivos cambiados en el FS del contenedor*.
* `docker stats --all` *muestra una lista de los contenedores corriendo*.
`
## Imagenes

### Lifecycle

* `docker images` *muestra todas las imagenes y tamaños*
* `docker import` *crea una imagen de un tarball*
* `docker build` *crea imagen de un  Dockerfile*
* `docker commit` *crea imagen de un contenedor, pausandolo temporalmente si esta corriendo.*
* `docker rmi` *remueve una imagen*.

### Informativos
* `docker history` *muestra el historial de una imagen*.
* `docker tag` *taggea una imagen a un nombre asignado*.


## 10. El modo interactivo

Comandos:


|  Uso | comando  |
|---|---|
| corre un ubuntu pero lo deja apagado | `docker run ubuntu` |
| lista todos los contenedores	| `docker ps -a` |
| Correr contenedor y entrar en la shell	| `docker run -it ubuntu`	|


- -i: interactivo
- -t: abre la consola

### Ver versión de linux
	cat /etc/lsb-release


- correr ubuntu de manera iteractiva
- abrir otra terminal y 
- correr docker ps 
- docker ps -a




## 11. Ciclo de vida de un contenedor


Cada q se ejecuta un contenedor esta ejecutando en realidad un proceso del sistema operativo
main process o proceso principal del contenedor, es el q determina si el container sigue vivo o no
por defecto un contenedor corre si el proceso principal sigue vivo.

es decir, si el proceso principal de un contenedor falla o se detine el contenedor tambien se detiene

un contenedor puede tener varios procesos corriendo pero solo se detiene el contenedor si el proceso
principal lo hace

```sh
# siempre que corra un contenedor yo le puedo especificar que comando debe correr

$ docker run --name alwaysup -d ubuntu tail -f /dev/null

# (ejecutar un proceso en un contenedor q ya existe)
docker exec 

# (Ingresar al contenedor en proceso secundario)
$ docker exec -it alwaysup bash 

$ ll
$ ps -aux

# el main process es el que tiene el PID = 1

$ exit
$ docker inspect --format '{{.State.Pid}}' alwaysup
$ kill <Id>
```

Relacion entre procesos que corren en el contenedor y el funcionamiento en si del contenedor.
Todo contenedor corre por lo menos un proceso o main process
El contenedor funciona si el main process esta funcionando


### Otros comentarios que se pueden usar

- `/dev/null`
- `/dev/full`
- `/dev/zero`
- `/dev/random`





## 12. Exponiendo contenedores



- `docker run -d --name proxy nginx` (corro un nginx)
- `docker stop proxy` (apaga el contenedor)
- `docker rm proxy` (borro el contenedor)
- `docker start proxy` (arranca el contenedor)
- `docker rm -f` <contenedor> (lo para y lo borra)
- `docker run -d --name proxy -p 8080:80 nginx` (corro un nginx y expongo el puerto 80 del contenedor en el puerto 8080 de mi máquina)
  localhost:8080 (desde mi navegador compruebo que funcione)
- `docker logs proxy` (veo los logs)
- `docker logs -f proxy` (hago un follow del log)
- `docker logs --tail 10 -f proxy` (veo y sigo solo las 10 últimas entradas del log)






## 13. Bind mounts

Manejo de datos en docker
conenedores, entidades auto-contenidas

**Bind mounts:** compartir archivos o datos entre contenedores, 
ata una ruta dentro de la maquina que ejecuta el contenedor con una ruta dentro del contenedor
todo lo que ocurra dentro de un contenedor va a quedar en esa ruta y aparecer ne la maquin anfitriona.

El riesgo es que le doy le contenedor acceso a una parte del disco

```sh
mkdir CursoDocker/dockerdata
cd .\CursoDocker\dockerdata\


$ mkdir dockerdata (creo un directorio en mi máquina)
$ docker run -d --name db mongo
$ docker ps (veo los contenedores activos)
$ docker exec -it db bash (entro al bash del contenedor)
$ mongo (binario de mongo dentro del container)


$ docker run -d --name db -v C:\Users\crist\CursoDocker\dockerdata\mongoData\:/data/db mongo
$ docker ps
$ docker exec -it db bash
$ mongo
	> use platzi
	switched to db platzi
	> db.users.insert({"nombre": "cvargas"})
	WriteResult({ "nInserted" : 1 })
	> exit
	bye
	root@dfb85eb6b036:/# exit
	exit

$ docker rm -f db
$ docker run -d --name mongo -v C:\Users\crist\CursoDocker\dockerdata\mongoData\:/data/db mongo
$ docker ps
$ docker exec -it mongo bash
$ mongo
	> use platzi
	switched to db platzi
	> db.users.find()
	{ "_id" : ObjectId("6119aa6cbb1772dd0426e433"), "nombre" : "cvargas" }
	>

```

WSL 2: 
- https://platzi.com/tutoriales/1650-prework/5895-aprende-a-instalar-wsl-2-de-la-manera-sencilla/






## 14. Volúmenes


Bind mount y volúmenes
Cuando usamos un contenedor, los datos generados se eliminan cuando el contenedor se detiene o se elimina, entonces, ¿cómo podemos guardar los datos? Hay dos formas de hacerlo enlazando el montaje y los volúmenes.

**Bind mount** nos ayuda a vincular un directorio en nuestra máquina a un directorio en un contenedor. Esto permite guardar datos en nuestro directorio y usar los mismos datos cada vez que usamos el contenedor.

Pero puede ser peligroso porque permitimos que el contenedor tenga acceso a un lugar en nuestra máquina y si el contenedor es malicioso, puede usar de mala manera cualquier información que tengamos en ese directorio.

**Los volúmenes** son la evolución del montaje de enlace. Los volúmenes resuelven los problemas de seguridad y privacidad que se encuentran en los montajes de enlace. ¿Como funciona? La parte del disco que compartimos con la ventana acoplable está completamente administrada por la ventana acoplable, y no tenemos acceso a menos que tengamos privilegios, pero es muy conveniente porque solo tenemos un lugar donde se almacenan los datos de nuestra ventana acoplable, y solo la ventana acoplable puede realizar modificaciones en eso.

```sh
# Listar los volumes
$ docker volume ls 

# Crear volumen
$ docker volume create dbdata 

# Correr BBDD y montar el volume
$ docker run -d --name db --mount src=dbdata,dst=/data/db mongo 

# Ver la información detallada del contenedor
$ docker inspect db

# Conectarme a la BBDD
$ mongo 

	## listo las BBDD
	shows dbs 
	## crear la BBDD platzi
	use platzi
	## insertar un nuevo dato
	db.users.insert({“nombre”:“guido”}) 
	## Buscar el nuevo dato
	db.users.find()
```


### Crear contenedor y asignar un volumen
docker run -d --name db --mount src=dbdata,dst=/data/db mongo

–mount es para asignar un volumen al contenedor, usando src le decimos que volumen es y dst (de destino) la ubicacion en el contenedor, mongo es la imagen.


- [Documentacion Volumenes docker](https://docs.docker.com/storage/volumes/)







## 15. Insertar y extraer archivos de un contenedor

#### Copiar archivo de mi Filesystem a un contenedor

```sh
$ touch prueba.txt
$ docker run -d --name copytest ubuntu tail -f /dev/null
$ docker ps
$ docker exec -it copytest bash
$ mkdir testing
$ exit
```

- Copiar prueba.txt -> carpeta /testing/ del contenedor y renombrar prueba.txt -> test.txt

$ docker cp prueba.txt copytest:/testing/test.txt
$ docker exec -ti copytest bash

- Copiar un archivo dentro de un contenedor a mi Filesystem

$ docker cp copytest:/testing localtesting

No es necesario q el contenedor este corriendo para hacer docker cp


### Documentacion
- [docker cp](https://docs.docker.com/engine/reference/commandline/cp/)




## 16. Conceptos fundamentales de Docker: imágenes

Hasta el momento se ha hablado el problema de la ejecucion de codigo de osea contenedores

Las imagenes son la solucion de construccion y distribucion de codigo

Plantillas o moldes a partir del cual se crea un contenedor

Una imagen es como una clase a partir de la cual de crean contenedores o objetos

###  Ver imagenes que tenemos en nuestro equipo
	$ docker image ls

una imagen vive en el disco como un conjunto de archivos o capas. el TAG latest es la ultima version
si no se especifica una version siempre trae latest

Docker descarga las imagenes de Docker Hub
https://hub.docker.com/

```sh
# Descargar una imagen
# docker pull <image_name>:<tag_version>
$ docker pull ubuntu
$ docker pull ubuntu:20.04
```

Nos muestra 2 imagenes de ubuntu latest y 20.04 eso es porque tenemos 2 punteros 
pero son lo mismo en el caso de ubuntu porque ya habiamos descargado ubuntu latest



## 17. Construyendo una imagen propia


Las imagenes se crean con un archivo que se llama Dockerfile
se crean con el comando build, se crea una imagen
luego se hace run

todo lo del Dockerfile se ejecuta en tiempo de build

```sh
$ mkdir imagenes
$ cd imagenes/
$ touch Dockerfile
$ code .
```

```docker
# Todos los Dockerfile comienzan con FROM y esta basado en algo mas en este caso vamos a usar ubuntu pero puede ser Node u otra imagen

FROM ubuntu:latest

# El comando RUN corre en tiempo de build, no al hacer docker run 
RUN touch /usr/src/hola-platzi-cvargas.txt
```

```sh
# docker build -t <imagen>:<tag> <ruta_contexto de build>
# en este caso el contexto aplica . por q en el directorio actual tengo el Dockerfile
# --file , -f		Nombre del Dockerfile (el valor predeterminado es 'PATH / Dockerfile')

$ docker build -t ubuntu:platzi_cvargas .
$ docker image ls
```

Una imagen es una forma logica de hablar de un conjunto de capas

### Loguien a docker hub
	$ docker login

### Re Tag para publicar nuestra imagen 
	$ docker tag ubuntu:platzi_cvargas ubuntu:platzi

### Publicar imagen
	$ docker 
	$ docker push 
	$ docker push cvargas9304/ubuntu:platzi



## 18. El sistema de capas

Cada capa es un pequeño cambio con respecto a la anterior

Las capas son el corazon de las imagenes

Cada uno de los comandos del Dockerfile genera una capa extra de codigo en nuestra imagen
|
una imagen es un nombre que apunta a una capa que apunta a otra capa y asi n veces

FROM Y RUN son capas esto es del Dockerfile

### Ver la info de como se construyó cada capa
	docker history ubuntu:platzi

### Ver la info de la imagen con el programa dive
	dive ubuntu:platzi

Las capas son inmutables, la inmutabilidad permite que se eficientes transferir imagenes a otras
tener esto en mente para saber como optimizar la imagen para que no ocupe tanto espacio y sea mas facil transferir

un contenedor tiene acceso a todas las capas de la imagen pero las ve a todas como el resultado

Al correr un contenedor se genera una capa mutable q es del contenedor, la ofrece docker
y solo es para el contenedor


### Investigar comando docker commit
https://docs.docker.com/engine/reference/commandline/commit/

### Herramienta Dive - ayuda a entender mejor como esta hecha una imagen
https://github.com/wagoodman/dive


- https://www.semantiq.com.mx/web/2020/03/25/comandos-de-respaldo-commit-exportar-e-importar-imagenes/
- https://phoenixnap.com/kb/how-to-commit-changes-to-docker-image


## 19. Usando Docker para desarrollar aplicaciones



Comandos:

```sh
$ git clone https://github.com/platzi/docker
$ docker build -t platziapp . (creo la imagen local)
$ docker image ls (listo las imagenes locales)
$ docker run --rm -p 3000:3000 platziapp (creo el contenedor y cuando se detenga se borra, lo publica el puerto 3000)
$ docker ps (veo los contenedores activos)
```



## 20. Aprovechando el caché de capas para estructurar correctamente tus imágenes

layer cache: si queremos contruir una capa que ya existe en el sistema docker aprovecha capas buildeadas

docker aprovecha las capas que ya buildio, para no repetir nada de lo que hizo

la layer base es la de FROM, si esta cambia daña el cache y vuelve a hacer todo desde el comienzo

estructurar bien el Dockerfile

---Concepto de un alumno
La clave está en estructurar nuestro Dockerfile de manera de que primero se copien todas las dependencias y posteriormente nuestro código fuente, que es el mas suceptible a cambios.








## 21. Docker networking: colaboración entre contenedores

1. Tener un contenedor de mongo
2. conectar nuestro contenedore


redes virtuales de doker o docker network

### listo las redes
	docker network ls 

### Redes:
- bridge: es una red por defecto 
- host: es una representacion virtual de la red de mi maquina
- none: si queremos q un conenedor no tenga acceso a nada

### Crear una red --attachable: nos permite q otros contenedores se conecten a esa red
	docker network create --attachable platzinet

### Correr container de mongo
	docker run -d --name db mongo

### Inspeccionar red
	docker network inspect platzinet -Inspeccionar la Red

### Conectar un contenedor a una red 
	docker network connect platzinet db

### Crear un contenedor conectado a una red 

MONGO_URL es una variable de entorno de index.js(app de ejemplo)

hostname es el nombre del contenedor, 27017 puerto por defecto de mongo, platziapp nombre de la imagen 
```sh
docker run -d --name <nombre_contenedor> -p 3000:3000 --env MONGO_URL=mongodb://<hostname>:27017/test platziapp
docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test platziapp
```

# Conectar el contendor de mi app a la red
	docker network connect platzinet app


Ahora tenemos 2 contenedores uno de mongo y otro con nuestra app 
y me estan ofreciendo la forma de trabajar como si estuviera en produccion

Vamos a trabajar con docker compose, herramienta q me permite hacer esto mas facil





## 22. Docker Compose: la herramienta todo en uno


Docker compose, es una manera de escribir de manera declarativa la arquitectura de servicios
que nuestra aplicacion necesita, mientras que los docker file se describen de manera imperativa, paso a paso.

En docker compose, hablamos de servicios, el cual puede tener mas de un contenedor.

### Borrar conenedores anteriores
	docker rm -f db app

### Iniciar los servicios declarados en el archivo de docker-compose.
	docker-compose up
	docker-compose up -d

### Crear las imagenes de los servicios de docker
	docker-compose build

### Visualizar los servicios que se están ejecutando.
	docker-compose ps


RECURSOS

- [Install Docker Compose](https://docs.docker.com/compose/install/)
- [Docker compose](https://iesgn.github.io/curso_docker_2021/sesion5/comando.html)


## 23. Subcomandos de Docker Compose


docker compose trabaja con servicios, no containers
los comandos aplican para los servicios contenidos en el archivo docker-compose.yml
tener en cuenta la ruta del archivo docker-compose.yml

### Listar redes
	docker network ls 

### Inspeccionar una red
	docker network inspect docker_default

### Veo todos los logs
	docker-compose logs 

### Solo veo el log del servicio “app”
	docker-compose logs app

### Follow o seguimiento a los logs del servicio app
	docker-compose logs -f app

### Entro al shell del contenedor app, no hace falta poner -it
	docker-compose exec app bash

### Ver contenedores generados por docker compose
	docker-compose ps

### Borrar todo lo generado por docker compose
	docker-compose down





## 24. Docker Compose como herramienta de desarrollo

### Contruye la imagen
```sh
docker-compose build
```
### Levanta los servicios del docker-compose
```sh
docker-compose up -d
```
--cambio en el codigo, cuando se hacen cambios hay que hacer re-build

### Contruye la imagen
```sh
docker-compose build app

docker-compose up -d
```

Agregar volumes a la altura del servicio

### Ver los logs de “app”
```sh
docker-compose logs app 
```

Usar docker compose como herramienta o ambiente de desarrollo,puedo usar varias tecnologias sin instalarlas en mi equipo

La ventaja de usar compose es q no tengo q crear containers, network a mano, etc.

Soluciones de monitoreo de archivos para diferentes tecnologias


- https://code.visualstudio.com/docs/remote/containers
- https://www.youtube.com/watch?v=KFyRLxiRKAc







## 25. Compose en equipo: override


docker-compose antes era un proyecto llamado fig

crear archivo docker-compose.override.yml, este archivo se combinara con el otro
sirve para hacer pequeños cambios sobre el compose file original

	docker-compose up -d
	docker-compose ps

	docker-compose exec app bash

### Levanta 2 instancias del servicio app en los puertos q corresponda
hay q modificar el docker-compose para admitir varios puertos

	docker-compose up -d --scale app=2
	docker-compose up -d --scale [nameService]=[numberContainers]


### Limpiar todo
	docker-compose down




El archivo docker-compose.overwrite.yml, permite sobre-escribir algunos parámetros 
del archivo principal de docker-compose.yml. Lo podemos usar para customizar entre distintos ambientes.

docker-compose scale servicio=X, para escalar (incrementar o decrementar) un número de servicios X según lo necesite.



Referencias:

- https://medium.com/it-dead-inside/making-sense-of-docker-compose-overrides-efb757460d64
- https://docs.docker.com/compose/reference/
- https://platzi.com/blog/django-docker/
- https://docs.docker.com/compose/reference/scale/




## 26. Administrando tu ambiente de Docker


Ser concientes de los recursos, impacto de docker, mantenimiento de docker
como administrar

###  veo todos los contenedores de mi máquina
	docker ps -a

### Borra todos los contenedores inactivos|apagados
	docker container prune 

### Borra todos los contenedores que estén corriendo o apagados
	docker rm -f $(docker ps -aq)

### Lista todas las redes
	docker network ls 

### Lista todos los volumes
	docker volume ls

### Lista todas las imágenes
	docker image ls

### Borrar lo inactivo
	docker [network|volume] prune

### Borra todo lo que no se esté usando
	docker system prune

### limito el uso de memoria
	docker run -d --name app --memory 1g platziapp
	docker run -d --name app --memory 4m platziapp

### Ver recursos consume docker en mi sistema
	docker stats 

### (puedo ver si el proceso muere por falta de recursos)
	docker inspect app 

ver la parte de State -> OOMKilled, si esta en true es que murio por memoria

https://github.com/platzi/docker




## 27. Deteniendo contenedores correctamente: SHELL vs. EXEC


```sh
cd avanzado/loop/
ll
```


### Construir la imagen
	docker build -t loop .

### Correr contenedor
	docker run -d --name looper loop


	docker stop looper (le envía la señal SIGTERM al contenedor)

### Proceso latest - ps ultimo proceso
	docker ps -l

- SIEMPRE QUE TENGAMOS UN CODIGO DE SALIDA SUPERIOR A 128, ES EL RESULTADO DE UNA SALIDA
POR UNA EXEPCION O UNA SEÑAL NO MANEJADA CORRECTAMENTE

	docker kill looper (le envía la señal SIGKILL al contenedor)

### Ver los procesos del contenedor
	docker exec looper ps -ef

RECORDAR QUE EL PROCESO PRINCIPAL DE UN CONTENEDOR SE ENCUENTRA CON EL PID 1
EL PROBLEMA ES QUE ESTA CORRIENDO ASI: /bin/sh -c /loop.sh
ESO QUIERE DECIR QUE /loop.sh ES HIJO DEL SHELL /bin/sh

```docker

### Shell: Ejecuta el proceso como hijo del shell

FROM ubuntu:trusty
COPY ["loop.sh", "/"]
CMD /loop.sh


### Exec: Ejecuta el comando como principal

FROM ubuntu:trusty
COPY ["loop.sh", "/"]
CMD ["/loop.sh"]
```

Recomendacion usar formato Exec y no Shell, el shell tiene consecuencias no deseables




[Comandos RUN, CMD y ENTRYPOINT en el Dockerfile](https://dockertips.com/comandos-run-cmd-y-entrypoint-en-el-dockerfile)







28. Contenedores ejecutables: ENTRYPOINT vs CMD


cd avanzado/ping

docker buils -t ping . (construyo la imagen)
docker run --name pinger ping <hostname> (ahora le puedo pasar un parámetro, previamente tengo que agregar el ENTRYPOINT en el Dockerfile)

```docker
FROM ubuntu:trusty
CMD ["/bin/ping", "-c", "3","localhost"]
El parametro que enviamos por linea de comandos sobreescribe
"/bin/ping", "-c", "3","localhost"

FROM ubuntu:trusty
ENTRYPOINT [ "/bin/ping", "-c", "3"]
CMD ["localhost"]
De esta manera solo se sobreescribe localhost
```


- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker CMD vs. Entrypoint Commands: What's the Difference?](https://phoenixnap.com/kb/docker-cmd-vs-entrypoint)
- [Understand how CMD and ENTRYPOINT interact](https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact)






## 29. El contexto de build

Cada ve que vamos a hacer una imagen, docker monta en un Filesystem temporal
todos los archivos disponibles en la ruta que le paso como ultimo parametro al docker build
hasta ahora hemos usado . (punto)

Esta es la forma en la que docker se asegura de no acceder a una area que no debe acceder durante un build

Es no copiar cosas q no necesito


Dockerfile:

#Copiar todos los harchivos hasta la ruta /usr/src/
COPY [".", "/usr/src/"]


### Archivos|direcotrios para no considerar en el contexto de build
.dockerignore





- [dockerignore file](https://docs.docker.com/engine/reference/builder/#dockerignore-file)







## 30. Multi-stage build

Casos donde yo no quiero que mi codigo del proyecto este en mi imagen productiva final
especialmente para lenguajes compilados. donde se busca solo tener el artefacto ejecutable

Otro caso es el codigo de test, solo quiero que este en el proyecto, no en la imagen productiva

Funcionalidad para Optimizar imagenes productivas sin tener que incluir todo lo q usamos en tiempo de dev o test
en un solo Dockerfile y aprovechando el cache de las capas para que se construyan rapido

Recordar la optimizacion de la imagenes en funcion del cache imagen

Ver carpeta build del repo proyect

### Especifíco la ruta del Dockerfile si lo tenemos en otra ruta, 
Observar el using cache (No se toma nada de tiempo y es util para la app productivas con muchas dependencias)

	docker build -t prodapp -f build/production.Dockerfile . 

	docker run -d --name prod prodapp


Resumen: Oprimizar imagenes productivas, sin incluir todo lo que teniamos en tiempo de desarrollo, test,
en un solo Dockerfile reusando el caache de las capas para que se construyan rapido


- https://www.docker.com/blog/advanced-dockerfiles-faster-builds-and-smaller-images-using-buildkit-and-multistage-builds/
- https://medium.com/@serrodcal/construcci%C3%B3n-de-im%C3%A1genes-docker-en-m%C3%BAltiples-etapas-7933179a3e1f
- https://docs.microsoft.com/es-es/visualstudio/docker/tutorials/image-building-best-practices



## 32. Docker-in-Docker

Posibilidad de usar docker desde otros containers

Docker daemon le hablamos a traves de una interfaz, en nuestra maquina

en linux todo es un archivo podemos montar archivos sobre conteainers

el cliente de nuestra maquinas le habla a docker a traves de un socket


contenedor que tiene docker 

### esto funciona en linux y mac no en wind (es curioso a mi me funciono)
	docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:19.03.12


### Dentro del contenedor que creamos hacemos docker ps

	docker run -d --name app prodapp

### Correr contenedor con mi docker socket y mi binario de docker cliente
docker run --rm it -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/bin/docker wagoodman/dive:latest prodapp

correr contenedores que pueden tener el control de la instalacion de docker 
y pueden correr otros contenedores

Es peligroso darle a un contenendor que no conocemos de una imagen que no entendemos 
acceso a nuestro sistema de docker. en un ambiente controlado puede ser.



---- Notas alumnos:

Un socket en sistemas Unix se utiliza para comunicación entre procesos. El docker deamon es el que tiene acceso a las imagenes y containers y este se comunica con la maquina host a traves del socket. Lo que estamos haciendo aquí es comunicar a un docker deamon en un contenedor a el docker deamon de la maquina host a traves del socket.
Sobre los usos de docker-in-docker… la verdad es que es recomendable no usarlo nunca porque trae problemas técnicos muy precisos que relaciona a como esta implementado docker. El responsable de docker-in-docker creo un articulo donde habla al respecto:
https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/#:~:text=The primary purpose of Docker,into your Jenkins container instead.

Si quieres saber mas sobre como usar docker-in-docker y usar mejores alternativas te recomiendo este articulo:
https://blog.nestybox.com/2019/09/14/dind.html

En resumen: Solo usa docker-in-docker como sandbox, para experimentar con contenedores e imágenes. Y si quieres algo parecido a docker-in-docker mejor usa sysbox.


el socket de docker conserva el estado de docker y una de las mejores herramientas hechas para docker es Prometheus que te permite monitoriar tus contenedores y esta herramienta necesita saber el estado de docker asi que ase uso del socket


