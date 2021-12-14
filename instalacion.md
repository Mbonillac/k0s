# Instalación de k0s 
Aquí encontrarás los pasos necesarios para instalar k0s.  
Empecemos...

* 1. Actualizar los repositorios:
~~~ 
root@debian209-1:~# root@debian209-1:~# apt update
Hit:1 http://deb.debian.org/debian bullseye InRelease
Get:2 http://security.debian.org/debian-security bullseye-security InRelease [44.1 kB]
Get:3 http://deb.debian.org/debian bullseye-updates InRelease [39.4 kB]
Get:4 http://security.debian.org/debian-security bullseye-security/main Sources [68.7 kB]
Get:5 http://security.debian.org/debian-security bullseye-security/main amd64 Packages [97.5 kB]
Get:6 http://security.debian.org/debian-security bullseye-security/main Translation-en [60.5 kB]
Fetched 310 kB in 0s (676 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
31 packages can be upgraded. Run 'apt list --upgradable' to see them.

~~~

* 2. Descargar la ultima versión estable de K0s y hacemos que sea ejecutable y damos permisos de ejecución:

~~~
root@debian209-1:~# curl -L https://get.k0s.sh | sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   650  100   650    0     0   6914      0 --:--:-- --:--:-- --:--:--  6914
Downloading k0s from URL: https://github.com/k0sproject/k0s/releases/download/v1.22.2+k0s.1/k0s-v1.22.2+k0s.1-amd64
k0s is now executable in /usr/local/bin

root@servidork0s:~# chmod 777 /usr/local/bin/k0s
~~~

* 3. Instalamos k0s como controlador con instancias de un único nodo:

~~~
root@debian209-1:~# k0s install controller --single
INFO[2021-12-07 14:30:47] no config file given, using defaults
INFO[2021-12-07 14:30:47] creating user: etcd
INFO[2021-12-07 14:30:47] creating user: kube-apiserver
INFO[2021-12-07 14:30:47] creating user: konnectivity-server
INFO[2021-12-07 14:30:47] creating user: kube-scheduler
INFO[2021-12-07 14:30:47] Installing k0s service
~~~

* 4. Iniciamos k0s como servicio.

~~~
root@debian209-1:~# k0s start
~~~

5. Reiniciamos el servidor y comprobamos el estado del servicio

~~~
root@debian209-1:~# systemctl status k0scontroller.service
● k0scontroller.service - k0s - Zero Friction Kubernetes
     Loaded: loaded (/etc/systemd/system/k0scontroller.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2021-12-07 14:37:19 CET; 37s ago
       Docs: https://docs.k0sproject.io
   Main PID: 439 (k0s)
      Tasks: 115
     Memory: 852.7M
        CPU: 11.182s
     CGroup: /system.slice/k0scontroller.service
             ├─439 /usr/local/bin/k0s controller --single=true
             ├─474 /var/lib/k0s/bin/kine --endpoint=sqlite:///var/lib/k0s/db/state.db?more=rwc&_journal=WAL&cache=shared --listen-address=unix:///>
             ├─480 /var/lib/k0s/bin/kube-apiserver --secure-port=6443 --v=1 --kubelet-certificate-authority=/var/lib/k0s/pki/ca.crt --service-acco>
             ├─495 /var/lib/k0s/bin/kube-scheduler --kubeconfig=/var/lib/k0s/pki/scheduler.conf --v=1 --bind-address=127.0.0.1 --leader-elect=true>
             ├─499 /var/lib/k0s/bin/kube-controller-manager --use-service-account-credentials=true --profiling=false --terminated-pod-gc-threshold>
             ├─520 /var/lib/k0s/bin/containerd --root=/var/lib/k0s/containerd --state=/run/k0s/containerd --address=/run/k0s/containerd.sock --log>
             ├─635 /var/lib/k0s/bin/containerd-shim-runc-v2 -namespace k8s.io -id 04aeb34dababb9675ebb5106fd7ba951edc309195f7a0af6470a501ea8fb781e>
             ├─680 /var/lib/k0s/bin/containerd-shim-runc-v2 -namespace k8s.io -id 85f29812ad55683ddbec01c7ef136473aa589043d01b3cc017d45824d1f3831c>
             ├─741 /var/lib/k0s/bin/containerd-shim-runc-v2 -namespace k8s.io -id c1656672026913a95b3b5a438f26375bccf68aa5c62ed1c2d2ad6e4c3e258dc9>
             └─867 /var/lib/k0s/bin/containerd-shim-runc-v2 -namespace k8s.io -id 3acedfe42bd4a2b60f332a052e45995533f4e9956ecbb84b740f1a06d482a4a7>

Dec 07 14:37:46 debian209-1 k0s[439]: time="2021-12-07 14:37:46" level=info msg="I1207 14:37:46.843705     499 shared_informer.go:247] Caches are >
Dec 07 14:37:46 debian209-1 k0s[439]: time="2021-12-07 14:37:46" level=info msg="I1207 14:37:46.843721     499 garbagecollector.go:151] Garbage co>
Dec 07 14:37:46 debian209-1 k0s[439]: time="2021-12-07 14:37:46" level=info msg="I1207 14:37:46.914332     499 shared_informer.go:247] Caches are >
Dec 07 14:37:48 debian209-1 k0s[439]: time="2021-12-07 14:37:48" level=info msg="E1207 14:37:48.193234     480 available_controller.go:524] v1beta>
Dec 07 14:37:48 debian209-1 k0s[439]: time="2021-12-07 14:37:48" level=info msg="current cfg matches existing, not gonna do anything" component=ku>
Dec 07 14:37:48 debian209-1 k0s[439]: time="2021-12-07 14:37:48" level=info msg="current cfg matches existing, not gonna do anything" component=co>
Dec 07 14:37:49 debian209-1 k0s[439]: time="2021-12-07 14:37:49" level=info msg="W1207 14:37:49.199813     480 handler_proxy.go:104] no RequestInf>
Dec 07 14:37:49 debian209-1 k0s[439]: time="2021-12-07 14:37:49" level=info msg="E1207 14:37:49.199863     480 controller.go:116] loading OpenAPI >
Dec 07 14:37:49 debian209-1 k0s[439]: time="2021-12-07 14:37:49" level=info msg=", Header: map[Content-Type:[text/plain; charset=utf-8] X-Content->
Dec 07 14:37:49 debian209-1 k0s[439]: time="2021-12-07 14:37:49" level=info msg="I1207 14:37:49.199869     480 controller.go:129] OpenAPI Aggregat>
lines 1-30/30 (END)
~~~

6. Iniciamos el cluster:

~~~
root@debian209-1:~# k0s start
~~~

7.  Creamos un pod:

~~~
root@debian209-1:~# k0s kubectl apply -f apache2.yaml
pod/pod-apache2 created
~~~

8. Comprobamos que esta lanzado:

~~~
root@debian209-1:~# k0s kubectl get all
NAME              READY   STATUS    RESTARTS   AGE
pod/pod-apache2   1/1     Running   0          61s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   74m
~~~

8. 1 Entramos dentro del pod y editamos la web. (Realmente copiamos el index.html y con un echo le pasamos un título)
~~~
root@debian209-1:~# k0s kubectl exec pod/pod-apache2 -it -- /bin/bash
root@pod-apache2:/usr/local/apache2#  mv /usr/local/apache2/htdocs/index.html /usr/local/apache2/htdocs/index.html.original
root@pod-apache2:/usr/local/apache2# echo "Bienvenidos a la web de Manuel Bonilla" > /usr/local/apache2/htdocs/index.html
root@pod-apache2:/usr/local/apache2# exit
~~~

8. 2 Creamos pasarela

~~~
root@debian209-1:~# k0s kubectl port-forward pod/pod-apache2 80:80
Forwarding from 127.0.0.1:80 -> 80
Forwarding from [::1]:80 -> 80
~~~

9. Desde otra terminal accedemos a la web del pod:

![comprobacion acceso a localhost](https://github.com/Mbonillac/k0s/blob/main/imagenes/comprobacion-web-apache.png?raw=true)