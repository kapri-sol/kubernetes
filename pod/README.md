# Pod

-   Pod는 쿠버네티스에서 관리하는 최소 배포 단위이다.

-   Pod는 하나 이상의 컨테이너를 포함한다.

## 생성

```sh
$ kubectl create -f pod.yaml

pod/hello-pod created

$ kubectl get pods

NAME        READY   STATUS    RESTARTS   AGE
hello-pod   1/1     Running   0          17s

$ kubectl logs -f hello-pod

listen : 3000
```

## probe
