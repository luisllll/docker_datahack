
1. Arrancar minikube.
    minikube start


2. Crear archivo namespace.



3. Crear un PVC para perisistir los datos (postgres-pvc).



4. Crear archivo de Deployment y Service de PostgreSQL.(postgres-deployment).



5. Crear archivo de Deployment y Service de Flask (flask-deployment) usando la imagen de la app alojada en Docker Hub.

    


6. Desplegar recursos en kubernetes.
    kubectl apply -f namespace.yaml
    kubectl apply -f postgres-pvc.yaml
    kubectl apply -f postgres-deployment.yaml
    kubectl apply -f flask-deployment.yaml



7. Comporbamos despliegue.
    kubectl get pods -n app-luis



8. Obtener url de la app.
    minikube service flask-service -n app-luis --url



9. Comporbar versión de la aplicacion. Estos comandos deben ejecutarse en una nueva terminal, una vez se haya abierto la dirección url.
    curl {url que se obtenga}/version
    curl http://127.0.0.1:62539/version #ejemplo


10. Crear un usuario.
        curl -X POST {url que se obtenga}/user -H "Content-Type: application/json" -d "{\"first_name\":\"Pablo\", \"last_name\":\"Pablez\", \"age\":60, \"email\":\"pablo@pablez.com\"}"


11. Comporbamos que se ha creqado el usuario.
    curl {url que se obtenga}/user/1



12. Crear otro usuario.
        curl -X POST {url que se obtenga}/user -H "Content-Type: application/json" -d "{\"first_name\":\"Laura\", \"last_name\":\"Laurez\", \"age\":44, \"email\":\"laura@laurez.com\"}"


13. Reiniciar los pods para comprobar persistencia.
    kubectl delete pod --all -n app-luis


14. Verificar que los pods se han reiniciado.
    kubectl get pods -n app-luis


15. Comprobar persistencia de los datos.
    curl {url que se obtenga}/count
    curl {url que se obtenga}/user/1
    curl {url que se obtenga}/user/2


16. Eliminar todos los deplyments, services y recursos del namespace.
    kubectl delete pvc postgres-pvc -n app-luis
    kubectl delete namespace app-luis





