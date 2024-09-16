# Kong LUA Plugin Install in Kubernetes


## Setup

In here we want to add some plugin in kubernetes using configmap

- Clone this repository
```shell
git clone https://github.com/mletre/kong.git
```

- Change Directory
```shell
cd kong/plugin-install
```

- Change Directory
```shell
kubectl create configmap my-custom-plugin --from-file=my-custom-plugin -n kong-dev
```

- Edit Kong Kubernetes Deployment for add the plugin
```shell
kubectl edit deployments -n kong-dev
```

- First Add the variable
![Alt text](./img/variable.jpeg?raw=true "Title")

- First Add the variable
![Alt text](./img/configmap.jpeg?raw=true "Title")

- First Add the variable
![Alt text](./img/mountpoint.jpeg?raw=true "Title")

- After this save the configuration and make new revision deployment
```shell
:wq
```

- Done