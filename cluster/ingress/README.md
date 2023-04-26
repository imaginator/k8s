```
kubectl patch daemonsets -n ingress nginx-ingress-microk8s-controller --patch-file ~/Documents/src/k8s/cluster/ingress/DaemonSet_nginx-ingress-microk8s-controller.yaml
kubectl patch configmaps -n ingress nginx-ingress-tcp-microk8s-conf  --patch-file ~/Documents/src/k8s/cluster/ingress/ConfigMap.yaml
```
