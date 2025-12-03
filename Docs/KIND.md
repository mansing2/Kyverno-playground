### Background

Kubernetes is an essential tool for container orchestration, but setting it up locally can often seem like a daunting task, there's a great tool called **Kind** (Kubernetes IN Docker) that allows you to run Kubernetes clusters on your local machine with ease. it is super useful for local development and testing, as it will enable you to simulate a multi-node Kubernetes environment

### Prerequisites

1. **Docker**: Kind uses Docker to create containers that simulate Kubernetes nodes. You'll need Docker installed and running. You can download Docker from here.
2. **Go (Optional)**: You'll need Go installed. Check out the [Go installation guide](https://golang.org/doc/install) if needed.
3. **Command-Line Interface (CLI)**: 

### Install KIND

./KIND-setup.mov

Option 1: macOS/Linux

```jsx
brew install kind
```

Option 2: Windows (Using Chocolatey)

```jsx
choco install kind
```

Once Kind is installed, verify it by checking its version.

```jsx
kind --version
> kind version 0.26.0
```

### Create a cluster

If you'd like to create a multi-node cluster, you can create a custom configuration file. Here's an example `kind-config.yaml` for a multi-node setup:

```bash
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

```bash
kind create cluster --config kind-config.yaml
```

### Interacting with Your Cluster

To verify that your cluster is running correctly, use `kubectl` to check the status of the nodes:

```bash
kubectl get nodes
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   68s   v1.32.0
kind-worker          Ready    <none>          53s   v1.32.0
kind-worker2         Ready    <none>          53s   v1.32.0
```

let's deploy a simple NGINX pod:

```bash
kubectl run nginx --image=nginx --restart=Never

kubectl expose pod nginx --type=NodePort --port=80

kubectl get service

NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
nginx        NodePort    10.111.245.234   <none>        80:30789/TCP   1m
```

We shall be able to access the nginx pod using `localhost:30789`.

### Deleting Cluster

```bash
kind delete cluster
```