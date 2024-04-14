```shell
docker build -t kubia .
docker images
docker run --name kubia-container -p 8080:8080 -d kubia
docker stop kubia-container
docker rm kubia-container
docker tag kubia luksa/kubia
```


**Поднимаем  ReplicaSet**
```shell
kubectl create -f replicaset-kubia.yaml
replicaset.apps/kubia-replica-set created
kubectl get rs
NAME                        DESIRED   CURRENT   READY   AGE
hello-minikube-7f54cff968   1         1         1       14d
kubia-replica-set           3         3         3       9s
kubectl get po
NAME                              READY   STATUS    RESTARTS   AGE
hello-minikube-7f54cff968-dzb9x   1/1     Running   0          67m
kubia-replica-set-fdzmk           1/1     Running   0          13s
kubia-replica-set-n5h8h           1/1     Running   0          13s
kubia-replica-set-v4lgl           1/1     Running   0          13s
ssd-monitor-m848l                 1/1     Running   0          67m
```kubectl apply -f kubia.loadbalancer.yaml
service/kubia-load-balancer created
kubectl get service
NAME                  TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-minikube        NodePort       10.96.36.162     <none>        8080:32152/TCP   14d
kubernetes            ClusterIP      10.96.0.1        <none>        443/TCP          118d
kubia-load-balancer   LoadBalancer   10.109.208.252   <pending>     8080:30690/TCP   4s
minikube service kubia-http-balancer

❌  Exiting due to SVC_NOT_FOUND: Service 'kubia-http-balancer' was not found in 'default' namespace.
You may select another namespace by using 'minikube service kubia-http-balancer -n <namespace>'. Or list out all the services using 'minikube service list'

kubectl get service
NAME                  TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hello-minikube        NodePort       10.96.36.162     <none>        8080:32152/TCP   14d
kubernetes            ClusterIP      10.96.0.1        <none>        443/TCP          118d
kubia-load-balancer   LoadBalancer   10.109.208.252   <pending>     8080:30690/TCP   19s
minikube service kubia-load-balancer
|-----------|---------------------|-------------|---------------------------|
| NAMESPACE |        NAME         | TARGET PORT |            URL            |
|-----------|---------------------|-------------|---------------------------|
| default   | kubia-load-balancer |        8080 | http://192.168.64.3:30690 |
|-----------|---------------------|-------------|---------------------------|
🎉  Opening service default/kubia-load-balancer in default browser...
kubectl get op
error: the server doesn't have a resource type "op"
kubectl get po
NAME                              READY   STATUS    RESTARTS   AGE
hello-minikube-7f54cff968-dzb9x   1/1     Running   0          75m
kubia-replica-set-fdzmk           1/1     Running   0          8m25s
kubia-replica-set-n5h8h           1/1     Running   0          8m25s
kubia-replica-set-v4lgl           1/1     Running   0          8m25s
ssd-monitor-m848l                 1/1     Running   0          75m

`**Deployment заменяет RS и RC, упрощает работу**`

**Поднимаем LoadBalancer**
```shell

```









