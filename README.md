ArgoCD
---
Argo CD on `lumos.run`.

1. Install Argo CD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. Change ArgoCD to insecure

```
kubectl patch -n argocd configmap argocd-cmd-params-cm -p '{"data": {"server.insecure": "true"}}'
kubectl rollout -n argocd restart deployment argocd-server
```

2. Apply Ingress

```
kubectl apply -n argocd -f ingress.yaml
```

3. Enable GitHub Authentication

```
# Set GitHub OAuth App Client ID and Secret
export GITHUB_CLIENT_ID=<GitHub OAuth App Client ID>
export GITHUB_CLIENT_SECRET=<GitHub OAuth App Client Secret>

kubectl patch -n argocd configmap argocd-cm -p "$(envsubst < argocd-cm.yaml)"
kubectl patch -n argocd configmap argocd-rbac-cm -p "$(envsubst < argocd-rbac-cm.yaml)"
kubectl rollout -n argocd restart deployment argocd-server
```
