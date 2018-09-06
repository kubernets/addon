# Nginx

## helm

### install

```shell
helm install stable/nginx-ingress --name nginx-ingress --namespace kube-system \
                                  --set controller.hostNetwork=true \
                                  --set controller.kind=DaemonSet
```

### delete

> helm delete nginx-ingress --purge
