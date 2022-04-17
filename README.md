# Wekan

## Instalacion
### Mongodb
```bash
# Creamos un namespace
kubectl create ns wekan-project

helm install wekan bitnami/mongodb --version 10.31.4
# Obtener la password
kubectl get secret --namespace wekan-project wekan-mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode
# Realizamos un port-forward
kubectl port-forward --namespace wekan-project svc/wekan-mongodb 27017:27017
mongo admin --host 127.0.0.1 --authenticationDatabase admin -u root -p <password obtenida anteriormente>
use wekan
db.createUser(
   {
     user: "wekan",
     pwd: "<password obtenida anteriormente>",
     roles: [ "readWrite", "dbAdmin" ],
     mechanisms:[ "SCRAM-SHA-1" ]
   }
)
# Poner a un usuario determinado como admin del producto
use wekan
db.users.update({username:'roldyx'},{$set:{isAdmin:true}})
```
### Wekan
```
Configurar la 
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
kubectl apply -f sealedsecret.yaml

```
