# Minikube Nginx Deployment (Kubernetes Local Cluster)

This project demonstrates how to deploy the official **nginx** web server on a local Kubernetes cluster using **Minikube**, manage it with **kubectl**, and access it from your browser.

---

## **Prerequisites**
Make sure you have installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Git](https://git-scm.com/)

---

## **Steps to Run**

### 1️⃣ Open Terminal 
---
### 2️⃣ Start Minikube
```bash
minikube start --driver=docker

This creates a single-node Kubernetes cluster locally.
3️⃣ Create Deployment & Service Files

deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:stable
          ports:
            - containerPort: 80

service.yaml

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP

4️⃣ Deploy to Kubernetes

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

5️⃣ Verify Deployment

kubectl get pods
kubectl get svc

6️⃣ Access the App

minikube service nginx-service

    On Windows/macOS: nginx welcome page opens in browser.

    On Linux: copy the URL from terminal and paste into browser.

7️⃣ Scale the Deployment

kubectl scale deployment nginx-deployment --replicas=3
kubectl get pods

8️⃣ Describe a Pod & View Logs

kubectl describe pod <pod-name>
kubectl logs deployment/nginx-deployment

9️⃣ Kubernetes Dashboard (Optional)

minikube dashboard

Opens the Kubernetes UI in your browser.
