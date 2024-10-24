### Integracao github x argo para login 
- dex com auth2
- Precisa criar uma org, time e configurar uma url valida do seu argo para callback (Authorization callback URL).
- Gerar um client ID para configurar no values do helm do Argo.

### Dex Docs
Está nos parâmetros de instalação do argo no aulão do dia 5.

###
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argocd/argo-cd -f ./aulao/argocd/install.yaml -n argocd --create-namespace
helm upgrade --install argocd argocd/argo-cd -f ./aulao/argocd/install.yaml -n argocd --create-namespace

### Exemplo config do values.yaml
configs:
  params:
    server.insecure: true
    server.dex.server: http://argocd-dex-server:5556
    dexserver.disable.tls: true
    server.dex.server.strict.tls: false
  cm:
    url: http://argocd.bernardolopes.com
    dex.config: |
      connectors:
      - type: github
        id: github
        name: GitHub
        config:
          clientID: eeb0d5439fa3d775eca7
          clientSecret: c0cd97e254b5ca84e7c68c67763b94852c628610
          orgs: 
          - name: Treinamento-ArgoCD

  rbac:
    policy.default: role:readonly
    policy.csv: |
      p, role:org-admin, applications, *, */*, allow
      p, role:org-admin, clusters, get, *, allow
      p, role:org-admin, repositories, *, *, allow
      p, role:org-admin, logs, get, *, allow
      p, role:org-admin, exec, create, */*, allow
      g, Treinamento-ArgoCD:DevOps, role:org-admin
    scopes: '[groups]'

### Adicionar permissao para um usuario de fora da org do GitHub logar como admin:
![alt text](image.png)


### Prometheus
kube-prometheus
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace

selector:
matchLabels:
    app: kube-prometheus-stack-alertmanager
    release: prometheus
    self-monitor: "true"


kubectl get prometheusrules -n monitoring
kubectl get servicemonitor -n monitoring


## Notificaoes:
https://github.com/argoproj/argo-helm/blob/main/charts/argo-cd/values.yaml