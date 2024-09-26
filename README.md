# local-k8s
local k8s

## Deploying to Kubernetes

To deploy the application to your Kubernetes cluster, use the following command:

```bash
kubectl apply -k k8s
```

This command will apply the configuration in the `k8s` directory, which includes the namespace, deployment, service, and ingress resources.
