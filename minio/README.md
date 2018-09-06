# Minio

- [minio](https://minio.io/)

## helm

### degbug

```shell
helm install stable/minio \
             --namespace kube-system \
             --name minio \
             --debug --dry-run
```

### install

```shell
helm install stable/minio \
             --namespace kube-system \
             --name minio
```

### delete

> helm delete minio --purge

## kubectl

```shell
kubectl apply -f pv.yaml
kubectl apply -f minio.yaml
kubectl apply -f ingress.yaml
```