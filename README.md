# k8s_multi_container_app

kubectl create secret generic pgpassword --from-literal PGPASSWORD=XYZ

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml


GCP:
1) Create a service account manually. 
Role : Kubernetes Engine Admin

2) Create a new Artifact Registry Repository fibonacci-app, add Add principals to "fibonacci-app", Role Artifact Registry Writer

3) Create a cluster manually fibonacci-app-cluster



Github Secret :
GKE_SA_KEY: content of the service account key as json
PROJECT_ID



git commit --allow-empty -m "Trigger CI"
