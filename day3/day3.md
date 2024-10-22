### Com applicationset para ignorar uma pasta no generator, por git por exemplo:
apiVersion: argoproj.io/v1alhpa1
kind: ApplicationSet
metadata:
  name: cluster-addons
  namespace: argocd
spec:
  goTemplate: true
  goTemplateOptions: ["missingkey=error"]
  generators:
  - git:
      repoURL: https://github.com/guilhermemaas/linuxtips-argocd.git
      revision: HEAD
      directories:
      - path: day3/apps/applicationset/apps/*/helm
      #- path: day3/apps/applicationset/apps/random-logger/helm
         #exclude: true

### Applicationset Git file:
### Applicationset Matrix (Git + Gitfile (Um config com json por exemplo e usar os valores na criacao do app))

### Applicationset Pull Request
Pode usar valores do git pull aberto para criar uma app, para por exemplo, o QA testar uma ou mais tasks antes de finalizar o merge.

https://argo-cd.readthedocs.io/en/stable/operator-manual/applicationset/Generators-Pull-Request/#template

Por exemplo, só criar ambiente quando for um PR para uma branch x ou y, e que contenha uma label, por exemplo "preview"

## Aulao EKS + Bootstrap Cluster com Argocd

### Atualizar o kubeconfig com o contexto do cluster EKS
aws eks update-kubeconfig --name cluster-aulao