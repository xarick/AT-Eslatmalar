# Go
Bu fayl Go bilan ishlashda ko'p uchraydigan buyruqlarni tartibli ko'rinishda jamlaydi.

## 1) Go environment va module

```bash
go env -w GO111MODULE=on                               # Module rejimini yoqish uchun
go env -w GOPROXY=https://proxy.golang.org,direct      # Default proxy sozlash uchun

go env -w GOPROXY=http://<proxy-host>:<proxy-port>     # Ichki proxy sozlash uchun
go env -w GONOSUMDB=<private-domain>                   # Private modul domenini checksum'dan chiqarish uchun
go env -w GONOPROXY=<private-domain>                   # Private modul domenini proxy'dan chiqarish uchun

go mod init github.com/<user>/<repo>                   # Yangi modul yaratish uchun
go get -u github.com/gin-gonic/gin                     # Kutubxonani yangilab o'rnatish uchun
go mod tidy                                            # Kerakli paketlarni tozalab/sinxronlash uchun
go clean -modcache                                     # Go module cache'ni tozalash uchun
```

## 2) Loyihani ishga tushirish

```bash
go run ./cmd/api/main.go                               # Loyihani ishga tushirish uchun
go run -v -x ./cmd/api/main.go                         # Batafsil build log bilan ishga tushirish uchun
```

## 3) Go work bilan ishlash

```bash
go work init                                            # Go workspace yaratish uchun
go work use ./tools ./tools/gopls                       # Bir nechta modulni workspace'ga qo'shish uchun
```

## 4) Swagger hujjat yaratish

```bash
go install github.com/swaggo/swag/cmd/swag@latest      # Swag CLI o'rnatish uchun
swag init -g cmd/main.go -o docs                        # Swagger hujjatini docs papkaga generatsiya qilish uchun
```

## 5) Live reload (Air)

```bash
go install github.com/cosmtrek/air@latest             # Air o'rnatish uchun
air init                                              # .air.toml fayl yaratish uchun
air                                                   # Loyihani live reload bilan ishga tushirish uchun
```

## 6) `database/sql` qisqa eslatma

```text
db.Exec(...)     => INSERT, UPDATE, DELETE uchun
db.Query(...)    => Ko'p qatorli SELECT uchun
db.QueryRow(...) => Bitta qatorli SELECT uchun
```

## 7) gRPC va Protobuf

### Pluginlarni o'rnatish

```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest         # Go protobuf plugin o'rnatish uchun
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest        # Go gRPC plugin o'rnatish uchun
go get -u google.golang.org/grpc                                       # gRPC kutubxonasini qo'shish uchun
```

### Protobuf kod generatsiyasi

```bash
protoc -I=proto --go_out=pb proto/*.proto
protoc -I=proto --go_opt=paths=source_relative --go_out=pb proto/*.proto

protoc --go_out=. --go-grpc_out=. proto/greet.proto
protoc --go_out=. \
  --go_opt=module=github.com/<user>/<repo> \
  --go-grpc_out=. \
  --go-grpc_opt=module=github.com/<user>/<repo> \
  proto/greet.proto

protoc --go_out=. \
  --go_opt=paths=source_relative \
  --go-grpc_out=. \
  --go-grpc_opt=paths=source_relative \
  proto/user_service.proto

protoc --go_out=. --go-grpc_out=. proto/auth.proto
protoc --go_out=. --go-grpc_out=require_unimplemented_servers=false:. proto/auth.proto

protoc --proto_path=proto --go_out=pb --go_opt=paths=source_relative --go-grpc_out=pb --go-grpc_opt=paths=source_relative proto/*.proto
```

## 8) Lint

```bash
golangci-lint run                                       # Kod sifatini tekshirish uchun
```

## 9) Jarayonni to'xtatish (Windows)

```bat
netstat -ano | findstr :8000                            # Portga bog'langan jarayonni topish uchun
taskkill /F /PID <pid>                                  # PID bo'yicha jarayonni to'xtatish uchun
```

## 10) CORS test (faqat lokal test uchun)

```bat
"C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-web-security --disable-gpu --user-data-dir=%LOCALAPPDATA%\Google\chromeTemp
```
Bu usul xavfsizlikni pasaytiradi, faqat test muhiti uchun.
