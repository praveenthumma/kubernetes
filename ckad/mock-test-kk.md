## Mock Test
```console

# Deploy a pod named reverse-proxy using the nginx:alpine image.
k run nginx-448839 --image=nginx:alpine

# Create a namespace named mynamespace

k create ns mynamespace

# Create a new Deployment named apache-frontend with 3 replicas using image httpd:2.4-alpine

k create deployment apache-frontend --image=httpd:2.4-alpine -replicas=3


# Deploy a dispatcher pod using the redis:alpine image with the labels set to env=production.

k run dispatcher --i=redis:alpine -l env=production

# A replicaset super-replica is created. However the pods are not coming up. Identify and fix the issue.

k create -f super-replica.yaml 

#

k expose deployment/redis  --name=messaging-service --port=6379 --type=ClusterIP -n=marketing -l name=redis-pod


# Create a new ConfigMap named cm-3392845. Use the spec given on the below.
# ConfigName Name: cm-3392845
# Data: DB_NAME=SQL3322
# Data: DB_HOST=sql322.mycompany.com
# Data: DB_PORT=3306

k create configmap cm-3392845 --from-literal=DB_NAME=SQL3322 --from-literal=DB_HOST=sql322.mycompany.com --from-literal=DB_PORT=3306

# Create a new Secret named db-secret-xxdf with the data given (on the below).
# Secret Name: db-secret-xxdf
# Secret 1: DB_Host=sql01
# Secret 2: DB_User=root
# Secret 3: DB_Password=password123
 k create secret generic db-secret-xxdf  --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123

# Export the logs of the e-com-1123 pod to the file /opt/outputs/e-com-1123.logs
k logs e-com-1123 -n=e-commerce > /opt/outputs/e-com-1123.logs

Create a Persistent Volume with the given specification.
# Volume Name: pv-analytics
# Storage: 100Mi
# Access modes: ReadWriteMany
# Host Path: /pv/data-analytics

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: "/pv/data-analytics"

# Create a redis deployment using the image redis:alpine with 1 replica and label app=redis.
# Expose it via a ClusterIP service called redis on port 6379.
# Create a new Ingress Type NetworkPolicy called redis-access which allows only the pods with label access=redis to access the deployment.


kubectl create deployment redis --image=redis:alpine --replicas=1
kubectl expose deployment redis --name=redis --port=6379 --target-port=6379

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: redis-access
  namespace: default
spec:
  podSelector:
    matchLabels:
       app: redis
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          access: redis
    ports:
     - protocol: TCP
       port: 6379

```
