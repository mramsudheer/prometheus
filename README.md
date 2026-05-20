# Prometheus Stack Setup on EKS


## Installation Steps


### Step 1 — Add Helm repo
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

### Step 2 — Install kube-prometheus-stack
```bash
helm upgrade --install prometheus-stack prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --create-namespace \
  --set grafana.service.type=LoadBalancer \
  --set grafana.adminPassword=admin123 \
  --set prometheus.prometheusSpec.retention=7d
```

### Step 3 — Verify pods are running
```bash
kubectl get pods -n monitoring
```

### Step 4 — Get Grafana URL
```bash
kubectl get svc prometheus-stack-grafana -n monitoring
# Use the EXTERNAL-IP (Classic ELB DNS name)
```

### Step 5 — Login to Grafana
- URL: `http://<EXTERNAL-IP>`
- Username: `admin`
- Password: `admin123`

---