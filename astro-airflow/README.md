# Astro helm airflow
- https://github.com/astronomer/airflow-chart

### Quick start
```bash
kubectl create namespace airflow

helm repo add astronomer https://helm.astronomer.io
helm install airflow --namespace airflow2 astronomer/airflow

# change kubectl namespace to "airflow2"
kubectl config set-context --current --namespace=airflow2
# validate 
kubectl config view --minify | grep namespace:
# get services under namespace = airflow2
kubectl get namespace
kubectl get pods

# run the airflow web server
kubectl port-forward svc/airflow-webserver 8080:8080
```