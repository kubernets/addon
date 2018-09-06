# Spinnaker

- [spinnaker-halyard](https://github.com/kubernets/spinnaker-halyard)

## Halyard安装

### **1. [安装Halyard](https://www.spinnaker.io/setup/install/halyard/)**

- Halyard with docker

    1. install Halyard

        ```shell
        wget https://github.com/kubernets/spinnaker-halyard/raw/master/get-spinnaker-halyard-image.sh

        bash get-spinnaker-halyard-image.sh

        mkdir ~/.hal

        docker run -p 8084:8084 -p 9000:9000 \
                                --name halyard --rm \
                                -v ~/.hal:/home/spinnaker/.hal \
                                -v ~/.kube:/home/spinnaker/.kube \
                                -it gcr.io/spinnaker-marketplace/halyard:1.9.1-20180830145737
        ```

    2. connect to Halyard

        > docker exec -it halyard bash

    3. remove

        > docker rm halyard

- Halyard with os

    1. install Halyard

        ```shell
        curl -O https://raw.githubusercontent.com/spinnaker/halyard/master/install/debian/InstallHalyard.sh

        sudo bash InstallHalyard.sh
        ```

    2. remove

        ```shell
        hal deploy clean
        sudo ~/.hal/uninstall.sh
        ```

- **注意**

    1. 在国内要使用代理，修改halyard运行文件的DEFAULT_JVM_OPTS配置

        ```java
        DEFAULT_JVM_OPTS='"-Djava.security.egd=file:/dev/./urandom" "-Dspring.config.location=/opt/spinnaker/config/" "-Dhttps.proxyHost=127.0.0.1" "-Dhttp.proxyHost=127.0.0.1" "-Dhttp.proxyPort=8118" "-Dhttps.proxyPort=8118"'
        ```

### **2. [选择云服务](https://www.spinnaker.io/setup/install/providers/)**

- [Kubernetes(legacy provider)](https://www.spinnaker.io/setup/install/providers/kubernetes/)

    1. 配置Kubernetes角色

        > kubectl create ns spinnaker

        > kubectl apply -f rbac.yaml

    2. 配置Docker Registry

        ```shell
        export ADDRESS=docker.bb-app.cn
        export REPOSITORIES=
        export USERNAME=spinnaker
        export PASSWORD=535251

        hal config provider docker-registry enable

        echo $PASSWORD | hal config provider docker-registry account add docker-registry \
            --address $ADDRESS \
            --repositories $REPOSITORIES \
            --username $USERNAME \
            --password

        ```

    3. 启用了提供程序

        > hal config provider kubernetes enable

    4. 添加帐户

        ```shell
        hal config provider kubernetes account add k8s-account \
            --docker-registries docker-registry
        ```

- [Kubernetes(Manifest Based)](https://www.spinnaker.io/setup/install/providers/kubernetes-v2/)

    1. 配置Kubernetes角色

        > kubectl create ns spinnaker

        > kubectl apply -f rbac.yaml

    2. 启用了提供程序

        > hal config provider kubernetes enable

    3. 添加帐户

        ```shell
        hal config provider kubernetes account add k8s-v2-account \
            --provider-version v2 \
            --context $(kubectl config current-context)

        hal config features edit --artifacts true
        ```

### **3. [选择云环境](https://www.spinnaker.io/setup/install/environment/)**

- [分布式安装](https://www.spinnaker.io/setup/install/environment/#distributed-installation)

  > hal config deploy edit --type distributed --account-name k8s-v2-account

### **4. [选择存储服务](https://www.spinnaker.io/setup/install/storage/)**

1. [Minio](https://www.spinnaker.io/setup/install/storage/minio/)

    ```shell
    export ENDPOINT=http://minio-service.kube-system.svc:9000
    export MINIO_ACCESS_KEY=HL21ZEKVAFDD6DK9Q5O3
    export MINIO_SECRET_KEY=Lc6lHSayTTqjTQC2d5LCWgKgThCmL1sfNduFsOF3

    echo $MINIO_SECRET_KEY | hal config storage s3 edit --endpoint $ENDPOINT \
        --access-key-id $MINIO_ACCESS_KEY \
        --secret-access-key

    hal config storage edit --type s3
    ```

### **5. [部署和连接](https://www.spinnaker.io/setup/install/deploy/)**

1. 选择一个版本

    > hal version list

2. 设置要使用的版本

    > hal config version edit --version $VERSION

3. 部署

    > hal deploy apply

4. 连接到Spinnaker UI

    > hal deploy connect

    > http://localhost:9000

### **6. 清除安装**

    > hal deploy clean

### **7. [部署CI](https://www.spinnaker.io/setup/ci/)**

- [Wercker](https://www.spinnaker.io/setup/ci/wercker/)

    ```shell
    hal config ci wercker enable
    hal config features edit --wercker true
    echo cc9c45c59ca4e0005668bf4fd8e9662830e98bd474fa111c567b8ac703016495 | hal config ci wercker master add wercker-obe \
        --address https://app.wercker.com \
        --user galaxyobe \
        --token

    hal deploy apply
    ```