# SSH
Bu fayl SSH ulanish, tunnel va remote app ishga tushirish bo'yicha amaliy eslatma.

## 1) Oddiy SSH ulanish

```bash
ssh username@<server-ip>                     # Oddiy ulanish uchun
ssh -p 2222 username@<server-ip>             # Custom port bilan ulanish uchun
ssh -i ~/.ssh/server_key.pem username@<server-ip>  # Private key bilan ulanish uchun
```

## 2) SSH kalit yaratish va ulash

```bash
ssh-keygen -t ed25519 -C "dev@example.com"   # Kalit juftligini yaratish uchun
ssh-copy-id -i ~/.ssh/id_ed25519.pub username@<server-ip>  # Public key'ni serverga qo'shish uchun
```

Agar `ssh-copy-id` bo'lmasa:

```bash
cat ~/.ssh/id_ed25519.pub | ssh username@<server-ip> "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## 3) SSH config ishlatish

`~/.ssh/config` namuna:

```sshconfig
Host app-server
  HostName <server-ip>
  User username
  Port 22
  IdentityFile ~/.ssh/server_key.pem
```

Ishlatish:

```bash
ssh app-server
```

## 4) Remote app ni backgroundda ishga tushirish

```bash
nohup ./app > app.out 2>&1 &               # App'ni terminaldan mustaqil ishga tushirish uchun
ps aux | grep ./app                        # Jarayonni tekshirish uchun
tail -f app.out                            # Logni real vaqtda ko'rish uchun
pkill -f ./app                             # App jarayonini to'xtatish uchun
```

## 5) SOCKS5 tunnel

`autossh` o'rnatish:

```bash
sudo apt update
sudo apt install -y autossh
```

Tunnel ochish:

```bash
autossh -M 0 -N -D 127.0.0.1:1080 -i ~/.ssh/server_key.pem username@<server-ip>
```

Tekshirish:

```bash
curl -s --socks5 127.0.0.1:1080 https://ifconfig.me
curl -s --socks5 127.0.0.1:1080 https://ipinfo.io/ip
```

## 6) Local va remote port forwarding

Local port forwarding:

```bash
ssh -L 8080:127.0.0.1:80 username@<server-ip>
```

Remote port forwarding:

```bash
ssh -R 9000:127.0.0.1:3000 username@<server-ip>
```

## 7) SCP bilan fayl ko'chirish

```bash
scp local.txt username@<server-ip>:/home/username/      # Localdan serverga yuborish uchun
scp username@<server-ip>:/home/username/remote.txt .    # Serverdan localga olish uchun
scp -i ~/.ssh/server_key.pem -r ./folder username@<server-ip>:/home/username/  # Papka yuborish uchun
```
