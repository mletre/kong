# Kong Install in Kubernetes


## Setup

To clone and run this POC, you’ll need to have Git, Docker, [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl), [Helm](https://helm.sh) and [minikube](https://github.com/kubernetes/minikube) installed on your computer.

or

Using the GKE (Google Kubernetes Engine)

- Clone this repository
```shell
git clone https://github.com/mletre/kong.git
```

- Go into the repository folder
```shell
cd kong/install/on-k8s
```

- Make Namespace
```shell
kubectl create ns kong-dev
```

- Edit Yaml file change database host with example format app name [app-name-postgresql.app-name.svc.cluster.local], Don't forget this step is important.
```shell
--
pg_host: kong-dev-postgresql.kong-dev.svc.cluster.local
--
```

- Lets Install Using Helm 
```shell
helm install kong-dev kong/kong -n kong-dev -f kong-prov-with-db.yaml
```

- Make sure the deployment, pods, and service are run
```shell
kubectl get all -n kong-dev
```

- By Default manager cannot detect the admin api, if you want to use kong manager, you must edit the deployment and api admin env
```shell
kubectl edit deployment -n kong-dev
```

- Add kong admin api url to the env:
```shell
env:
- name: KONG_ADMIN_GUI_API_URL
  value: ip-kong-admin:8001
```
- Done


## Source

- https://docs.konghq.com/gateway/3.8.x/install/kubernetes/proxy/?install=oss
