
1. Creo un docker-compose que albergue PostgreSQL y la app con las configuraciones necesarias, usando la iamgen de Docker hub.


2. Levantar los container con el docker-compose.
    docker-compose up --build -d


3. Vemos si los containers están corriendo.
    docker container ps


4. Comprobamos que el network está levantado y comunica.
    docker network ls
    docker network inspect ejercicio_docker_compose_network_luis_compose


5. Extraemos la versión para ver que todo está funcionando.
    curl http://localhost:5000/version


6. Creación de usuario.
    curl -X POST http://localhost:5000/user -H "Content-Type: application/json" -d "{\"first_name\":\"Maria\", \"last_name\":\"Mariez\", \"age\":77, \"email\":\"maria@mariez.com\"}"


7. Comporbamos que se ha creado el usuario.
    curl http://localhost:5000/user/1


8. Crear otro usuario.
    curl -X POST http://localhost:5000/user -H "Content-Type: application/json" -d "{\"first_name\":\"Marta\", \"last_name\":\"Martez\", \"age\":23, \"email\":\"marta@martez.com\"}"


9. Detener contenedores para comprobar la persistencia de datos.
    docker-compose down


10. Volver a levantar los contenedores.
    docker-compose up -d


11. Comprobar persistencia de los datos.
    curl http://localhost:5000/count
    curl http://localhost:5000/user/1
    curl http://localhost:5000/user/2


12. Detener contenedores para que no interfieran en los demás ejercicios.
    docker-compose down
    docker volume rm ejercicio_docker_compose_postgres_data



