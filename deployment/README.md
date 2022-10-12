# Deployment

-   새로운 이미지의 Pod를 생성하고 기존 Pod를 제거한다.

```sh
$ kubectl create -f deployment.yaml

deployment.apps/hello-deployment created

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS    RESTARTS   AGE
pod/hello-deployment-66d4bc9449-dmdhf   1/1     Running   0          3m17s
pod/hello-deployment-66d4bc9449-lwhpt   1/1     Running   0          3m17s
pod/hello-deployment-66d4bc9449-vvkng   1/1     Running   0          3m17s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   3         3         3       3m17s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           3m17s

$ kubectl set image deployment.apps/hello-deployment van6065/hello-nodejs:v2

deployment.apps/hello-deployment image updated

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS              RESTARTS   AGE
pod/hello-deployment-66d4bc9449-dmdhf   1/1     Running             0          14m
pod/hello-deployment-66d4bc9449-lwhpt   1/1     Running             0          14m
pod/hello-deployment-66d4bc9449-vvkng   1/1     Running             0          14m
pod/hello-deployment-7878f588c9-2cphs   0/1     ContainerCreating   0          4s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   3         3         3       14m
replicaset.apps/hello-deployment-7878f588c9   1         1         0       4s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     1            3           14m

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS              RESTARTS   AGE
pod/hello-deployment-66d4bc9449-dmdhf   1/1     Running             0          14m
pod/hello-deployment-66d4bc9449-lwhpt   1/1     Terminating         0          14m
pod/hello-deployment-66d4bc9449-vvkng   1/1     Terminating         0          14m
pod/hello-deployment-7878f588c9-2cphs   1/1     Running             0          17s
pod/hello-deployment-7878f588c9-58sqt   1/1     Running             0          5s
pod/hello-deployment-7878f588c9-phzpt   0/1     ContainerCreating   0          1s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   1         1         1       14m
replicaset.apps/hello-deployment-7878f588c9   3         3         2       17s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           14m

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS        RESTARTS   AGE
pod/hello-deployment-66d4bc9449-dmdhf   0/1     Terminating   0          15m
pod/hello-deployment-66d4bc9449-lwhpt   0/1     Terminating   0          15m
pod/hello-deployment-66d4bc9449-vvkng   0/1     Terminating   0          15m
pod/hello-deployment-7878f588c9-2cphs   1/1     Running       0          51s
pod/hello-deployment-7878f588c9-58sqt   1/1     Running       0          39s
pod/hello-deployment-7878f588c9-phzpt   1/1     Running       0          35s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   0         0         0       15m
replicaset.apps/hello-deployment-7878f588c9   3         3         3       51s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           15m

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS        RESTARTS   AGE
pod/hello-deployment-66d4bc9449-dmdhf   0/1     Terminating   0          15m
pod/hello-deployment-7878f588c9-2cphs   1/1     Running       0          54s
pod/hello-deployment-7878f588c9-58sqt   1/1     Running       0          42s
pod/hello-deployment-7878f588c9-phzpt   1/1     Running       0          38s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   0         0         0       15m
replicaset.apps/hello-deployment-7878f588c9   3         3         3       54s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           15m

$ kubectl get po,rs,deploy

NAME                                    READY   STATUS    RESTARTS   AGE
pod/hello-deployment-7878f588c9-2cphs   1/1     Running   0          93s
pod/hello-deployment-7878f588c9-58sqt   1/1     Running   0          81s
pod/hello-deployment-7878f588c9-phzpt   1/1     Running   0          77s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/hello-deployment-66d4bc9449   0         0         0       15m
replicaset.apps/hello-deployment-7878f588c9   3         3         3       94s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/hello-deployment   3/3     3            3           15m
```
