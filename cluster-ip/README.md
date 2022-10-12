# Cluster IP

-   Pod와 통신할 수 있는 고정 IP를 만들어준다.

```sh
$ kubectl create -f cluster-ip.yaml
deployment.apps/hello-deployment created
service/hello-cluster-ip created

$ kubectl get deploy,svc

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   2/3     3            2           8s

NAME                       TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
service/hello-cluster-ip   ClusterIP   10.99.150.54   <none>        3000/TCP   8s
service/kubernetes         ClusterIP   10.96.0.1      <none>        443/TCP    5d

$ kubectl get nodes -o wide
NAME       STATUS   ROLES                  AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
minikube   Ready    control-plane,master   5d    v1.20.7   192.168.49.2   <none>        Ubuntu 20.04.2 LTS   4.19.121-linuxkit   docker://20.10.7

$ minikube ssh
Last login: Fri Oct  7 08:00:41 2022 from 192.168.49.1

$ docker@minikube:~$ curl 10.99.150.54:3000
hello

$ minikube service hello-cluster-ip

|-----------|------------------|-------------|--------------|
| NAMESPACE |       NAME       | TARGET PORT |     URL      |
|-----------|------------------|-------------|--------------|
| default   | hello-cluster-ip |             | No node port |
|-----------|------------------|-------------|--------------|
😿  service default/hello-cluster-ip has no node port
🏃  Starting tunnel for service hello-cluster-ip.
|-----------|------------------|-------------|------------------------|
| NAMESPACE |       NAME       | TARGET PORT |          URL           |
|-----------|------------------|-------------|------------------------|
| default   | hello-cluster-ip |             | http://127.0.0.1:50333 |
|-----------|------------------|-------------|------------------------|
🎉  Opening service default/hello-cluster-ip in default browser...
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

$ curl http://127.0.0.1:50333
hello%
```
