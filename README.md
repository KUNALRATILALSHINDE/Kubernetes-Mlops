# Kubernetes-MLOps 🚀

> Working on Kubernetes deployment in the MLOps journey.

---

## 📚 Steps to Execute the Project

---

### 1. Build the Application

- Create or use an existing ML/AI-based application.
- Test it **locally** to ensure it behaves as expected.

Example:

```bash
python app.py
```

---

### 2. Prepare and Build the Docker Image

- Create a `Dockerfile` in your project directory.
- Build the Docker image:

```bash
docker build -t kubernetes-test-app:latest .
```

- Verify if the image was created:

```bash
docker images
```

- Run and test the Docker container locally:

```bash
docker run -p 5000:5000 kubernetes-test-app:latest
```

Visit `http://localhost:5000` to check if it’s working.

---

### 3. Create the Deployment YAML

- Define a **Kubernetes Deployment** and **Service** inside `deployment.yaml`.

Basic commands to apply it:

```bash
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get services
```

---

### 4. Install Minikube

- Visit the [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/).
- Download `.exe` file and install via **PowerShell** (Run as Administrator).
- After installation, **restart your terminal** (or your system if needed).

Start Minikube:

```bash
minikube start
# OR with embedded certificates
minikube start --embed-certs
```

---

### 5. Troubleshooting Minikube

**Common Error:**
> Failing to connect to `https://registry.k8s.io/`

**Solutions:**

- If behind a proxy, configure environment variables:

```bash
minikube start --docker-env HTTP_PROXY=http://your-proxy:port --docker-env HTTPS_PROXY=https://your-proxy:port
```

- If no proxy:

```bash
unset HTTP_PROXY
unset HTTPS_PROXY
unset NO_PROXY
```

- Test DNS resolution:

```bash
nslookup registry.k8s.io
```

- If issues persist:

```bash
minikube stop
minikube delete --all
minikube start
```

---

### 6. Verify Minikube and Kubernetes Status

- Check Minikube status:

```bash
minikube status
```

- Check Kubernetes resources:

```bash
kubectl get all -A
kubectl get pods -A
kubectl get nodes -A
```

- Check your cluster info:

```bash
kubectl cluster-info
```

---

### 7. Adding Nodes (Multi-Node Minikube Cluster)

```bash
minikube start --nodes=2
# or
minikube start --nodes=2 --embed-certs
```

Check the nodes:

```bash
kubectl get nodes
```

---

### 8. Load Docker Image to Minikube

- Check available images:

```bash
minikube image list
docker images
```

- Load your Docker image into Minikube:

```bash
minikube image load kubernetes-test-app:latest
```

- Double check if your image is loaded:

```bash
minikube image list
```

---

### 9. Deploy and Expose the Application

Apply your deployment:

```bash
kubectl apply -f deployment.yaml
```

Expose the service (if not already done in YAML):

```bash
kubectl expose deployment kubernetes-test-app --type=NodePort --port=8080
```

Access the service:

```bash
minikube service kubernetes-test-app
```

---

## 🛠️ Useful Kubectl Commands

| Command | Description |
|:---|:---|
| `kubectl get pods` | List all pods |
| `kubectl describe pod <pod-name>` | Show detailed pod info |
| `kubectl logs <pod-name>` | View logs for a pod |
| `kubectl delete pod <pod-name>` | Delete a specific pod |
| `kubectl get svc` | List services |
| `kubectl get nodes` | List nodes in the cluster |
| `kubectl apply -f <file>` | Apply configuration from a file |
| `kubectl delete -f <file>` | Delete resources specified in a file |
| `kubectl port-forward <pod-name> <local-port>:<pod-port>` | Forward a port from a pod to your local machine |

---
