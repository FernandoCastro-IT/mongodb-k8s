# Deploying MongoDB on Kubernetes with Minikube

This repository contains configuration files and steps to deploy MongoDB on a local Kubernetes cluster using Minikube.

## 🛠 Prerequisites

- [Minikube](https://minikube.sigs.k8s.io/docs/start/) installed and configured
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed

## 🚀 Getting Started

### 1. Start Minikube
```bash
minikube start --cpus=2 --memory=4g
```

### 2. Create a PersistentVolumeClaim (PVC)
Apply the `mongodb-pvc.yaml` file:
```bash
kubectl apply -f mongodb-pvc.yaml
```

### 3. Deploy MongoDB using StatefulSet
Apply the `mongodb-statefulset.yaml` file:
```bash
kubectl apply -f mongodb-statefulset.yaml
```

### 4. Create a Headless Service
Apply the `mongodb-service.yaml` file:
```bash
kubectl apply -f mongodb-service.yaml
```

### 5. Verify Deployment
Check the status of your MongoDB deployment:
```bash
kubectl get statefulsets mongodb
kubectl get pods -l app=mongodb
kubectl get services mongodb
kubectl get pvc
```

## 🧩 Connect using MongoDB Compass

### 1. Download MongoDB Compass
Download and install MongoDB Compass from: [https://www.mongodb.com/try/download/compass](https://www.mongodb.com/try/download/compass)

### 2. Port Forward to Localhost
Expose MongoDB running in the cluster to your local machine:
```bash
kubectl port-forward svc/mongodb 27017:27017
```
This will make MongoDB accessible at `localhost:27017`.

### 3. Connect with Compass
- Open MongoDB Compass
- In the connection string field, use:
  ```
  mongodb://localhost:27017
  ```
- Click **Connect**

You should now see your MongoDB instance running in Minikube.

## 📦 Files Included

- `mongodb-pvc.yaml` - Persistent Volume Claim for MongoDB data
- `mongodb-statefulset.yaml` - StatefulSet configuration to manage MongoDB pod
- `mongodb-service.yaml` - Headless Service for stable networking

## 🛡 Best Practices

- Allocate enough resources when starting Minikube
- Monitor and manage storage through PVCs
- Implement security measures for production deployments
- Set up regular backups and restoration mechanisms

## ✅ Conclusion

This setup provides a simple and effective way to deploy MongoDB on Minikube for development and testing purposes.

Feel free to contribute or open issues for improvements!
