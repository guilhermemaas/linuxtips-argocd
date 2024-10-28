### Argo Events:
https://argoproj.github.io/argo-events/installation/



NAMESPACE=argo-events
kubectl proxy &
kubectl get namespace $NAMESPACE -o json |jq '.spec = {"finalizers":[]}' >temp.json
curl -k -H "Content-Type: application/json" -X PUT --data-binary @temp.json 127.0.0.1:8001/api/v1/namespaces/$NAMESPACE/finalize


### Webhook Event Source
k port-forward -n argo-events svc/webhook-eventsource-svc 12000:12000

### Sensor vai pegar o evento e fazer alguma coisa (Exemplo, criar um pod)
curl -XPOST localhost:12000/example --header "Content-Type: application/json" -d '{"ola": "mundo"}'

### Verificar o log de eventos recebidos
k logs webhook-eventsource-p5dn5-6fc498dfbc-6gfn7 -n argo-events