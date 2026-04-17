# DevOps Project 5: Kubernetes Monitoring with Prometheus & Grafana
**********************************************************************
This project demonstrates a complete end-to-end Kubernetes monitoring setup with Prometheus and Grafana,
including custom Node.js metrics, alerting rules, and real-time observability dashboards.

* The goal is to simulate a real-world observability setup with metrics, dashboards, and alerts.


## Architecture
******************
User ---> Node.js App (Pod) ---> Service ---> ServiceMonitor ---> Prometheus ---> Grafana / Alertmanager


## Technical Stack
*********************
- Node.js
- Docker
- Kubernetes
- Prometheus (kube-prometheus-stack via Helm)
- Grafana
- Alertmanager
- Prometheus Operator (ServiceMonitor)



## Features
**************

##### Application Metrics
- `http_requests_total` (with labels: method, route, status)
- `http_errors_total`
- `http_request_duration_seconds` (Histogram)

##### Monitoring
- Prometheus scrapes metrics using ServiceMonitor
- Metrics exposed via `/metrics` endpoint

##### Visualization (Grafana)
- Requests per second
- Total requests
- Error rate
- Request latency (P95)

##### Alerting
- High request rate alert:
PromQL --> `rate(http_requests_total[1m]) > 0.1`



## Key Queries
*****************

- Requests per second:
PromQL --> `rate(http_requests_total[1m])`

- Error rate:
PromQL --> `rate(http_errors_total[1m])`

- Latency (95th percentile):
PromQL --> `histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))`



## Load Testing
******************

- Simulate traffic:
Bash --> `while true; do curl http://localhost:3001; done`

- Simulate errors:
Bash --> `while true; do curl http://localhost:3001/error; done`



## Screenshots
*****************
#### Application Running
![App Running](Project-5_Screenshots/1_App_Running.png)

#### Metrics Endpoint
![Prometheus Metrics Endpoint](Project-5_Screenshots/2_Prometheus_Metrics_Endpoint.png)

#### Prometheus Targets
![Prometheus Targets](Project-5_Screenshots/3_Prometheus_Targets.png)

#### Http Requests Total
![Http Requests Total](Project-5_Screenshots/4_Http_Requests_Total.png)

#### Grafana Dashboard
![Grafana Dashboard](Project-5_Screenshots/5_Grafana_Dashboard_1.png) 
![Grafana Dashboard](Project-5_Screenshots/6_Grafana_Dashboard_2.png)

#### Error Simulation
![Error-Simulation Graph-change](Project-5_Screenshots/7_Error_Simulation-Graph_change.png)

#### Alerts
![Alert Inactive](Project-5_Screenshots/8_Alert_Inactive.png)
![Alert Firing](Project-5_Screenshots/9_Alert_Firing.png)



## What I Learned
********************
- How to use PromQL queries
- How Prometheus scrapes metrics using ServiceMonitor
- Difference between Counter and Histogram
- How to calculate latency percentiles (P95)
- How alerting works in Prometheus
- How Kubernetes labels connect components together (Pods, Services, and ServiceMonitors)


## Author
Ali Yasser
