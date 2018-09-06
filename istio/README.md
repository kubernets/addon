# Istio

- [Kubernetes](https://istio.io/zh/docs/setup/kubernetes/)

## get

> curl -L https://git.io/getLatestIstio | sh -

## helm

### install

```shell
helm install install/kubernetes/helm/istio \
                --name istio \
                --namespace istio-system \
                --set tracing.enabled=true
```

### delete

> helm delete --purge istio
