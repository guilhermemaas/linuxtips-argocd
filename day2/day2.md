### Application
É o link entre o cluster e o repositório git.

### App of Apps
E uma maneira de agrupar apps, por exemplo, uma stack de observabilidade.

### Prunelast
    syncOptions:
    - CreateNamespace=true
    - PruneLast=true

Vai executar um Sync + Prune pros objetos que nao precisam mais existir segundo o que esta no repo git.