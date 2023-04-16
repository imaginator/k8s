```lang=bash
#!/bin/bash
sudo apt update
sudo apt upgrade
sudo apt install snapd -y
snap version
sudo snap install microk8s --classic
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube
su - $USER
microk8s status --wait-ready
microk8s enable dns ingress prometheus cert-manager hostpath-storage dashboard

# self signed certs
kubectl apply -f ~/Documents/src/k8s/cert-manager/clusterIssuer/yml

# other helpers
kubectl cluster-info
kubectl get all --all-namespaces
kubectl get nodes

```
