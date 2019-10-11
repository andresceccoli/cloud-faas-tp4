# Instrucciones

## OpenFaas
https://okteto.com/blog/how-to-develop-a-serverless-app-with-openfaas-and-okteto/

## MinIO

#### En Docker
https://docs.min.io/docs/minio-docker-quickstart-guide.html

#### En Okteto - solo como referencia
https://docs.min.io/docs/deploy-minio-on-kubernetes.html
https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/k8s-yaml.md

PVC (persistent volume claim)
```
kubectl create -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-pvc.yaml?raw=true
```

Deployment
```
kubectl create -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-deployment.yaml\?raw\=true
```

Service
Okteto no soporta el LoadBalancer que sugiere la guia (https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-service.yaml?raw=true). Por lo que se puede crear el servicio cambiando el tipo por ClusterIP.
```
kubectl create -f minio-clusterip-service.yaml
```

## Administrar MinIO con la herramienta mc

https://docs.min.io/docs/minio-client-quickstart-guide.html

## Conectar OpenFaas con MinIO

Crear funcion node con faas-cli y agregar el cliente minio para javascript  

https://docs.min.io/docs/javascript-client-quickstart-guide.html

Tener en cuenta el endPoint y puerto correcto dependiendo del deployment de minio.

#### Funciones
Implementar las siguientes funciones:
- Crear bucket: crea un nuevo bucket solo si no existe. En caso de existir, debe retornar un mensaje indicando la situacion.
- Listar buckets: devuelve la lista de buckets creados


## Cleanup
```
kubectl delete -f minio-clusterip-service.yaml  
kubectl delete -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-deployment.yaml\?raw\=true  
kubectl delete -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-pvc.yaml?raw=true  
kubectl delete -f https://raw.githubusercontent.com/okteto/samples/master/openfaas/openfaas.yml  
kubectl delete secret basic-auth  
```
