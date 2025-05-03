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
