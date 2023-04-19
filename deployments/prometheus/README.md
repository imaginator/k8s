```
kubectl create secret generic additional-scrape-configs --from-file=prometheus-additional.yaml --dry-run=client -oyaml > additional-scrape-configs.yaml
kubectl apply -f additional-scrape-configs.yaml -n observability
kubectl -n observability get secrets | grep scrape
```

edit with:
`kubectl -n observability edit prom`

and add the following three lines

```
apiVersion: monitoring.coreos.com/v1
kind: Prometheus
metadata:
  name: prometheus
spec:
  serviceAccountName: prometheus
  serviceMonitorNamespaceSelector: {}
  serviceMonitorSelector: {}
  podMonitorSelector: {}
  additionalScrapeConfigs:                    # add
    name: additional-scrape-configs           # add
    key: prometheus-additional-job.yaml       # add
  resources:
    requests:
      memory: 400Mi
  enableAdminAPI: false
```
