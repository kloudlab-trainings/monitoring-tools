Monitor Nginx
### 1. Installing and Configuring NGINX:
   - Install NGINX if it's not already installed:
     ```
     sudo apt update
     sudo apt install nginx
     ```
   - Ensure NGINX is running:
     ```
     sudo systemctl status nginx
     ```

### 2. Install and Configure NGINX Exporter:
   - Download NGINX Exporter and give it executable permissions:
     ```
     wget https://github.com/nginxinc/nginx-prometheus-exporter/releases/download/v0.9.0/nginx-prometheus-exporter-0.9.0-linux-amd64
     chmod +x nginx-prometheus-exporter-0.9.0-linux-amd64
     ```
   - Start the NGINX Exporter:
     ```
     ./nginx-prometheus-exporter-0.9.0-linux-amd64
     ```

### 3. Configuring Prometheus:
   - Install Prometheus if not already installed:
     ```
     wget https://github.com/prometheus/prometheus/releases/download/v2.30.0/prometheus-2.30.0.linux-amd64.tar.gz
     tar xvfz prometheus-2.30.0.linux-amd64.tar.gz
     cd prometheus-2.30.0.linux-amd64/
     ```
   - Configure Prometheus to scrape NGINX Exporter. Add the following to the `prometheus.yml` file:
     ```
     scrape_configs:
       - job_name: 'nginx'
         static_configs:
         - targets: ['localhost:9113']
     ```
   - Start Prometheus:
     ```
     ./prometheus
     ```

### 4. PromQL Queries and Dashboard Creation:
   - Query NGINX metrics in Prometheus. For example:
     ```
     nginx_http_requests_total
     ```
   - Create a Grafana dashboard and add panels to visualize NGINX metrics.
   - Use Grafana to create custom queries and visualizations for specific NGINX metrics, such as requests per second, active connections, or response times.