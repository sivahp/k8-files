## 🔹 What is `containerPort` in Kubernetes?

In Kubernetes, the `containerPort` specifies **which port inside the container** the application is listening on.

### ✅ Example:

```yaml
ports:
  - containerPort: 80
```

This means:

* The containerized app (e.g., NGINX) listens on port `80` **inside the container**.
* It doesn't expose the port to the outside world by itself—this is just for Kubernetes documentation and internal networking.

> 🧠 Important: **`containerPort` does not expose the application externally**. To access the app from outside the cluster, you must create a **Service**.

---

## 🔹 How to Test After Deploying the Pod

Let’s say you have deployed the Pod using your YAML file. Here’s how to test it:

---

### ✅ Step 1: Deploy the Pod

```bash
kubectl apply -f example-pod.yaml
```

---

### ✅ Step 2: Verify the Pod is Running

```bash
kubectl get pods
kubectl describe pod example-pod
```

---

### ✅ Step 3: Access the Pod (Internal Test)

You can **exec into the Pod** and test locally:

```bash
kubectl exec -it example-pod -- curl http://localhost:80
```

This tests if the NGINX server is working inside the container.

---

### ✅ Step 4: Expose the Pod to External Access

Pods are **ephemeral and not directly accessible externally**. You need to create a **Service**:

### ➤ Expose as a ClusterIP (internal only)

```bash
kubectl expose pod example-pod --port=80 --target-port=80 --name=example-service
```

### ➤ Expose as a NodePort (external access)

```bash
kubectl expose pod example-pod --type=NodePort --port=80 --target-port=80 --name=example-service
```

Then, run:

```bash
kubectl get service example-service
```

You’ll see something like:

```
example-service   NodePort   10.96.0.1   <none>   80:32123/TCP
```

You can now access it from outside the cluster:

```bash
curl http://<Node-IP>:32123
```

> Replace `<Node-IP>` with the IP address of any worker node in your cluster.

---

## 🔸 Summary

| Term             | Meaning                                    |
| ---------------- | ------------------------------------------ |
| `containerPort`  | Port app listens to inside the container   |
| `kubectl exec`   | Used to test inside the Pod                |
| `kubectl expose` | Used to create a Service to expose the Pod |

---
