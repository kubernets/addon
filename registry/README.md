# Registry

## degbug

```shell
helm install stable/docker-registry \
             --namespace kube-system \
             --name docker-registry \
             --debug --dry-run
```

## install

```shell
helm install stable/docker-registry \
             --namespace kube-system \
             --name docker-registry
```

### delete

> helm delete docker-registry --purge

## 自定义证书

> openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=docker.bb-app.cn"
> kubectl -n kube-system create secret tls docker.bb-app.cn --key=tls.key --cert=tls.crt  