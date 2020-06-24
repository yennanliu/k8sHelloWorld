# k8sHelloWorld


### Quick start
```bash
### airflow - k8s ###

# step 1) install airflow source code
minikube start --memory='4g' --kubernetes-version=v1.14.10
cd minikube-airflow
git clone https://github.com/apache/airflow.git
git checkout c8597cbf143b970ad3c7b0d62e3b44d1dfdc8afe # make Airflow in verison=1.10.7

# step 2) update Update Build Script : scripts/ci/kubernetes/docker/build.sh
# -> comment "kind load docker-image "${IMAGE}:${TAG}""

# step 3) export env variable
### run the docker server first
eval $(minikube docker-env)

# step 4) build image 
export AIRFLOW_CONTAINER_DOCKER_IMAGE=apache/airflow:v1-10-test-python3.5-ci
./scripts/ci/kubernetes/docker/build.sh

# step 5) deploy airflow 
./scripts/ci/kubernetes/app/deploy_app.sh -d git_mode

# step 6) check airflow pods
kubectl get pods

# step 7) open airflow web server
minikube service airflow 

```

```bash
### azure vote app ###

### prerequisite 
# 1) install az (Azure CLI)
# 2) az auth (k8s)
az aks get-credentials --resource-group <your_resource_group> --name <your_k8s_cluster_name>
az aks browse --resource-group <your_resource_group> --name <your_k8s_cluster_name>

# https://docs.microsoft.com/zh-tw/azure/aks/kubernetes-walkthrough
kubectl apply -f azure-vote-all-in-one-redis.yaml
# get k8s status 
kubectl get service azure-vote-front --watch
```

### Ref 
- Airflow
	- https://gist.github.com/kppullin/54d07f557c7c64c321786d6ed40b46e1
	- https://github.com/Sureya/airflow_k8s_executor/
	- https://www.coderbridge.com/@FrankYang0529/aecbf64852184efc8674d47bebe823aa
	- https://www.techatbloomberg.com/blog/airflow-on-kubernetes/
	- https://docs.bitnami.com/tutorials/deploy-apache-airflow-kubernetes-helm/