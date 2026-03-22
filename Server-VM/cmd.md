# CMD Cheat Sheet (CP)

Bu fayl Windows CMD uchun asosiy va amaliy buyruqlarni jamlaydi.

## 1) Asosiy buyruqlar

```bat
exit                         REM CMD oynasidan chiqish uchun
cls                          REM Oynani tozalash uchun

cd folder_name               REM Papkaga kirish uchun
cd ..                        REM Oldingi papkaga qaytish uchun

help                         REM Buyruqlar ro'yxatini ko'rish uchun
help X                       REM X buyruq bo'yicha yordam olish uchun
help rmdir                   REM Muayyan buyruq bo'yicha yordam uchun
rmdir /?                     REM Buyruq sintaksisini ko'rish uchun

dir                          REM Joriy papkadagi fayllarni ko'rish uchun
mkdir new_folder             REM Yangi papka yaratish uchun
rmdir new_folder             REM Bo'sh papkani o'chirish uchun
rmdir /s /q new_folder       REM Ichidagi fayllar bilan papkani o'chirish uchun

del file.txt                 REM Bitta faylni o'chirish uchun
del C:\path\file.txt         REM Boshqa papkadagi faylni o'chirish uchun
del /s *.txt                 REM Joriy papkada .txt fayllarni rekursiv o'chirish uchun
del /s *.*                   REM Joriy papkada barcha fayllarni rekursiv o'chirish uchun

move file.txt .\backup\      REM Faylni ko'chirish uchun
copy file.txt new_name.txt   REM Fayl nusxasini olish uchun
ren file.txt new_name.txt    REM Fayl nomini o'zgartirish uchun
```

## 2) Qidirish va saralash

```bat
more file.txt                        REM Matnni sahifalab ko'rish uchun
sort file.txt                        REM Alifbo tartibida saralash uchun
sort /r file.txt                     REM Teskari tartibda saralash uchun
sort file.txt > sorted.txt           REM Saralangan natijani faylga yozish uchun

find "text" file.txt                 REM Fayldan matn qidirish uchun
find "text" *                        REM Barcha fayllardan matn qidirish uchun
find /i "text" *                     REM Katta-kichik harfga e'tiborsiz qidirish uchun

dir > out.txt                        REM Buyruq natijasini faylga yozish uchun
echo Salom > out.txt                 REM Matnni faylga yozish uchun
```

## 3) Tizim va tarmoq

```bat
ipconfig                       REM Tarmoq sozlamalarini ko'rish uchun
echo %username%                REM Joriy foydalanuvchi nomini ko'rish uchun
tree                           REM Papkalarni daraxt ko'rinishida ko'rish uchun
systeminfo                     REM Tizim ma'lumotlarini ko'rish uchun
tasklist                       REM Jarayonlar ro'yxatini ko'rish uchun
tasklist /v                    REM Jarayonlarni kengaytirilgan ko'rishda olish uchun

net user                       REM Foydalanuvchilar ro'yxatini ko'rish uchun
net user administrator         REM Muayyan foydalanuvchi ma'lumotlarini ko'rish uchun

ping 192.168.1.1               REM Tarmoq ulanishini tekshirish uchun
title My CMD Window            REM Oyna sarlavhasini o'zgartirish uchun
```

## 4) `.cmd`/`.bat` script namunalari

Hello world:

```bat
@echo off
title Dars
echo Hello world
pause
```

Ikki son yig'indisi:

```bat
@echo off
set /p a=Enter a:
set /p b=Enter b:
set /a c=%a%+%b%
echo Natija=%c%
pause
```

`if exist` bilan fayl tekshirish:

```bat
@echo off
if exist .\test.txt (
  echo Fayl topildi
) else (
  echo Fayl topilmadi
)
pause
```

`for` sikli:

```bat
@echo off
for %%i in (1,2,3,4,5) do echo %%i
pause
```

1 dan 5 gacha papka yaratish:

```bat
@echo off
for /l %%i in (1,1,5) do mkdir .\%%i
pause
```

## 5) Arifmetik scriptlar

Ikki son bilan amallar:

```bat
@echo off
set /p a=Enter a:
set /p b=Enter b:

set /a c=a+b
echo yigindi=%c%

set /a c=a-b
echo ayirma=%c%

set /a c=a/b
echo bolinma=%c%

set /a c=a*b
echo kopaytma=%c%
pause
```

Argument orqali yig'indi (`calc.cmd 3 4`):

```bat
@echo off
set /a a=%1
set /a b=%2
set /a c=%a%+%b%
echo natija=%c%
pause
```

## 6) Inline argument bilan papka yaratish

`mk.cmd my_folder`:

```bat
@echo off
mkdir %1
```

## 7) `if` va taqqoslash misollari

Son 5 ga tengligini tekshirish:

```bat
@echo off
set /p a=Enter a:
if %a%==5 echo son 5 ga teng
pause
```

`EQU/NEQ/LSS/LEQ/GTR/GEQ` operatorlari:

```bat
@echo off
set /p a=Enter a:

if %a% EQU 5 echo son 5 ga teng
if %a% NEQ 5 echo son 5 ga teng emas
if %a% LSS 5 echo son 5 dan kichik
if %a% GEQ 5 echo son 5 ga teng yoki katta
pause
```

`if else` bilan katta/kichik tekshirish:

```bat
@echo off
set /p a=Enter a:
if %a% LSS 5 (
  echo son 5 dan kichik
) else (
  echo son 5 dan katta yoki teng
)
pause
```

## 8) `for` sikli misollari

1 dan 10 gacha chiqarish:

```bat
@echo off
for /l %%i in (1,1,10) do echo %%i
pause
```

1 dan 5 gacha fayl yaratish:

```bat
@echo off
for /l %%i in (1,1,5) do echo.> .\%%i.txt
pause
```

1 dan 5 gacha papka yaratish:

```bat
@echo off
for /l %%i in (1,1,5) do mkdir .\%%i
pause
```
