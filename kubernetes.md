## Links to resources

- https://github.com/k8s-cookbook/recipes
- https://kubernetes.io/training/

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

- install kubeadm on all the servers that will be part of your kubernetes cluster -- master and other nodes. For Ubuntu, that looks like

```bash
# apt-get update && apt-get install -y apt-transport-https

# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

# cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
  deb http://apt.kubernetes.io/ kubernetes-xenial main
  EOF

# apt-get update
```

Then install these

```bash
# apt-get install -y docker.io
# apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```

- initialise cluster with `kubeadm init`
- after initialising cluster on the master node, collect the token and join the other nodes by running this on the node terminals: `kubeadmin join --token <token>`
- on the master node terminal you can run: `kubectl get nodes` to see results
- finally it is required to create a network that satisfies 







