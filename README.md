# Kubernetes Policy Playground with Kyverno
This repository is a playground environment to experiment with Kubernetes workloads and policies using Kyverno.

It assumes you are running a local Kubernetes cluster and want to understand how Kyverno works in practice. 


# Prerequisites
Before getting started, make sure you have the Kubernetes Cluster set up, just in case you want to set up everything from a scratch refer [Playground Setup Guide](Docs/KIND.md)

# Install Kyverno
Kyverno is installed using Helm.

```jsx
helm repo add kyverno https://kyverno.github.io/kyverno/
helm repo update
helm install kyverno kyverno/kyverno -n kyverno --create-namespace
```

Verify Kyversno Installation
```jsx
kubectl get pods -n kyverno
```