# Test_Helm_Chart
Test task goals:
- create namespace "unitest" with Prometheus, BlackBox exporter and Grafana
- BlackBox exporter aimed on "google.com"
- Grafana with [dashboard](https://grafana.com/grafana/dashboards/13659-blackbox-exporter-http-prober/) 
- Grafana admin panel with password "unitest123"
## Dependencies

By default this chart installs additional, dependent charts:

- [grafana](https://github.com/grafana/helm-charts/tree/main/charts/grafana)
- [prometheus-blackbox-exporter](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-blackbox-exporter)
- [kube-state-metrics](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-state-metrics) installed as a part of prometheus chart
- [prometheus](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus)

To disable the dependency during installation, set `prometheus.kubeStateMetrics.enabled` to `false`.

_See [helm dependency](https://helm.sh/docs/helm/helm_dependency/) for command documentation._


## Install chart
Clone current repository 
```
cd Test_Helm_Chart
helm install app . -n unitest --create-namespace
```
Realese name "app" required because it is locked as a part of Prometheus datasource url in Grafana.
## Access to Grafana dashboard
You should forward grafana endpoint to localhost:
```
kubectl port-forward svc/app-grafana 3000:80
```
Default credential:
```
username: admin
password: unitest123
```
## Upgrade chart
```
helm upgrade app . -n unitest
```
## Uninstall chart
```
helm uninstall app
```

