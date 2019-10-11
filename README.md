# Instrucciones

## OpenFaas
https://okteto.com/blog/how-to-develop-a-serverless-app-with-openfaas-and-okteto/

## MinIO
https://docs.min.io/docs/deploy-minio-on-kubernetes.html
https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/k8s-yaml.md

#### PVC (persistent volume claim)
```
kubectl create -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-pvc.yaml?raw=true
```

#### Deployment
```
kubectl create -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-deployment.yaml\?raw\=true
```

#### Service
Okteto no soporta el LoadBalancer que sugiere la guia (https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-service.yaml?raw=true). Por lo que se puede crear el servicio cambiando el tipo por ClusterIP.
```
kubectl create -f minio-clusterip-service.yaml
```

## Conectar con MinIO


## Clean up
```
kubectl delete -f minio-clusterip-service.yaml
kubectl delete -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-deployment.yaml\?raw\=true
kubectl delete -f https://github.com/minio/minio/blob/master/docs/orchestration/kubernetes/minio-standalone-pvc.yaml?raw=true
```
