# Replica Set

-   pod의 수가 일정하게 유지되게 관리한다.
-   label이 일치하는 pod를 관리한다.

## 실행

```sh
$ kubectl create -f replica.yaml

replicaset.apps/hello-replica created

$ kubectl get pods


NAME                  READY   STATUS    RESTARTS   AGE
hello-replica-bwsjf   1/1     Running   0          5s

$ kubectl get replicaset

NAME            DESIRED   CURRENT   READY   AGE
hello-replica   1         1         1       3m

$ kubectl delete pod hello-replica-bwsjf
pod "hello-replica-bwsjf" deleted

$ kubectl get pods

NAME                  READY   STATUS        RESTARTS   AGE
hello-replica-bwsjf   1/1     Terminating   0          27s
hello-replica-rndw4   1/1     Running       0          7s

$ kubectl get pods

NAME                  READY   STATUS    RESTARTS   AGE
hello-replica-rndw4   1/1     Running   0          48s

$ kubectl get pod --show-labels

NAME                  READY   STATUS    RESTARTS   AGE   LABELS
hello-replica-rndw4   1/1     Running   0          24m   app=hello-pod

$ kubectl label pod hello-replica-rndw4 app-

pod/hello-replica-rndw4 labeled

$ kubectl get pods --show-labels

NAME                  READY   STATUS    RESTARTS   AGE   LABELS
hello-replica-7kd5g   1/1     Running   0          12s   app=hello-pod
hello-replica-rndw4   1/1     Running   0          25m   <none>

$ kubectl apply -f replica.yaml

replicaset.apps/hello-replica configured

$ kubectl get pods

NAME                  READY   STATUS    RESTARTS   AGE
hello-replica-77f87   1/1     Running   0          4m36s
hello-replica-7kd5g   1/1     Running   0          10m
hello-replica-8dpth   1/1     Running   0          4m36s
```
