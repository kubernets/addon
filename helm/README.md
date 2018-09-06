# Helm

- [Installing Helm](https://docs.helm.sh/using_helm/#installing-helm)
- [利用 Helm 简化应用部署](https://help.aliyun.com/document_detail/58587.html)

## install

```shell
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```

## images

- tiller

    ```shell
    docker pull kubernets/tiller:v2.10.0
    docker tag docker.io/kubernets/tiller:v2.10.0 gcr.io/kubernetes-helm/tiller:v2.10.0
    docker rmi docker.io/kubernets/tiller:v2.10.0
    ```

## setup

> helm init
> kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default

```shell
helm init --client-only --stable-repo-url https://aliacs-app-catalog.oss-cn-hangzhou.aliyuncs.com/charts/
helm repo add incubator https://aliacs-app-catalog.oss-cn-hangzhou.aliyuncs.com/charts-incubator/
helm repo update
```

## upgrade

> helm init --upgrade