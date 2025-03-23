# Forest Staking - Aptos Node Monitoring

This repository provides setup files and configuration guidance to monitor an **Aptos validator node** using:

- **Prometheus** for metric collection
- **Grafana** for dashboards and visualization
- **NGINX** as a secure reverse proxy for web access
- **Systemd services** for persistent and reliable operation

---

## 🔧 What's Included

| Component     | Purpose                                 |
|---------------|-----------------------------------------|
| `validator.service`      | Systemd unit for the Aptos validator node     |
| `validator.yaml`         | Aptos validator node config                   |
| `prometheus.service`     | Prometheus systemd unit                       |
| `grafana-nginx.conf`     | NGINX config to reverse proxy Grafana         |
| `prometheus-nginx.conf`  | NGINX config to reverse proxy Prometheus      |

---

## 🌐 Live Dashboard URLs

| Service     | Domain Name              |
|-------------|---------------------------|
| Prometheus  | [p.foreststaking.com](https://p.foreststaking.com) |
| Grafana     | [g.foreststaking.com](https://g.foreststaking.com) |

---

## 📁 Directory Structure

```
.
├── systemd
│   ├── validator.service
│   └── prometheus.service
│
├── config
│   └── validator.yaml
│
├── nginx
│   ├── grafana-nginx.conf
│   └── prometheus-nginx.conf
│
└── README.md
```

---

## ✅ Requirements

- Ubuntu 20.04+ server
- `aptos-node` binary installed
- NGINX + Certbot
- Domains properly pointed to server IP
- Firewall configured to only expose ports `80` and `443`

---

## 🧠 Usage

### 1. Place systemd service files
```bash
sudo cp systemd/*.service /etc/systemd/system/
sudo systemctl daemon-reload
```

### 2. Start services
```bash
sudo systemctl enable validator prometheus
sudo systemctl start validator prometheus
```

### 3. Set up NGINX configs
```bash
sudo cp nginx/*.conf /etc/nginx/sites-available/
sudo ln -s /etc/nginx/sites-available/grafana-nginx.conf /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/prometheus-nginx.conf /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

---

## 🔐 Security Notes
- Prometheus is protected with basic HTTP auth via `.htpasswd`
- All traffic routed through HTTPS with Let's Encrypt SSL

---

## 👷 Author
**Forest Staking** – [foreststaking.com](https://foreststaking.com)
