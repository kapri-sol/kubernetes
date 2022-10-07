# Replica Set

-   pod의 수가 일정하게 유지되게 관리한다.

## 실행

```sh
$ kubectl create -f replica-set.yaml

replicaset.apps/hello-replica created

$ kubectl get pods

NAME                  READY   STATUS    RESTARTS   AGE
hello-replica-tq25v   1/1     Running   0          23s
```
