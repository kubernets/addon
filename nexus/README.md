# Nexus

- [nexus repository oss](https://www.sonatype.com/nexus-repository-oss)
- [Changing the Context Path](https://help.sonatype.com/repomanager3/installation/configuring-the-runtime-environment#ConfiguringtheRuntimeEnvironment-ChangingtheContextPath)

- [使用nexus3.x配置docker镜像仓库及仓库代理](https://segmentfault.com/a/1190000015629878)

## Helm

## degbug

```shell
helm install stable/sonatype-nexus \
             --namespace kube-system \
             --name sonatype-nexus \
             --debug --dry-run
```

## install

```shell
helm install stable/sonatype-nexus \
             --namespace kube-system \
             --name sonatype-nexus \
             --set fullnameOverride=sonatype-nexus
```

### delete

> helm delete sonatype-nexus --purge


## Settings

### Changing the Context Path

```yaml
"env": [
    {
        "name": "CONTEXT_PATH",
        "value": "nexus/"
    }
],
```