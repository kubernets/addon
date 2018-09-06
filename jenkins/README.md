# Jenkins

- [Official Jenkins Docker image](https://github.com/jenkinsci/docker/blob/master/README.md)

## Helm

### install

```shell
helm install stable/jenkins --name jenkins --namespace kube-system
```

### delete

> helm delete jenkins --purge