# Docker

Bu fayl Docker bilan kundalik ishlash uchun qisqa va amaliy buyruqlar toplami.

## 1) Image buyruqlari

```bash
docker images                                # Image ro'yxatini ko'rish uchun
docker pull nginx:latest                     # Image yuklab olish uchun
docker build -t my/app:1.0 -f Dockerfile .   # Dockerfile asosida image yaratish uchun
docker rmi <image_id_or_name>                # Bitta image'ni o'chirish uchun
docker rmi -f $(docker images -q)            # Barcha image'larni o'chirish uchun
```

## 2) Container buyruqlari

```bash
docker ps                                    # Ishlayotgan container'larni ko'rish uchun
docker ps -a                                 # Barcha container'larni ko'rish uchun
docker run nginx                             # Oddiy holatda container ishga tushirish uchun
docker run -d nginx                          # Container'ni background rejimda ishga tushirish uchun
docker run -p 1234:8080 nginx                # Tashqi va ichki portni bog'lash uchun
docker run --name app -p 30500:80 nginx      # Yangi container ishga tushirish uchun
docker run -d --name app -p 30500:80 nginx   # Background rejimda ishga tushirish uchun
docker stop app                               # Container'ni to'xtatish uchun
docker kill app                               # Container'ni majburan to'xtatish uchun
docker rm app                                 # Container'ni o'chirish uchun
docker rm $(docker ps -aq)                    # Barcha container'larni o'chirish uchun
docker stop $(docker ps -q)                   # Barcha ishlayotgan container'larni to'xtatish uchun
```

## 3) Log va ichkariga kirish

```bash
docker logs app                               # Container loglarini ko'rish uchun
docker logs -f app                            # Loglarni real vaqt rejimida ko'rish uchun
docker exec -it app /bin/sh                   # Container ichida shell ochish uchun
docker exec -u "$UID:$GID" -it app /bin/bash # Joriy user bilan container ichida bash ochish uchun
docker exec app cat /etc/hosts                # Container nomidan buyruq bajarish uchun
docker attach app                              # Asosiy process'ga ulanish uchun
```

## 4) Tozalash buyruqlari

```bash
docker container prune                        # To'xtagan container'larni o'chirish uchun
docker image prune                            # Ishlatilmayotgan image'larni o'chirish uchun
docker system prune -f                        # Keraksiz obyektlarni birga tozalash uchun
docker system prune -a --volumes -f           # Barcha keraksiz image/volume'larni ham tozalash uchun
```

## 5) Docker Compose

```bash
docker compose build                          # Servis image'larini build qilish uchun
docker compose up                             # Servislarni ishga tushirish uchun
docker compose up -d                          # Servislarni background rejimda ishga tushirish uchun
docker compose up --build -d                  # Qayta build qilib backgroundda ishga tushirish uchun
docker compose down                           # Servislarni to'xtatish va tarmoqni yopish uchun
docker compose ps                             # Compose servis holatini ko'rish uchun
docker compose logs -f                        # Compose loglarini real vaqtda ko'rish uchun
```

## 6) Build argument va proxy misoli

```bash
docker build --build-arg PROXY=http://host:port --network host -t octanapp --no-cache -f Dockerfile.local .
docker build --build-arg PROXY=http://host:port -t myapp -f Dockerfile.local .
docker build -f Dockerfile.local .            # Local Dockerfile bilan image build qilish uchun
docker run -p 8080:8080 myapp
```

## 7) Laravel loyihasi yaratish

```bash
docker run --rm -it \
  -v "$PWD":/app \
  --user "$(id -u):$(id -g)" \
  composer create-project laravel/laravel example-app
```
