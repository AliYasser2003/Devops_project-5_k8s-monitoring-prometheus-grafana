# Devops_project-5_k8s-monitoring-prometheus-grafana
End-to-end Kubernetes monitoring setup with Prometheus and Grafana, including custom Node.js metrics, alerting rules, and real-time observability dashboards.
# 🚀 DevOps Project 5: Kubernetes Monitoring with Prometheus & Grafana

## 📌 Overview

This project demonstrates a complete **end-to-end monitoring system** for a containerized Node.js application running on Kubernetes using:

* Prometheus (metrics collection)
* Grafana (visualization)
* Alertmanager (alerting)
* Custom application metrics (Node.js)

The goal is to simulate a **real-world observability setup** with metrics, dashboards, and alerts.

---

## 🧠 Architecture

User → Node.js App (Pod) → Service → ServiceMonitor → Prometheus → Grafana / Alertmanager

---

## ⚙️ Tech Stack

* Node.js (Express)
* Docker
* Kubernetes (Minikube)
* Prometheus (kube-prometheus-stack via Helm)
* Grafana
* Alertmanager
* Prometheus Operator (ServiceMonitor)

---

## 📊 Features

### ✅ Application Metrics

* `http_requests_total` (with labels: method, route, status)
* `http_errors_total`
* `http_request_duration_seconds` (Histogram)

### ✅ Monitoring

* Prometheus scrapes metrics using ServiceMonitor
* Metrics exposed via `/metrics` endpoint

### ✅ Visualization (Grafana)

* Requests per second
* Total requests
* Error rate
* Request latency (P95)

### ✅ Alerting

* High request rate alert:

```yaml
rate(http_requests_total[1m]) > 0.1
```

---

## 📈 Key Queries

**Requests per second**

```promql
rate(http_requests_total[1m])
```

**Error rate**

```promql
rate(http_errors_total[1m])
```

**Latency (95th percentile)**

```promql
histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))
```

---

## 🔥 Load Testing

Simulate traffic:

```bash
while true; do curl http://localhost:3001; done
```

Simulate errors:

```bash
while true; do curl http://localhost:3001/error; done
```

---

## 🐳 Deployment Steps

### 1. Build Docker image

```bash
eval $(minikube docker-env)
docker build -t monitoring-app .
```

### 2. Apply Kubernetes resources

```bash
kubectl apply -f k8s/
```

### 3. Verify pods

```bash
kubectl get pods
```

---

## 📸 Screenshots

* App running (`/`)
* Metrics endpoint (`/metrics`)
* Prometheus targets (UP)
* Prometheus queries
* Grafana dashboards
* Alert firing

---

## 🎯 What I Learned

* How Prometheus scrapes metrics using ServiceMonitor
* Difference between Counter and Histogram
* How to calculate latency percentiles (P95)
* How alerting works in Prometheus
* How Kubernetes labels connect components together

---

## 🧠 Key Concepts

* **ServiceMonitor** connects Prometheus to services using labels
* **Histogram** enables latency analysis (P95, P99)
* **rate()** converts counters into real-time metrics
* **Alert rules** trigger based on PromQL queries

---

## 🚀 Future Improvements

* Add CPU/Memory alerts
* Integrate email/Slack alerts
* Add Horizontal Pod Autoscaler (HPA)
* Improve dashboard design

---

## 👤 Author

Ali Yasser
