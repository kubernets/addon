# heapster

## images

- heapster-amd64

    ```shell
    docker pull kubernets/heapster-amd64
    docker tag docker.io/kubernets/heapster-amd64:latest k8s.gcr.io/heapster-amd64:v1.5.4
    docker rmi docker.io/kubernets/heapster-amd64:latest
    ```

- heapster-influxdb-amd64

    ```shell
    docker pull kubernets/heapster-influxdb-amd64
    docker tag docker.io/kubernets/heapster-influxdb-amd64:latest k8s.gcr.io/heapster-influxdb-amd64:v1.5.2
    docker rmi docker.io/kubernets/heapster-influxdb-amd64:latest
    ```

- heapster-grafana-amd64

    ```shell
    docker pull kubernets/heapster-grafana-amd64
    docker tag docker.io/kubernets/heapster-grafana-amd64:latest k8s.gcr.io/heapster-grafana-amd64:v5.0.4
    docker rmi docker.io/kubernets/heapster-grafana-amd64:latest
    ```

## install

    kubectl apply -f heapster.yaml

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/influxdb.yaml

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/grafana.yaml

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/rbac/heapster-rbac.yaml

## helm

### install

```shell
helm install --namespace kube-system stable/heapster \
             --name heapster \
             --set nameOverride=heapster \
             --set rbac.create=true
```

### delete

> helm delete --purge heapster