# narvar
# Building a local cluster through minikube
 Steps are as follows: 
  First install Virtual Box
  
   # Install minikube 
  
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  
  chmod +x minikube-linux-amd64 
  
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
  
# Install kubectl as well 
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
 
 curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
 
 echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
 
 sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
 
 minikube start --vm-driver virtualbox #Minikube will start with virtualbox 
 
 # creating our index.html file through Dockerfile
  Will update both the codes 
  
  login to docker
  # Build the image
  docker login
  
  sudo chmod 666 /var/run/docker.sock
  #Build the image
  
  docker build -t <docker-hub username>/hello-world:1.0 .
  
  docker images

Now push your docker image to dockerhub 

docker push <docker-hub username>/hello-world:1.0
# Now start the minikube 
 minikube start --vm-driver virtualbox 
# Create the deployment

kubectl create deployment hello-world --image=<docker-hub username>/hello-world:1.0

kubectl expose deployment hello-world --type=NodePort --port=80 --name=hello-world

kubectl get pods

kubectl get svc hello-world

minikube addons list

minikube addons enable metrics-server

kubectl get pod,svc -n kube-system

#Adding Cluster monitoring through helm

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

./get_helm.sh

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm install prometheus prometheus-community/prometheus

kubectl get svc prometheus-server-np

minikube service prometheus-server-np  --url

curl http://192.168.59.100:32008/metrics
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-np






