# prometheus-e-grafana

usando helm para instalar
https://helm.sh/docs/intro/install/


```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```


para instalar o prometheus:
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update


para pegar os parametros quepodem ser usadpos na instalação do prometheus:

helm show values prometheus-community/prometheus > prometheus/values-prometheus.yaml

--- para atualizar e instalar use:
helm upgrade --install prometheus prometheus-community/prometheus --set alertmanager.enabled=false,server.p
ersistentVolume.enabled=false,server.service.type=LoadBalancer,server.global.scrape_interval=10s,pushgateway.en
abled=false


para o prometheus pegar as metricas dos pods, deve-se fazer a alteração a seguir no manifesto, incluindo as annottions

```
  template:
    metadata:
      labels:
        app: kubenews
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/prot: "8080"
        prometheus.io/path: "/metrics"
    spec:
```

utilizando o promql para consultar as metricas:


ele trabalha consuiltando uma metrica definida com filtros tambem.

https://prometheus.io/docs/prometheus/latest/querying/examples/

http_requests_total{method="POST|PUT"}
http_requests_total[1m]

rate(http_requests_total[5m]) #media
sum(rate(http_requests_total[5m]))
sum(rate(http_requests_total[5m])) by (method)

# USANDO O GRAFANA INTEGRADO COM O PROMETHEUS

https://grafana.com/



https://artifacthub.io/packages/helm/grafana/grafana
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update


helm show values grafana/grafana > grafana/values-grafana.yaml

--- para atualizar e instalar use:
helm upgrade --install grafana grafana/grafana --set service.type=LoadBalancer

para pegar a senha do adm

1. Get your 'admin' user password by running:

   kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

a saida será como o exemplo:
```
bI64SeXqBFgiL11V8x5F3gtWwRNh5C2mgBb1L0Yl
```

crie um datasouce para o prometheus:

nome do service do prometheus
URL:http://prometheus-server

criando um dash
sum(rate(http_requests_total{path!="/metrics"}[5m])) by (app, method, path)

importando um dash

https://grafana.com/grafana/dashboards/
coloque o tipo de dash que voce quer , copie o ID e no grafana faça a importação.










