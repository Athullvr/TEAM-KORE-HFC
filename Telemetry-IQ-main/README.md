# Telemetry IQ

Telemetry IQ  is a predictive system telemetry monitoring, ML-driven anomaly detection, and blast radius propagation analysis platform. It provides real-time system performance insights, correlates code deployments and configuration changes to performance drops, and traces potential service failure pathways to estimate downstream risks, affected users, and financial exposure.

---

## 🚀 Key Features

* **Real-time Metrics Dashboard**: Interactive visual dashboards displaying live CPU, memory, request rates, error counts, and latency percentiles.
* **ML-based Anomaly Detection**: Uses pre-trained **Isolation Forest** and **Random Forest** models to continuously score system metrics and identify anomalous behavior.
* **Change Correlation Engine**: Automatically maps recent deployment, configuration, or rollback events to metrics shifts to determine if a change caused the degradation.
* **Blast Radius Analysis & Propagation Tracing**: Traces system dependency graphs to predict downstream service impacts, estimate affected users, assess SLA violation risks, and calculate financial exposure.
* **Simulated Failure Scenarios**: Built-in test harnesses to simulate system anomalies like memory leaks, traffic spikes, and faulty deployments.

---

## 🛠️ Tech Stack & Architecture

Telemetry IQ is built on a modern, decoupled microservices architecture:

* **Frontend**: Next.js & React dashboard styled with Tailwind CSS, utilizing interactive charts and dependency visualization.
* **Backend**: FastAPI web server hosting endpoints for metrics ingestion, machine learning inference, and analytics.
* **Database**: MongoDB for persisting system metrics, deployment event history, alerts, and user profiles.
* **Monitoring & Alerts**: Prometheus for metrics collection and scraping, combined with customized Grafana instances.
* **ML Engines**: Python-based models built on `scikit-learn` and loaded via `joblib` for on-the-fly metric feature extraction (e.g., trend, variance, volatility, and unit economics ratios).

---

## 📂 Project Structure

```
Telemetry-IQ/
├── src/
│   ├── backend/             # FastAPI backend containing the ML model logic, database setup, and APIs
│   ├── frontend/            # Next.js frontend dashboard application
│   ├── mock-services/       # Scenarios simulating normal usage, traffic spikes, memory leaks, and bad deploys
│   ├── data/                # Data storage directory for ML inputs, outputs, and cached results
│   ├── prometheus.yml       # Prometheus server configuration
│   ├── grafana_custom.ini   # Custom configuration for Grafana
│   ├── docker-compose.yml   # Multi-container orchestration config
│   └── run_locally.sh       # Local script to launch backend, mock-services, and monitoring tools
├── isolation_forest_model.pkl  # Trained Isolation Forest model for anomaly detection
└── random_forest_model.pkl     # Trained Random Forest model for metric classification
```

## 📈 ML Feature Engineering

The anomaly detection engine extracts **15 critical system features** from time-series metrics before running prediction algorithms:
1. `mean_cpu` - Average CPU usage
2. `std_cpu` - CPU standard deviation (dispersion)
3. `min_cpu` - Minimum CPU usage
4. `max_cpu` - Maximum CPU usage
5. `delta_cpu` - End-to-start CPU difference
6. `cpu_trend` - CPU slope trend line
7. `cpu_volatility` - Rate of CPU variance
8. `mean_memory` - Average memory footprint
9. `std_memory` - Memory dispersion
10. `memory_trend` - Memory growth trend line
11. `mean_requests` - Average request throughput
12. `request_spike_count` - Number of sudden traffic increases
13. `throughput_delta` - Net throughput delta
14. `cost_delta` - Financial cost variance
15. `unit_economics_ratio` - Compute resources per processed request
