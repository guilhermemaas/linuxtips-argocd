### Instalação
https://argo-cd.readthedocs.io/en/stable/
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

### Pegar a senha default de admin
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
echo pass | base64 -d
#pC1xs7QLa9b2jKOp
kubectl port-forward svc/argocd-server -n argocd 8080:443

### Database
O Argocd armazena os dados no ETCD

### Exemplos de apps
https://github.com/argoproj/argocd-example-apps

### O Argo cria alguns CRDs (Custom Resource Defitions). Um deles são as applications:
k get applications -A
NAMESPACE   NAME        SYNC STATUS   HEALTH STATUS
argocd      guestbook   Synced        Healthy

### O argo olha pra branch definida a cada 3 min para pegar diffs
targetRevision: HEAD

### Argocd com application set permite criar um set todo de aplicação (NS + Deployment) por pull request

### Webhooks Git x Argocd para deploy insta ao fazer commit
Usar o ngrok para lab