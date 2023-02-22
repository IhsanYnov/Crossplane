# Crossplane
Nous commencons par l'installation de Docker sur notre machine debian 
DOCKER 
 > sudo apt-get update
 > sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
    
> sudo mkdir -m 0755 -p /etc/apt/keyrings
> curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

> echo \
   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
  > sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  > sudo docker run hello-world
  
Une fois Docker installé nous installons ensuite minikube.
  
  MINIKUBE
  > curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  > sudo install minikube-linux-amd64 /usr/local/bin/minikube
 On le lance 
  > minikube start
 Et on vérifie qu'il s'est bien lancé.
  > minikube kubectl cluster-info
 On installe Crossplane
  > minikube kubectl -- create namespace crossplane-system
  > helm repo add crossplane-stable https://charts.crossplane.io/stable
  > helm install crossplane --namespace crossplane-system crossplane-stable/crossplane --version 1.4.0
  > minikube kubectl -- get pods --namespace crossplane-system
 On créer un CRD pour crosplane ou sera créer la ressource "maressource.mongroupe.example.com"
  > minikube kubectl -- apply -f mycustomresource-crd.yaml
 On verifie que le CRD a bien été créer 
  > minikube kubectl -- get crd

