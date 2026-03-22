# Proxy
Bu fayl turli vositalar uchun proxy sozlash bo'yicha qisqa eslatma.

## 1) Windows

CMD uchun:

```bat
set HTTP_PROXY=http://<proxy-host>:<proxy-port>
set HTTPS_PROXY=http://<proxy-host>:<proxy-port>
```

WinHTTP uchun:

```bat
netsh winhttp set proxy proxy-server="http://<username>:<password>@<proxy-host>:<proxy-port>"
```

## 2) Linux/macOS

Shell session uchun:

```bash
export http_proxy=http://<proxy-host>:<proxy-port>
export https_proxy=http://<proxy-host>:<proxy-port>
export no_proxy=localhost,127.0.0.1,*.example.local
```

## 3) Curl

```bash
curl -x http://<proxy-host>:<proxy-port> http://google.com --proxy-ntlm
```

## 4) Git

```bash
git config --global http.proxy http://<proxy-host>:<proxy-port>
git config --global https.proxy http://<proxy-host>:<proxy-port>
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 5) Go

```bash
go env -w GO111MODULE=on
go env -w GOPROXY=https://proxy.golang.org,direct

go env -w GOPROXY=http://<proxy-host>:<proxy-port>
go env -w GONOSUMDB=<private-domain>
go env -w GONOPROXY=<private-domain>
```

## 6) Python (pip)

Windows: `%APPDATA%\pip\pip.ini`  
Linux: `$HOME/.config/pip/pip.conf` yoki `$HOME/.pip/pip.conf`

```ini
[global]
proxy = http://<proxy-host>:<proxy-port>
https_proxy = http://<proxy-host>:<proxy-port>
trusted-host =
    pypi.python.org
    pypi.org
    files.pythonhosted.org
```

Global bo'lmagan holat uchun:

```bash
pip install --proxy http://<username>:<password>@<proxy-host>:<proxy-port> <package-name>
```

## 7) NPM

```bash
npm config set proxy http://<proxy-host>:<proxy-port>
npm config set https-proxy http://<proxy-host>:<proxy-port>
npm config set registry https://registry.npmjs.org
npm config set strict-ssl false
```

## 8) Composer

```bash
composer config --global disable-tls true
composer config --global secure-http false
composer config --global repo.packagist composer http://packagist.org
```

## 9) Spring / Maven

IntelliJ IDEA'da proxy yoqilgandan so'ng:

```text
name: MAVEN_OPTS
value: -Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true
```

`C:\Users\<user>\.m2\settings.xml` uchun namuna:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <offline>false</offline>
  <proxies>
    <proxy>
      <active>true</active>
      <protocol>http</protocol>
      <host><proxy-host></host>
      <port><proxy-port></port>
    </proxy>
  </proxies>
  <mirrors>
    <mirror>
      <id>maven-default-http-blocker</id>
      <mirrorOf>external:dont-match-anything-mate:*</mirrorOf>
      <name>Pseudo repository for external HTTP repositories.</name>
      <url>http://0.0.0.0/</url>
    </mirror>
  </mirrors>
</settings>
```
