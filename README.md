# k8s_multi_container_app

kubectl create secret generic pgpassword --from-literal PGPASSWORD=XYZ

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml



Create a cluster manually

Create a service account manually. Role : Kubernetes Engine Admin


Github Secret :
GKE_SA_KEY: content of the service account key as json