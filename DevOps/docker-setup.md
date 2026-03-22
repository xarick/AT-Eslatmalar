# Docker O'rnatish va Sozlash

Bu fayl Docker Engine'ni o'rnatish, tekshirish va boshlang'ich sozlash uchun.

## 1) Ubuntu (APT) orqali o'rnatish

### Eski paketlarni olib tashlash

```bash
sudo apt-get remove -y docker docker-engine docker.io containerd runc
```

### Repozitoriya uchun tayyorgarlik

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Docker APT repo ulash

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Docker paketlarini o'rnatish

```bash
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Tekshirish

```bash
sudo systemctl enable --now docker
sudo docker run hello-world
docker --version
docker compose version
```

## 2) RHEL/CentOS (YUM/DNF) orqali o'rnatish

### Eski paketlarni olib tashlash

```bash
sudo yum remove -y \
  docker \
  docker-client \
  docker-client-latest \
  docker-common \
  docker-latest \
  docker-latest-logrotate \
  docker-logrotate \
  docker-engine
```

### Repo ulash va o'rnatish

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl enable --now docker
sudo docker run hello-world
```

## 3) Post-install (sudo'siz ishlatish)

```bash
sudo usermod -aG docker $USER
newgrp docker
docker ps
```

`newgrp docker` joriy session uchun yangi groupni yoqish uchun. Kerak bo'lsa tizimga qayta kirish ham mumkin.

## 4) Docker CLI proxy sozlash (`~/.docker/config.json`)

```bash
mkdir -p ~/.docker
cat > ~/.docker/config.json <<'JSON'
{
  "proxies": {
    "default": {
      "httpProxy": "http://IP:PORT",
      "httpsProxy": "http://IP:PORT",
      "noProxy": "*.example.com,127.0.0.0/8,localhost"
    }
  }
}
JSON
```

## 5) Docker daemon proxy sozlash (systemd)

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo tee /etc/systemd/system/docker.service.d/http-proxy.conf > /dev/null <<'EOF'
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:80"
Environment="HTTPS_PROXY=http://proxy.example.com:443"
Environment="NO_PROXY=localhost,127.0.0.1,.corp"
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 6) Docker'ni olib tashlash

Ubuntu:

```bash
sudo apt-get remove -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo rm -rf /var/lib/docker /var/lib/containerd
```

RHEL/CentOS:

```bash
sudo yum remove -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo rm -rf /var/lib/docker /var/lib/containerd
```

## 7) Foydali rasmiy havolalar

- https://docs.docker.com/engine/install/ubuntu/
- https://docs.docker.com/engine/install/centos/
- https://docs.docker.com/engine/install/linux-postinstall/
- https://docs.docker.com/network/proxy/
