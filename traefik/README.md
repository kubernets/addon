# Traefik

## apply

```shell
kubectl apply -f https://raw.githubusercontent.com/containous/traefik/master/examples/k8s/traefik-rbac.yaml

kubectl apply -f https://raw.githubusercontent.com/containous/traefik/master/examples/k8s/traefik-ds.yaml

kubectl apply -f ui.yaml
```

## helm

### install

```shell
helm install stable/traefik --name traefik --namespace kube-system --values values.yaml
```

### delete

> helm delete traefik --purge

## 证书

### 自定义证书

> openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=k8s.bb-app.cn"
> kubectl -n kube-system create secret tls k8s.bb-app.cn --key=tls.key --cert=tls.crt

### 安装证书

```shell
kubectl apply -f k8s.bb-app.cn-cert.yaml
```