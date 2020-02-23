![sfeir-lunch-logo](https://raw.githubusercontent.com/Charon11/sfeir-lunch-k8s/master/doc/85259543_497659104232764_6938243096563941376_n.png)

# Install Minikube
Start by installing minikube with 
```shell 
brew cask install minikube
```
Start minikube 
```shell
minikube start
```

Enable ingress with 
```shell
minikube addons enable ingress
```

Start dashboard
```shell
minikube dashboard

🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:62252/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
```


# Pod
Add pod from pod.yml
```shell
kubectl apply -f pod.yml

namespace/pod created
configmap/sfeir-lunch-config created
pod/sfeir-lunch created
```

Show pod
```shell
kubectl get po -n pod

NAME          READY   STATUS    RESTARTS   AGE
sfeir-lunch   2/2     Running   0          6s
```

# Deployment

Add deployment from deployment.yml
```shell
kubectl apply -f deployment.yml

deployment.apps/sfeir-lunch-deploy created
```

Show deployment
```shell
kubectl get deploy

NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
sfeir-lunch-deploy   3/3     3            3           62s
```

# Service

Add service from service.yml
```shell
kubectl apply -f service.yml

service/sfeir-lunch-service created
```

Show deployment
```shell
kubectl get svc

NAME                  TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
sfeir-lunch-service   NodePort    10.96.145.7   <none>        80:32000/TCP   29s
```

# Ingress

Add ingress from ingress.yml
```shell
kubectl apply -f ingress.yml

ingress.networking.k8s.io/sfeir-lunch-ingress created
```

Show deployment
```shell
kubectl get ingresses

NAME                  HOSTS            ADDRESS        PORTS   AGE
sfeir-lunch-ingress   sfeir-lunch.lu   192.168.64.6   80      28s
```

Modify etc/hosts and add route
```shell
sudo vim /etc/hosts

+ 192.168.64.6    sfeir-lunch.lu
```

Curl
```shell
curl "http://sfeir-lunch.lu"
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```