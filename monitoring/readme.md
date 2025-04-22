Cài Node Exporter trên máy chủ: port 9100
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
tar xvfz node_exporter-1.6.1.linux-amd64.tar.gz
cd node_exporter-1.6.1.linux-amd64
./node_exporter
```

chạy Node Exporter trong Docker
```bash
/root/thu/BigDataProject/node_exporter-1.6.1.linux-amd64/node_exporter &

sudo netstat -tuln | grep 9100

sudo ufw allow 9100
```

Cấu hình Prometheus để scrape Node Exporter
```bash
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'inference-api'
    scrape_interval: 5s
    static_configs:
      - targets: ['inference-api:8000']

  - job_name: 'node-exporter'
    scrape_interval: 15s
    static_configs:
      - targets: ['localhost:9100']  # Thay 'localhost' bằng IP hoặc hostname của Node Exporter
```

Khởi động lại Prometheus
```bash
docker-compose restart prometheus
```