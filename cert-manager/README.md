# Cert manager

## 参考

- [使用Let's Encrypt实现Kubernetes Ingress自动化HTTPS](https://my.oschina.net/u/2306127/blog/1929250)
- [cert-manager: Automatically provision TLS certificates in Kubernetes](https://vinta.ws/code/cert-manager-automatically-provision-tls-certificates-in-kubernetes.html)

## helm

### install

1. 测试

```shell
helm install --namespace kube-system stable/cert-manager \
             --name cert-manager \
             --set fullnameOverride=cert-manager \
             --set ingressShim.defaultIssuerName=letsencrypt-staging \
             --set ingressShim.defaultIssuerKind=ClusterIssuer
```

1. 正式

```shell
helm install --namespace kube-system stable/cert-manager \
             --name cert-manager \
             --set fullnameOverride=cert-manager \
             --set ingressShim.defaultIssuerName=letsencrypt-prod \
             --set ingressShim.defaultIssuerKind=ClusterIssuer
```

### upgrade

```shell
helm upgrade cert-manager stable/cert-manager \
             --name cert-manager \
             --set fullnameOverride=cert-manager \
             --set ingressShim.defaultIssuerName=letsencrypt-prod \
             --set ingressShim.defaultIssuerKind=ClusterIssuer
```

### delete

> helm delete --purge cert-manager

## setup

1. helm install
2. kubectl apply -f cluster-issuer.yaml
3. kubectl apply -f k8s.bb-app.cn-cert.yaml

## command

> kubectl get clusterissuers

> kubectl get certificates --all-namespaces

> kubectl describe certificate

> kubectl describe secret
