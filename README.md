# DEVOPS Project: Multi Docker Containers On Kubernetes With GCP and GitHub Actions

## Goal
Deploy an over the top complicated - 4 containers + 1 Relational Database + 1 in-memory Cache - Fibonacci calculator into a staging environment in a public cloud using Kubernetes and a CI/CD pipeline (**manual actions required prior**).

Stack:

* Cloud Platform: GCP
* Code Hosting Platform: GitHub
* CI/CD Tool: GitHub Actions
* Container Build Tool: Docker
* Container Registry: Docker Hub
* Staging Environment: Google Kubernetes Engine

## Local Deployment

![Local Deployment](/misc/local_deployment.jpg)

### Prerequisites
* Create a secret for the Postgres database
`kubectl create secret generic pgpassword --from-literal PGPASSWORD=XYZ`

* Deploy the application K8S resources

`kubectl apply -f k8s`

* Deploy the ingress-nginx K8S resource

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml`

* (optional) Deploy the dashboard K8S resource

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml`

`kubectl apply -f k8s-dashboard`

`kubectl proxy`

Visit the following URL in your browser to access your Dashboard:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

Obtain the token for this user by running the following in your terminal:
`kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"`

## GCP Deployment

![GCP Deployment](/misc/gcp_deployment.jpg)


![GKE Dashboard](/misc/gke_dashboard.jpg)

### Prerequisites
1) GCP: Create a service account "github-actions-deployer" with "Kubernetes Engine Admin" role

2) GCP: Create a GKE cluster "fibonacci-app" in "northamerica-northeast1-a" zone

3) GCP: Connect to the cluster via Cloud Shell

* Get the GKE credentials

`gcloud container clusters get-credentials fibonacci-app --zone northamerica-northeast1-a`

* Create a secret for the Postgres database
`kubectl create secret generic pgpassword --from-literal PGPASSWORD=XYZ`

* Install Helm
`curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3`

`chmod 700 get_helm.sh`

`./get_helm.sh`

* Install Ingress-Nginx via Helm

`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`

`helm install my-release ingress-nginx/ingress-nginx`

4) GitHub: Create the following secrets
* SA_KEY: content of the service account - created at step #1 - key as json
* PROJECT_ID
* DOCKERHUB_USERNAME
* DOCKERHUB_TOKEN

## Misc
`git commit --allow-empty -m "Trigger CI"`
