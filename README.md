
### Architectural Diagram

![Data Pipeline](https://i.imgur.com/cutWQI5.png)


### Prerequisites

The following prerequisites are required
1. A Kubernetes Cluster
2. [Kubectl CLI](https://kubernetes.io/docs/tasks/tools/)
3. [Argo CLI](https://github.com/argoproj/argo-workflows/releases/tag/v3.4.5).


### Installation
Run the following command in your cluster to bypass the client authentication:
```
kubectl patch deployment \
  argo-server \
  --namespace argo \
  --type='json' \
  -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/args", "value": [
  "server",
  "--auth-mode=server"
]}]'
```

Make the UI accessible on your web browser

```
kubectl -n argo port-forward deployment/argo-server 2746:2746
```

Clone the repo and run the following command to execute the data pipeline

```
argo submit -n argo --watch data-pipeline.yaml
```

View the Workflow
```
https://localhost:2746
```