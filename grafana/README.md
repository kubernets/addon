# Grafana

## helm

### install

```shell
helm install --namespace kube-system stable/grafana \
             --name grafana \
             --set image.tag=5.2.3 \
             --set fullnameOverride=grafana \
             --set rbac.create=true \
             --set sidecar.dashboards.enabled=true \
             --set sidecar.datasources.label=true \
             --set sidecar.datasources.enabled=true
             --dry-run --debug

```

### delete

> helm delete --purge grafana


## help

1. password

> kubectl get secret --namespace kube-system grafana-grafana -o jsonpath="{.data.grafana-admin-password}" | base64 --decode ; echo