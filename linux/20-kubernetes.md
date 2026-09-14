# Kubernetes CLI

## kubectl

```text
| Command                                     | Description                                            |
| ------------------------------------------- | ------------------------------------------------------ |
|   kubectl version                           | Displays Kubernetes client/server version information. |
|   kubectl cluster-info                      | Displays Kubernetes cluster information.               |
|   kubectl get nodes                         | Lists Kubernetes cluster nodes.                        |
|   kubectl get pods                          | Lists pods in the current namespace.                   |
|   kubectl get pods -A                       | Lists pods across all namespaces.                      |
|   kubectl get svc                           | Lists Kubernetes Services.                             |
|   kubectl get deployments                   | Lists Deployments.                                     |
|   kubectl describe pod pod-name             | Displays detailed pod information and events.          |
|   kubectl logs pod-name                     | Displays pod/application logs.                         |
|   kubectl exec -it pod -- bash              | Opens a shell inside a pod.                            |
|   kubectl apply -f file.yaml                | Creates or updates Kubernetes resources from YAML.     |
|   kubectl delete -f file.yaml               | Deletes resources defined in YAML.                     |
|   kubectl scale deployment app --replicas=3 | Changes the number of Deployment replicas.             |
|   kubectl rollout status deployment/app     | Displays Deployment rollout status.                    |
|   kubectl rollout undo deployment/app       | Rolls back a Deployment to a previous revision.        |

```
