# opentelemetry-observability-using-python

A hands-on project to learn and implement **observability for Python microservices** using the **OpenTelemetry stack**.  
This demo showcases how to collect and visualize **metrics, logs, and traces** across multiple FastAPI services, similar to what an SRE or DevOps engineer would build in a real-world environment.

---

## 🚀 Why This Project?
Modern systems are **distributed** and often complex. Debugging and monitoring them without proper observability tools is nearly impossible.  
This project helps answer questions like:
- Is my service healthy?
- How many requests is it handling?
- Where are failures happening?
- How do I trace a request across multiple services?

By building this stack, I explored how observability connects the dots between **metrics, logs, and traces** to give complete visibility.

---

## 🛠️ Tech Stack
- **Python 3 + FastAPI** → Three microservices (`app-a`, `app-b`, `app-c`)  
- **OpenTelemetry SDK** → Automatic instrumentation for metrics, logs, and traces  
- **Prometheus** → Metrics collection  
- **Loki** → Centralized log aggregation  
- **Tempo** → Distributed tracing  
- **Grafana** → Visualization layer  
- **Docker & Docker-Compose** → Container orchestration  
---

## 📋 Prerequisites

Before starting, make sure you have:

1.  **Docker & Docker Compose** installed (Install Guide)
    
2.  **Loki Docker logging driver** installed:
    
    `docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions` 
    
    > Needed for containers to forward logs directly to Loki.
    
3.  **Ports availability**:
    
    -   8000–8002 → FastAPI services
        
    -   3100 → Loki
        
    -   9090 → Prometheus
        
    -   3000 → Grafana
---

## ⚡ Getting Started

### 1. Clone the repo
```
git clone https://github.com/Isameer3056/opentelemetry-observability-using-python.git
cd opentelemetry-observability-using-python
```
### 2. Build and run
```
docker-compose up --build -d
```
This launches all three apps along with Prometheus, Loki, Tempo, and Grafana.

Services will be available at:

-   Service A: [http://localhost:8000](http://localhost:8000)
    
-   Service B: [http://localhost:8001](http://localhost:8001)
    
-   Service C: [http://localhost:8002](http://localhost:8002)
    
-   Grafana: [http://localhost:3000](http://localhost:3000) (default: `admin` / `admin`)
    
-   Prometheus: [http://localhost:9090](http://localhost:9090)

-   Loki: [http://localhost:3100](http://localhost:3100)

### 3. Verify the apps
```
curl http://localhost:8000
curl http://localhost:8001
curl http://localhost:8002
```
## Generate Load
Send requests so telemetry data starts flowing:

Linux / Mac

```
while true; do curl -s http://localhost:8000 > /dev/null; sleep 1; done
```
Windows (PowerShell)
```
powershell

while ($true) { curl http://localhost:8000 | Out-Null; Start-Sleep -Seconds 1 }
```
Repeat for 8001 and 8002.

---

### 📊 Visualize Observability Data
- Grafana → http://localhost:3000 (default login: admin/admin)

- Prometheus → http://localhost:9090

- Loki → Logs via Grafana Explore

- Tempo → Traces via Grafana Explore

---

Example queries in Grafana:

- **Metrics (Prometheus)**:

```scss
rate(http_server_requests_total[1m])
```
- **Logs (Loki)**:

```
{container="app-a"}
```
- **Traces (Tempo)**: Search by service name `app-a`, `app-b`, `app-c`

---

### 📌 Insights & Learnings
- Traces help follow a single request across multiple services.

- Logs provide context and are correlated with traces.

- Metrics give quantitative signals about performance and failures.

- Grafana becomes a single pane of glass for all observability data.

- Running everything in Docker-Compose makes it easy to test locally.

---

This project provided me with a practical understanding of how SREs and DevOps engineers can monitor, troubleshoot, and improve distributed systems.
