
# 🐳 Dockerized Server Manager

This repository contains a `docker-compose.yml` file that sets up:

- [Technitium DNS Server](https://github.com/TechnitiumSoftware/DnsServer)
- [Nginx Proxy Manager](https://github.com/NginxProxyManager/nginx-proxy-manager)

Useful for local DNS resolution and easy management of reverse proxies with Let's Encrypt support.

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
```

### 2. Start the Services

```bash
docker compose up -d
```

This will start:

* Technitium DNS Server on port `5380`
* Nginx Proxy Manager on ports `80`, `81`, and `443`
* MariaDB as the database backend for NPM

---

## 🌐 Access the Applications

### 🧠 Technitium DNS Server

* **URL:** [http://localhost:5380](http://localhost:5380)

### 🛠️ Nginx Proxy Manager (NPM)

* **URL:** [http://localhost:81](http://localhost:81)
* Default login:

  * **Email:** `admin@example.com`
  * **Password:** `changeme`

> ⚠️ Make sure to change these credentials after first login.

---

## ⚙️ Run Your Own Web App

You can run your web app on **any port**, for example:

```bash
docker run -d -p 3000:3000 your-app-image
```

Then:

1. **Open Nginx Proxy Manager** ([http://localhost:81](http://localhost:81))
2. **Add a new proxy host**:

   * Domain: your-domain.com
   * Forward Hostname / IP: `host.docker.internal` (for local apps)
   * Forward Port: `3000` (or your app’s port)
3. Enable SSL (optional) with Let's Encrypt

---

## 🌍 Connect Domain to the World via DNS

1. Open **Technitium DNS Server** ([http://localhost:5380](http://localhost:5380))
2. Create a **new zone** for your domain (e.g. `your-domain.com`)
3. Add **A records** pointing your domain/subdomains to your public IP
4. (Optional) Add CNAME, TXT, or MX records as needed

Once configured and your domain is using Technitium as its authoritative DNS server (or if you're using it as a local resolver), it will route traffic properly to your local services via Nginx Proxy Manager.

---

## 🛑 Stopping the Services

```bash
docker compose down
```

---

## 🗂️ Volumes Used

* `dns_data`: Persistent data for DNS server
* `app_data`: Configuration and SSL data for NPM
* `npm_db_data`: MariaDB database storage

---

## 📝 Requirements

* [Docker](https://docs.docker.com/get-docker/)
* [Docker Compose](https://docs.docker.com/compose/)

```
