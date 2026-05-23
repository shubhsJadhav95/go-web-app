# Go Web Application

This is a simple website written in Golang. It uses the `net/http` package to serve HTTP requests.

## Running the server

To run the server, execute the following command:

```bash
go run main.go
```

The server will start on port 8080. You can access it by navigating to `http://localhost:8080/courses` in your web browser.

## Looks like this

![Website](static/images/golang-website.png)

## Docker Configuration

docker build -t shubhsjadhav95/go-webapp:v1 .

docker run -d -p 8080:8080 --name go-webapp shubhsjadhav95/go-webapp:

docker push shubhsjadhav95/go-webapp:v1

## K8s configurations

### Check k8s connection
kubectl config current-context

### Create an EKS cconnection
aws eks update-kubeconfig --region us-east-1 --name <your-aws-cluster-name>

### Deploy Pods

kubectl apply -f k8s/manifest/deployment.yaml
kubectl apply -f k8s/manifest/service.yaml
kubectl apply -f k8s/manifest/ingress.yaml

### Update service type

kubectl edit svc go-webapp

type: NodePort / LoadBalancer

### Create an External Address 

eksctl create nodegroup \
  --cluster demo-cluster \
  --region us-east-1 \
  --name demo-nodes \
  --node-type t3.micro \
  --nodes 2

### connect k8s

kubectl get svc go-webapp //Get Port
kubectl get nodes -o wide //Get External IP

http://<External IP>:<Port>

SG inbond rule add TCP PORT

### Install Nginx Controller

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml

kubectl get pods -n ingress-nginx


## HELM

helm create go-webapp-chart

cd go-webapp-chart/template

cp ../../../k8s/maifest/* 

helm install go-webapp ./go-webapp-chart

## Github Action

mkdir .github/workflow/ci.yaml