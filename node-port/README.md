# Node Port

-   클러스터 외부에서 Node로 직접 접근해서 Pod와 통신할 수 있다.

```sh
$ kubectl create -f node-port.yaml

deployment.apps/hello-deployment created
service/hello-node-port created

$ kubectl get deploy,svc
NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           21s

NAME                      TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/hello-node-port   NodePort    10.98.70.130   <none>        3000:31000/TCP   21s
service/kubernetes        ClusterIP   10.96.0.1      <none>        443/TCP          5d

$ minikube service hello-node-port

|-----------|-----------------|-------------|---------------------------|
| NAMESPACE |      NAME       | TARGET PORT |            URL            |
|-----------|-----------------|-------------|---------------------------|
| default   | hello-node-port |        3000 | http://192.168.49.2:31000 |
|-----------|-----------------|-------------|---------------------------|
🏃  Starting tunnel for service hello-node-port.
|-----------|-----------------|-------------|------------------------|
| NAMESPACE |      NAME       | TARGET PORT |          URL           |
|-----------|-----------------|-------------|------------------------|
| default   | hello-node-port |             | http://127.0.0.1:50965 |
|-----------|-----------------|-------------|------------------------|
🎉  Opening service default/hello-node-port in default browser...
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

$ curl http://192.168.49.2:31000
```
