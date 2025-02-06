1. Creo la imagen de mi app "app_luis" usando el Dockerfile que he creado.
    docker build -t app_luis .


2. Compruebo que la imagen ha sido creada.
    docker images


3. Me descargo la imagen de postgres 14
    docker pull postgres:14


4. Creación de un network para que ambos contenedores (la app y postgres) puedan comunicarse.
    docker network create network_luis


5. Desplegar PosgreSQL indicandole nombre del contendor, usuario, network a la que conectar y puerto al que apuntar.
    docker run -d --name postgres_luis -e POSTGRES_USER=luis -e POSTGRES_PASSWORD=luis01 -e POSTGRES_DB=master -p 5432:5432 --network network_luis -v postgres_data:/var/lib/postgresql/data postgres:14


6. Comprobamos que el contendor existe.
    docker container ps


7. Creamos el contenedor de la app indicando network, credenciales, puertos necesarios, conexiona al postgres y la versión.
    docker run -d --name app_container --network network_luis -e DB_HOST=postgres_luis -e DB_PORT=5432 -e DB_NAME=master -e DB_USER=luis -e DB_PASSWORD=luis01 -e VERSION=0.0.0-lll -p 5000:5000 app_luis


8. Comprobamos que los contenedores están conectados mediante el network.
    docker network inspect network_luis


9. Creación de usuario.
    curl -X POST http://localhost:5000/user -H "Content-Type: application/json" -d "{\"first_name\":\"Luis\", \"last_name\":\"Lloret\", \"age\":25, \"email\":\"luis@lloret.com\"}"


10. Comporbamos que se ha creqado el usuario.
    curl http://localhost:5000/user/1


11. Crear otro usuario.
    curl -X POST http://localhost:5000/user -H "Content-Type: application/json" -d "{\"first_name\":\"Pepe\", \"last_name\":\"Pepez\", \"age\":45, \"email\":\"pepe@pepez.com\"}"


12. Detener contenedores para comprobar la persistencia de datos.
    docker stop app_container postgres_luis


13. Volver a levantar los contenedores.
    docker start app_container postgres_luis


14. Comprobar persistencia de los datos.
    curl http://localhost:5000/count
    curl http://localhost:5000/user/1
    curl http://localhost:5000/user/2


15. Subir la imagen de app_luis a Docker hub para su uso posteriror en el ejercicio de kubernetes.
    docker login
    docker push lullll/app_luis:latest


16. Una vez que vemos que todo funciona, detener contenedores, borrarlos, borrar el network y volumenes.
    docker stop app_container postgres_luis
    docker rm postgres_luis app_container
    docker network rm network_luis
    docker volume rm postgres_data








