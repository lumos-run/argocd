ArgoCD
---
Argo CD on `lumos.run`.

1. Install Argo CD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. Apply Ingress

```
kubectl apply -n argocd ingress.yaml
```
