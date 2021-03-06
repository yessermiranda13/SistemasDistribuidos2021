# Taller Kubernetes 
![Imagen de Arquitectura de kubernetes](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)
Este taller puede ser realizado de las siguientes maneras:
 * [Usando un escenario de Katacoda con todo preparado](https://www.katacoda.com/cloudnativeplusgt/scenarios/k8s_up_running)
 * [Instalando kubernetes de forma local](https://kubernetes.io/docs/tasks/tools/)
 * [Usando una instancia de kubernetes de un proveedor de la nube](https://azure.microsoft.com/en-us/services/kubernetes-service/)

## Practica 1 - Creacion de un pod


#### Ver estado de los nodos

```bash
kubectl get nodes 
```

#### Crear pod a partir de imagen NGINX

```bash
kubectl run nginx --image=nginx --restart=Never 
```

#### Ver estado del pod

```bash
kubectl get pods
```

#### Exponer puerto para acceso externo

```bash
kubectl expose pod/nginx --port=80 --target-port=80 --type=NodePort --name=nginx-svc
```


## Practica #2 - Servidor Node


#### Crear pod a partir de imagen NodeJS

```bash
kubectl run nodejs --image=alesandrog/nodejs-uraccan --restart=Never 
```

#### Ver estado del pod

```bash
kubectl get pods
```

#### Exponer puerto para acceso externo

```bash
kubectl expose pod/nodejs --port=3000 --target-port=3000 --type=NodePort --name=nodejs-svc
```

### Monitoreo del Pod

#### Ver logs del pod

```bash
kubectl logs pod/nodejs
```

#### Ingresar a bash

```bash
kubectl exec -it nodejs -- /bin/bash
```

#### Eliminar pod

```bash
kubectl delete pod/nodejs
```


## Practica #3 - Deployment con .YAML


#### Crear archivo deployment.yml

```bash
vim deployment.yml
```

#### Construir deployment a partir del archivo

```bash
kubectl apply -f deployment.yml
```

#### Verificar estado del deployment

```bash
kubectl get deployments 
```

#### Verificar que la cantidad de replicas sea correcta

```bash
kubectl get pods
```

#### Generar LoadBalancer para el deployment

```bash
kubectl expose deployment/app1 --port=3000 --target-port=3000 --type=LoadBalancer --name=balanceador
```

#### Ver puerto abierto para el LoadBalancer

```bash
kubectl get services
```

#### Ver informacion detallada del deployment

```bash
kubectl describe deployment/app1 
```