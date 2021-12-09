# Comprobaciones:  

## Estado de k0s  

~~~

root@debian209-1:~# k0s status
Version: v1.22.2+k0s.1
Process ID: 4698
Role: controller
Workloads: true
~~~
## Cluster creado  

~~~
root@debian209-1:~# kubectl get all
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   86m
~~~  

## Nodos que forman el cluster  

~~~
root@debian209-1:~# kubectl get nodes
NAME          STATUS   ROLES    AGE     VERSION
debian209-1   Ready    <none>   5h53m   v1.22.2+k0s
~~~

## Información del pod:
~~~
root@servidork0s:~# k0s kubectl get all
NAME              READY   STATUS    RESTARTS   AGE
pod/pod-apache2   1/1     Running   0          15m

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   89m
~~~

## Información detallada del pod:

~~~
root@servidork0s:~# k0s kubectl describe pod/pod-apache2
Name:         pod-apache2
Namespace:    default
Priority:     0
Node:         servidork0s/27.0.172.224
Start Time:   Tue, 07 Dec 2021 22:21:13 +0100
Labels:       app=apache2
              autor=Manuel
              service=web
Annotations:  kubernetes.io/psp: 00-k0s-privileged
Status:       Running
IP:           10.244.0.13
IPs:
  IP:  10.244.0.13
Containers:
  contenedor-apache2:
    Container ID:   containerd://5f362d7df1b6be2bf8f25f29d6fbb0931450faa6f7c7448015bc5337f36c5fc5
    Image:          httpd
    Image ID:       docker.io/library/httpd@sha256:fba8a9f4290180ceee5c74638bb85ff21fd15961e6fdfa4def48e18820512bb1
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Tue, 07 Dec 2021 22:21:15 +0100
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-hmmzw (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-hmmzw:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  16m   default-scheduler  Successfully assigned default/pod-apache2 to servidork0s
  Normal  Pulling    16m   kubelet            Pulling image "httpd"
  Normal  Pulled     16m   kubelet            Successfully pulled image "httpd" in 1.239824329s
  Normal  Created    16m   kubelet            Created container contenedor-apache2
  Normal  Started    16m   kubelet            Started container contenedor-apache2
~~~