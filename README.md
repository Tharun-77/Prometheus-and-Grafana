# Prometheus-and-Grafana
We are going to learn about prometheus and grafana using helm charts in the kind k8s cluster

---
# Introduction
Prometheus is a time series database and open-source monitoring system that focuses on collecting and storing metrics, while Grafana is a data visualization and monitoring tool that can connect to Prometheus to create dashboards and explore data. They are commonly used together, with Prometheus handling data collection and storage and Grafana providing the visualization and analysis capabilities. 

---
# Helm Installation Guide (Linux, Windows, macOS)

Helm is the package manager for Kubernetes. It helps you define, install, and manage Kubernetes applications using Helm charts.

---

## Install Helm on Ubuntu (Linux)

### Step 1: Download and run the install script
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

### Step 2: Verify Installation
```bash
helm version
```

Expected output: `version.BuildInfo{Version:"v3.x.x", ...}`

---

## Install Helm on Windows

### Option 1: Using Chocolatey
```powershell
choco install kubernetes-helm
```

### Option 2: Manual Installation
1. Download the latest Windows release from:  
   https://github.com/helm/helm/releases

2. Extract the zip file.

3. Move `helm.exe` to a directory in your `PATH`.

4. Verify installation:
```powershell
helm version
```

---

## Install Helm on macOS

### Option 1: Using Homebrew (recommended)
```bash
brew install helm
```

### Option 2: Using the install script
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

### Verify Installation
```bash
helm version
```

---

## Basic Helm Usage

### Add a Chart Repository
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

### Install a Chart (Example: nginx)
```bash
helm install my-nginx bitnami/nginx
```

### List Installed Releases
```bash
helm list
```

### Uninstall a Release
```bash
helm uninstall my-nginx
```

---

## Uninstall Helm

### Ubuntu/macOS
```bash
sudo rm /usr/local/bin/helm
```

### Windows
Delete `helm.exe` from your system's PATH directory.

---

## Resources

- Helm Documentation: https://helm.sh/docs/
- Helm GitHub Releases: https://github.com/helm/helm/releases
- Artifact Hub for Charts: https://artifacthub.io/

# Installing Prometheus and Grafana using Helm

This guide shows how to deploy Prometheus and Grafana on Kubernetes using Helm charts from the Bitnami repository.

---

## Prerequisites

- A running Kubernetes cluster
- `kubectl` configured to access your cluster
- Helm installed (`helm version`)

---

## Step 1: Add the Bitnami Helm repository

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

---

## Step 2: Create a namespace (optional but recommended)

```bash
kubectl create namespace monitoring
```

---

## Step 3: Install Prometheus

```bash
helm install prometheus bitnami/kube-prometheus \
  --namespace monitoring
```

This installs:
- Prometheus
- Alertmanager
- Node Exporter
- Kube State Metrics
- Prometheus Operator

---

## Step 4: Install Grafana

```bash
helm install grafana bitnami/grafana \
  --namespace monitoring \
  --set adminPassword='admin123' \
  --set service.type=NodePort
```

Change `'admin123'` to a secure password.

---

## Step 5: Access Grafana Dashboard

### Get the Grafana service URL:
```bash
kubectl get svc --namespace monitoring grafana
```

If using `NodePort`, access it via:
```
http://<NodeIP>:<NodePort>
```

Or use port forwarding:
```bash
kubectl port-forward --namespace monitoring svc/grafana 3000:3000
```
Then access it at:
```
http://localhost:3000
```

Login with:
- **Username:** `admin`
- **Password:** `admin123` (or the password you set)

---

## Step 6: Add Prometheus as a Grafana Data Source

1. Go to Grafana UI → Gear icon → Data Sources.
2. Add a new data source → Choose "Prometheus".
3. Enter URL: `http://prometheus-kube-prometheus-prometheus.monitoring.svc.cluster.local`
4. Save & Test.

---

## Optional: Uninstall Everything

```bash
helm uninstall prometheus --namespace monitoring
helm uninstall grafana --namespace monitoring
kubectl delete namespace monitoring
```

---

## References

- Bitnami Prometheus Chart: https://bitnami.com/stack/kube-prometheus/helm
- Bitnami Grafana Chart: https://bitnami.com/stack/grafana/helm
- Grafana Docs: https://grafana.com/docs/
- Prometheus Docs: https://prometheus.io/docs/

