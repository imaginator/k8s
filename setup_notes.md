``` lang=bash
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

# now setup Kubernetes
alias kubectl='microk8s kubectl'
kubectl cluster-info
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl get all --all-namespaces
kubectl get nodes
# expose dashboard
kubectl --namespace kubernetes-dashboard patch svc kubernetes-dashboard -p '{"spec": {"type": "NodePort"}}'

```