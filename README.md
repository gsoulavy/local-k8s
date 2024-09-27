# Kubernetes Development Environment

This repository contains Kubernetes manifests for setting up a local development environment with various data services and monitoring using Kustomize.

## Services

The following services are included in this setup:

- MongoDB
- Redis
- Microsoft SQL Server (MSSQL)
- Azurite (Azure Storage Emulator)
- RabbitMQ
- Prometheus (Monitoring)

## Directory Structure

```
.
├── README.md
└── k8s/
    ├── kustomization.yaml
    ├── namespace/
    │   ├── data.yaml
    │   └── metrics.yaml
    ├── config/
    │   └── prometheus.yaml
    ├── storage/
    │   ├── mongo.yaml
    │   ├── redis.yaml
    │   ├── mssql.yaml
    │   ├── azurite.yaml
    │   ├── rabbitmq.yaml
    │   └── prometheus.yaml
    ├── deployment/
    │   ├── mongo.yaml
    │   ├── redis.yaml
    │   ├── mssql.yaml
    │   ├── azurite.yaml
    │   ├── rabbitmq.yaml
    │   └── prometheus.yaml
    └── service/
        ├── mongo.yaml
        ├── redis.yaml
        ├── mssql.yaml
        ├── azurite.yaml
        ├── rabbitmq.yaml
        └── prometheus.yaml
```

## Setup Instructions

1. Ensure you have a Kubernetes cluster running locally (e.g., Minikube, Docker Desktop with Kubernetes enabled).
2. Make sure you have `kubectl` installed and configured to use your local cluster.
3. Clone this repository:
   ```
   git clone https://github.com/gsoulavy/local-k8s.git
   cd local-k8s
   ```
4. Apply the Kubernetes manifests using Kustomize:
   ```
   kubectl apply -k ./k8s
   ```

## Accessing Services

After deploying the services, you can access them using the following connection details:

- MongoDB: `mongodb://admin:password@localhost:30017`
  - Username: `admin`
  - Password: `p@ssw0rd`
- Redis: `redis://localhost:30379`
- MSSQL: `Server=localhost,30433;User Id=sa;Password=P@ssw0rd;`
- Azurite:
  - Blob: `http://localhost:31000`
  - Queue: `http://localhost:31001`
  - Table: `http://localhost:31002`
- RabbitMQ:
  - AMQP: `amqp://localhost:30672`
  - Management UI: `http://localhost:31672`
  - Username: `admin`
  - Password: `p@ssw0rd`
- Prometheus:
  - Web UI: `http://localhost:30090`

Note: These services are exposed using NodePort services. Make sure your local Kubernetes cluster allows access to these NodePorts.

## Configuration

The `kustomization.yaml` file in the `k8s/` directory manages the deployment of all services. You can modify this file to add, remove, or customize services as needed.

Individual service configurations can be adjusted by modifying the respective YAML files in the service-specific directories under `k8s/`.

### Prometheus Configuration

Prometheus is configured using a ConfigMap located at `k8s/config/prometheus.yaml`. You can modify this file to adjust scraping intervals, add new targets, or customize other Prometheus settings.

## Namespaces

The services are organized into two namespaces:

- `data`: Contains all data services (MongoDB, Redis, MSSQL, Azurite, RabbitMQ)
- `metrics`: Contains the Prometheus monitoring service

## Troubleshooting

If you encounter any issues, please check the following:

1. Ensure all pods are running:
   ```
   kubectl get pods --all-namespaces
   ```
2. Check pod logs for any errors:
   ```
   kubectl logs <pod-name> -n <namespace>
   ```
3. Verify services are exposed correctly:
   ```
   kubectl get services --all-namespaces
   ```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
