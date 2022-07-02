# narvar
# Building a local cluster through minikube
 Steps are as follows: 
  First install Virtual Box
  Install minikube through
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  chmod +x minikube-linux-amd64 
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
# Install kubectl as well 
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
 
 curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
 
 echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
 
 sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
 
 minikube start --vm-driver virtualbox #Minikube will start with virtualbox 
