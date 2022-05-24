## Links to resources

- https://github.com/k8s-cookbook/recipes

# From Chapter 1: getting started with Kubernetes in kubernetes cookbook

- [Kubernetes Playground from Kubernetes website](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- [Kubernetes Playground from Kataconda](https://www.katacoda.com/courses/kubernetes/playground)


**Kubernetes command line interface:**  
To interact with your kubernetes cluster you can use the kubernetes command line interface.  
For this, install kubectl (kube control) using brew

### Minikube

To use kubernetes for testing/dev/training on your local machine use minikube

- basically minikube allows you to use kubernetes on your local machine without any installation except the minikube binary
```bash
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.18.0/ \
                    minikube-linux-amd64
$ chmod +x minikube
$ sudo mv minikube /usr/local/bin/
```

- `minikube start` 
- `kubectl get nodes`
- [minikube docs](https://kubernetes.io/docs/tutorials/hello-minikube/)
- [minikube repo](https://github.com/kubernetes/minikube)
- `minikube start/stop/delete/ip/ssh/dashboard/docker-env`

minikube uses docker to be able to start containers. But in order to do this you need to set up the correct docker environment using `minikube docker-env`.  
You can use `minikube ssh` with `minikube ip` to log into the vm created by docker daemon allowing you to see logs and debug.  

Use `minikube dashboard` to see the kubernetes dashboard

### Starter example

Run the following to start the Ghost microblogging platform on minikube

```bash
$ kubectl run ghost --image=ghost:0.9
$ kubectl expose deployments ghost --port=2368 --type=NodePort
```

use `kubectl get pods` to monitor and use `minikube service ghost` to access ghost on browser

`kubectl run` and `kubectl expose` are both called _generators_. They are convenience commands to create a deployment and service object respectively.

# From Chapter 2: creating a kubernetes cluster in kubernetes cookbook



