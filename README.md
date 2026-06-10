# 🔐 Kubernetes Network Policy Workload Isolation Project

## Overview

This project demonstrates Kubernetes Network Policies to isolate workloads using a Zero-Trust security model.

## Components

* Frontend Pod
* Backend Pod
* Database Pod

## Network Policies

* Default Deny Ingress
* Allow Frontend → Backend
* Allow Backend → Database

## Project Structure

```text
.
├── pods.yaml
├── default-deny.yaml
├── allow-backend-db.yaml
├── allow-frontend-backend.yaml
├── docs/
│   └── architecture.png
└── README.md
```

## Deployment

```bash
kubectl apply -f pods.yaml
kubectl apply -f default-deny.yaml
kubectl apply -f allow-backend-db.yaml
kubectl apply -f allow-frontend-backend.yaml
```

## Verification

### Allowed

* Frontend → Backend
* Backend → Database

### Blocked

* Frontend → Database
* Database → Backend

## Test Commands

```bash
kubectl exec frontend -n app -- curl http://backend-svc
kubectl exec frontend -n app -- curl --connect-timeout 5 http://db-svc
kubectl exec backend -n app -- curl http://db-svc
kubectl exec database -n app -- curl --connect-timeout 5 http://backend-svc
```

## Results

| Source   | Destination | Status    |
| -------- | ----------- | --------- |
| Frontend | Backend     | ✅ Allowed |
| Frontend | Database    | ❌ Blocked |
| Backend  | Database    | ✅ Allowed |
| Database | Backend     | ❌ Blocked |

## Technologies Used

* Kubernetes
* Network Policies
* NGINX
* kubectl

## Author

Manjunatha Lokesh
