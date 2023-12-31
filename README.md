## Kubernetes playaround

For local deployment with Minikube

Cluster with two pods: 
- one for mongodb database v5.0 and the other for simple webapp (also from Docker hub)

#### K8s manifest files 
* mongo-config.yaml
* mongo-secret.yaml
* mongo.yaml
* webapp.yaml

#### K8s commands

##### start Minikube and check status
    minikube start
    minikube status

##### get minikube node's ip address
    minikube ip

##### get basic info about k8s components
    kubectl get node
    kubectl get pod
    kubectl get service
    kubectl get all

##### get extended info about components
    kubectl get pod -o wide
    kubectl get node -o wide

##### get detailed info about a specific component
    kubectl describe svc {svc-name}
    kubectl describe pod {pod-name}

##### get application logs
    kubectl logs {pod-name}
    
##### stop your Minikube cluster
    minikube stop

<br />

### Project startup steps

    minikube start

In terminal, while positioned in ```kubernetes-playaround``` folder, execute next commands (order is important):

    kubectl apply -f mongo-config.yaml

    kubectl apply -f mongo-secret.yaml

    kubectl apply -f mongo.yaml

    kubectl apply -f webapp.yaml


Check Minikube IP adress with: 
    
    minikube ip

Use that address and port: 30100 to access webapp through browser, for example: http://192.168.49.2:30100

### Possible startup problems solutions

If the NodePort service webapp with `MinikubeIP:NodePort` is not accessible through browser, next command can be executed to start service:
    
    minikube service webapp-service

<br />

For encoding/decoding secrets base64 had been used with next commands: 

    echo mysupersecret | base64
    echo mysupersecret | base64 --decode

..but had problems with starting mongodb deployment if those are ran in macOS, so running them in online encoding tool and then pasting back to secret's file helped