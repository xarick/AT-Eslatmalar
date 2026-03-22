# Terminal
Bu fayl Linux terminal buyruqlari bo'yicha amaliy eslatma.

## 1) Navigatsiya va umumiy buyruqlar

```bash
man pwd                     # Buyruq hujjatini ko'rish uchun
clear                       # Terminalni tozalash uchun
exit                        # Sessiyadan chiqish uchun

pwd                         # Joriy papka yo'lini ko'rish uchun
cd folder                   # Papkaga kirish uchun
cd ..                       # Oldingi papkaga qaytish uchun
cd ~                        # Home papkaga o'tish uchun
```

## 2) Fayl/papka bilan ishlash

```bash
mkdir docs                  # Papka yaratish uchun
touch notes.txt             # Bo'sh fayl yaratish uchun
echo "salom" > notes.txt    # Faylga yozish uchun

ls                          # Joriy papkadagi fayllarni ko'rish uchun
ls -l                       # Batafsil ro'yxatni ko'rish uchun
ls -la                      # Yashirin fayllar bilan ko'rish uchun

cat notes.txt               # Fayl ichini chiqarish uchun
less notes.txt              # Faylni sahifalab ko'rish uchun
head -n 5 notes.txt         # Yuqoridan 5 qatorni ko'rish uchun
tail -n 5 notes.txt         # Pastdan 5 qatorni ko'rish uchun

cp notes.txt notes2.txt     # Nusxa olish uchun
mv notes.txt ./backup/      # Ko'chirish uchun

rm notes.txt                # Faylni o'chirish uchun
rm -i notes.txt             # Tasdiqlab o'chirish uchun
rmdir empty_dir             # Bo'sh papkani o'chirish uchun
rm -r dir_name              # Papkani ichidagi fayllar bilan o'chirish uchun
```

## 3) Qidirish va saralash

```bash
grep "text" file.txt                # Matn qidirish uchun
grep -n "text" file.txt             # Qator raqami bilan qidirish uchun
grep -i "text" file.txt             # Katta-kichik harfga e'tiborsiz qidirish uchun
grep -r "text" ./                   # Rekursiv qidirish uchun
grep -l "text" *.txt                # Faqat fayl nomlarini olish uchun

find ./ -name "fi*"                 # Nomi bo'yicha fayl/papkani topish uchun
sort file.txt                       # Saralash uchun
du -sh ./                           # Hajmni ko'rish uchun
```

## 4) Tizim va jarayonlar

```bash
uname -a                     # Tizim ma'lumotini ko'rish uchun
free -h                      # RAM holatini ko'rish uchun
uptime                       # Tizim uptime ni ko'rish uchun
df -h                        # Disk holatini ko'rish uchun

ps                           # Joriy sessiya jarayonlarini ko'rish uchun
ps aux                       # Barcha jarayonlarni ko'rish uchun
ps aux | grep app            # Muayyan jarayonni qidirish uchun

kill -15 <pid>               # Jarayonni yumshoq to'xtatish uchun
kill -9 <pid>                # Jarayonni majburan to'xtatish uchun
top                          # Jarayonlarni real vaqtda kuzatish uchun
htop                         # Qulay monitoring interfeysi uchun
nice -n 10 ./app             # Prioritet berib ishga tushirish uchun
renice -n 5 -p <pid>         # Ishlayotgan jarayon prioritetini o'zgartirish uchun
```

## 5) Ruxsatlar va ownership

```bash
chmod 755 file.txt           # Ruxsatni raqamli usulda berish uchun
chmod o+wx file.txt          # Others uchun ruxsat qo'shish uchun
chmod o-x file.txt           # Others uchun execute ruxsatini olish uchun
chmod -R 755 folder/         # Papka ichidagi hamma faylga ruxsat berish uchun

sudo chown user file.txt     # Egasini o'zgartirish uchun
sudo chgrp group file.txt    # Guruhini o'zgartirish uchun
sudo chown user:group file.txt # Egasi va guruhini birga o'zgartirish uchun
```

## 6) Foydalanuvchi va guruh

```bash
whoami                        # Joriy foydalanuvchini ko'rish uchun
groups                        # Joriy guruhlarni ko'rish uchun

sudo adduser testuser         # Foydalanuvchi qo'shish uchun
sudo passwd testuser          # Foydalanuvchi parolini yangilash uchun
sudo deluser testuser         # Foydalanuvchini o'chirish uchun

sudo groupadd devgroup        # Guruh yaratish uchun
sudo usermod -aG devgroup testuser  # Foydalanuvchini guruhga qo'shish uchun
sudo delgroup devgroup        # Guruhni o'chirish uchun
```

## 7) Tarmoq buyruqlari

```bash
hostname                      # Host nomini ko'rish uchun
ping google.com               # Tarmoq ulanishini tekshirish uchun
ip a                          # IP interfeyslarni ko'rish uchun
ifconfig                      # Legacy usulda interfeyslarni ko'rish uchun
netstat -r                    # Routing jadvalini ko'rish uchun
arp -e                        # ARP jadvalini ko'rish uchun
nslookup example.com          # DNS lookup uchun
dig example.com               # DNS yozuvlarini tekshirish uchun
traceroute example.com        # Marshrut yo'lini tekshirish uchun
```

## 8) Paketlar va servislar

```bash
sudo apt update               # Paket ro'yxatini yangilash uchun
sudo apt upgrade              # Paketlarni yangilash uchun
sudo apt install <package>    # Paket o'rnatish uchun
sudo apt remove <package>     # Paket o'chirish uchun

sudo systemctl status ssh     # Servis holatini ko'rish uchun
sudo systemctl enable ssh     # Servisni doimiy yoqish uchun
sudo systemctl start ssh      # Servisni ishga tushirish uchun
```

## 9) Archive va hex

```bash
tar -cvf archive.tar file1 file2     # Arxiv yaratish uchun
tar -xvf archive.tar -C ./            # Arxivdan chiqarish uchun
hexdump -C file.bin                   # Hex + ASCII ko'rish uchun
```

## 10) Job control

```bash
./script.sh &                 # Orqa fon rejimida ishga tushirish uchun
jobs                          # Joriy terminaldagi joblarni ko'rish uchun
fg %1                         # Jobni old rejimga qaytarish uchun
kill %1                       # Jobni to'xtatish uchun
nohup ./script.sh &           # Terminal yopilganda ham ishni davom ettirish uchun
disown %1                     # Jobni shelldan ajratish uchun
pkill -f script.sh            # Script nomi bo'yicha jarayonni o'chirish uchun
```

## 11) Scheduler (at va cron)

Crontab sintaksis rasmi: [crontab.png](./images/crontab.png)

```bash
sudo apt install at                      # at paketini o'rnatish uchun
echo "echo hello > /tmp/out.txt" | at 16:30  # Belgilangan vaqtda buyruq bajarish uchun

atq                                      # Navbatdagi at vazifalarni ko'rish uchun
atrm <job-id>                            # at vazifani o'chirish uchun

crontab -e                               # Cron jadvalini tahrirlash uchun
crontab -l                               # Cron jadvalini ko'rish uchun
crontab -r                               # Cron jadvalini o'chirish uchun

* * * * * /home/<user>/script.sh         # Har daqiqada bajarish uchun
10 * * * * /home/<user>/script.sh        # Har soatning 10-daqiqasida bajarish uchun
30 2 * * * /home/<user>/script.sh        # Har kuni 02:30 da bajarish uchun
@reboot /home/<user>/script.sh           # Tizim qayta ishga tushganda bajarish uchun
```

## 12) Bash script mini misollar

O'zgaruvchi:

```bash
#!/bin/bash
site="example.com"
echo "$site bizning sayt"
```

Argument bilan hisoblash:

```bash
#!/bin/bash
sum=$(( $1 + $2 ))
echo "Natija: $sum"
```

`if/else`:

```bash
#!/bin/bash
if [ "$1" -gt 5 ]; then
  echo "Son 5 dan katta"
else
  echo "Son 5 dan kichik yoki teng"
fi
```

`while`:

```bash
#!/bin/bash
num=1
sum=0
while [ "$num" -le "$1" ]; do
  sum=$((sum + num))
  num=$((num + 1))
done
echo "Yig'indi: $sum"
```

`for` bilan ro'yxat:

```bash
#!/bin/bash
for lang in C++ Go Python PHP; do
  echo "$lang dasturlash tili"
done
```

Array bilan ishlash:

```bash
#!/bin/bash
langs=("C++" "Go" "Python" "PHP")
echo "Birinchi til: ${langs[0]}"
for lang in "${langs[@]}"; do
  echo "Til: $lang"
done
```

## 13) Environment qiymatlar

```bash
env                          # Barcha environment qiymatlarini ko'rish uchun
printenv PATH                # Muayyan qiymatni ko'rish uchun
echo $PATH                   # PATH qiymatini chiqarish uchun

export MY_SITE=example.com   # Session uchun env qiymat qo'shish uchun
echo $MY_SITE                # Qo'shilgan qiymatni tekshirish uchun
```

Doimiy sozlash uchun `~/.bashrc` yoki `~/.bash_profile` fayliga yoziladi.

## 14) Foydalanuvchi ma'lumot fayllari

```bash
cat /etc/passwd              # Foydalanuvchi hisoblarini ko'rish uchun
sudo cat /etc/shadow         # Parol hash ma'lumotlarini ko'rish uchun
sudo cat /etc/gshadow        # Guruhning maxfiy ma'lumotlarini ko'rish uchun
```

## 15) Password policy (chage)

```bash
sudo chage -l testuser                 # Parol muddati holatini ko'rish uchun
sudo chage testuser                    # Interaktiv qayta sozlash uchun
sudo chage -M 10 testuser              # Maksimal parol muddatini 10 kunga sozlash uchun
sudo chage -d YYYY-MM-DD testuser      # Keyingi parol yangilash sanasini berish uchun
```

## 16) SSH server o'rnatish (Linux)

```bash
sudo apt update
sudo apt install openssh-server        # SSH server o'rnatish uchun
sudo systemctl enable ssh              # SSH serverni doimiy yoqish uchun
sudo systemctl start ssh               # SSH serverni ishga tushirish uchun
sudo systemctl status ssh              # SSH server holatini tekshirish uchun

ssh username@127.0.0.1 -p 2222         # Muayyan host/port bilan ulanish uchun
```

Client o'rnatish:

```bash
sudo apt install openssh-client         # Debian/Ubuntu uchun
sudo dnf install openssh-clients        # Fedora/RHEL/CentOS uchun
```

## 17) TTY va session

```bash
tty                            # Joriy terminal nomini ko'rish uchun
sudo chvt 2                    # Boshqa virtual terminalga o'tish uchun
history                        # Buyruqlar tarixini ko'rish uchun
```

## 18) Tarmoq bo'yicha qo'shimcha buyruqlar

```bash
route                          # Marshrut jadvalini ko'rish uchun
netstat                        # Tarmoq aloqalari va socket holatini ko'rish uchun
ethtool <iface>                # Tarmoq interfeysi texnik ma'lumotini ko'rish uchun
host example.com               # Domenning IP manzilini ko'rish uchun
```

ARP flag eslatmasi:
- `C` - Connected
- `M` - Manual entry
- `P` - Proxy ARP
- `<space>` - vaqtinchalik yozuv

## 19) `htop` ustunlari qisqacha

```text
tasks   => Jarayonlar soni uchun
thr     => Oqimlar soni uchun
pid     => Jarayon ID uchun
user    => Jarayon egasi uchun
pri     => Prioritet uchun
ni      => Nice qiymati uchun
virt    => Virtual xotira hajmi uchun
res     => Band qilingan RAM uchun
shr     => Umumiy xotira uchun
s       => Holat (running/sleeping/zombie) uchun
cpu     => CPU foizi uchun
mem     => RAM foizi uchun
time    => Jarayon ishlash vaqti uchun
command => Jarayon nomi uchun
```

## 20) Midnight Commander (MC)

```bash
sudo apt install mc            # MC o'rnatish uchun
mc                             # MC ishga tushirish uchun
```

Asosiy tugmalar:
- `F2` - Fayl menyusi uchun
- `F3` - Ko'rish rejimi uchun
- `F4` - Tahrirlash rejimi uchun
- `F5` - Nusxa olish uchun
- `F6` - Ko'chirish uchun
- `F7` - Papka yaratish uchun
- `F8` - O'chirish uchun
- `F9` - Yuqori menyu uchun
- `F10` - Chiqish uchun

Qo'shimcha tugmalar:
- `Insert` - Fayl tanlash uchun
- `Alt + ?` - Qidirish uchun
- `Alt + i` - Yashirin fayllarni yoqish/o'chirish uchun
- `Ctrl + o` - MC panelini yashirish/ko'rsatish uchun
- `Ctrl + u` - Panellarni almashtirish uchun
- `Ctrl + r` - Panelni yangilash uchun

## 21) Vim qisqa eslatma

```bash
sudo apt install vim           # Vim o'rnatish uchun
vim filename                   # Fayl ochish uchun
vim -R filename                # Faqat o'qish rejimida ochish uchun
```

Rejimlar:
- `Normal` - boshqaruv rejimi uchun
- `Insert` - matn kiritish rejimi uchun
- `Visual` - belgilash rejimi uchun

Asosiy buyruqlar:
- `:w` - saqlash uchun
- `:q` - chiqish uchun
- `:wq` - saqlab chiqish uchun
- `:q!` - saqlamasdan chiqish uchun
- `yy` - qator nusxasi uchun
- `dd` - qator kesish uchun
- `p` - joylash uchun
- `/text` - qidirish uchun

## 22) Qo'shimcha script misoli (vaqtni faylga yozish)

```bash
#!/bin/bash
out_file="output.txt"
while true; do
  date > "$out_file"
  sleep 1
done
```
