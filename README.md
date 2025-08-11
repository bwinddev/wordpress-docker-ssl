
# 🐳 WordPress + Docker + HTTPS (.test domain)

A local development environment using WordPress, MySQL, Nginx, and full HTTPS support via mkcert on the https domain.

---

## 🔧 Requirements

- Docker & Docker Compose
- mkcert (to generate local HTTPS certificates)
- Terminal / Code editor

---

## 📁 Project Structure

```
wpdocker/
├── docker-compose.yml
├── wordpress/              # WordPress files (mapped to container)
├── php.ini                 # Custom PHP settings
├── nginx/
│   ├── conf.d/
│   │   └── default.conf    # Nginx virtual host with proxy
│   └── ssl/
│       ├── your.test.pem
│       └── your.test-key.pem
```

---

## 🚀 Starting the environment

```bash
docker compose up -d --build
```

---

## 🔐 Generating HTTPS Certificates with mkcert

If you don't have certificates yet:

### 1. Install mkcert

#### Ubuntu:

```bash
sudo apt install libnss3-tools
brew install mkcert
mkcert -install
```

Or manually:

```bash
wget https://github.com/FiloSottile/mkcert/releases/latest/download/mkcert-v1.4.4-linux-amd64
chmod +x mkcert-v1.4.4-linux-amd64
sudo mv mkcert-v1.4.4-linux-amd64 /usr/local/bin/mkcert
mkcert -install
mkcert your.test
```

### 2. Generate certificates

```bash
mkcert -key-file ./nginx/ssl/your.test-key.pem -cert-file ./nginx/ssl/your.test.pem your.test
```

### 3. Add domain to /etc/hosts

```bash
sudo nano /etc/hosts
```

Add this line:

```
127.0.0.1 your.test
```

---

## 🐘 Database Access

- DB host: `db`
- DB user: `wordpress`
- DB password: `wordpress`
- DB name: `wordpress`
- DB root password: `wordpress`

---

## 🧯 Troubleshooting

- **Database connection error**: check port bindings and environment variables.
- **"Cookies are blocked"**: ensure your browser accepts cookies for `http://your.test`.
- **HTTPS not working**: recheck certificate paths and `hosts` file.

---

## 🧹 Reset / Clean Up

```bash
docker compose down -v
rm -rf wordpress/* dbdata/*
```

---

## 📌 Notes

- If your browser block cookies add cert file in settings in browser to allow third party cookies.
