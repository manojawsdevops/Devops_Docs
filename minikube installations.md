curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo -E minikube start --driver=none
minikube start --vm-driver=none
sudo apt install conntrack
minikube start

