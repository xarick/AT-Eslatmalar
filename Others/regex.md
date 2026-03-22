# Regex
Bu fayl muntazam ifodalar bo'yicha tezkor eslatma.

## 1) Belgilar to'plami

```text
[aeiou]      => unli harflarni topish uchun
[A-Z]        => katta harflarni topish uchun
[a-zA-Z]     => katta va kichik harflarni topish uchun
[0-9]        => raqamlarni topish uchun
[^0-9]       => raqamdan boshqa belgilarni topish uchun
```

## 2) Qisqa belgilashlar

```text
\d           => raqamlarni topish uchun
\D           => raqamdan boshqa belgilarni topish uchun
\w           => harf, raqam va "_" belgilarini topish uchun
\W           => \w dan tashqari belgilarni topish uchun
\s           => bo'sh joy, tab, newline belgilarini topish uchun
\S           => bo'sh joy bo'lmagan belgilarni topish uchun
```

## 3) So'z chegarasi

```text
\bmen\b      => "men" so'zini to'liq so'z sifatida topish uchun
\Bmen\B      => "men" ikki tomondan ham so'z ichida bo'lganda topish uchun
\Bmen|men\B  => "men" faqat bir tomondan chegarasiz bo'lsa topish uchun
```

## 4) Alternatsiya va ixtiyoriylik

```text
men|man                 => men yoki man topish uchun
m(e|a)n                 => men yoki man topish uchun
m[ea]n                  => men yoki man topish uchun
color|colour            => color yoki colour topish uchun
colou?r                 => "u" ixtiyoriy bo'lgan holatni topish uchun
java(script)?           => java yoki javascript topish uchun
java(?:script)?         => non-capturing group bilan java/javascript topish uchun
```

## 5) Nuqta va kvantifikatorlar

```text
.            => istalgan bitta belgi uchun
\.           => nuqta belgisini topish uchun
\@           => @ belgisini topish uchun
s...m        => s va m orasida 3 ta istalgan belgi bo'lgan holat uchun
s.{3}m       => s...m bilan bir xil
s.{2,4}m     => s va m orasida 2 tadan 4 tagacha belgi bo'lgan holat uchun
a.{1,}?e     => a dan e gacha minimal moslik uchun
a.+?e        => a va e orasida kamida bitta belgi bilan minimal moslik uchun
a.*?e        => a va e orasida 0 yoki ko'p belgi bilan minimal moslik uchun
```

## 6) Lookaround

```text
and(?= he)                       => "and" dan keyin " he" bo'lsa topish uchun
\b\w+?\b(?=[\s,]*?and)           => "and" dan oldingi so'zlarni topish uchun
```

## 7) Amaliy patternlar

```text
\b\w+@\w+\.\w+\b                 => oddiy email formatni topish uchun
(\b\w+)@(\w+\.\w+\b)             => email qismlarini guruhlab olish uchun
(?:(\w+):\/\/)?([^/]+)(.+)?      => URL qismlarini guruhlab olish uchun
```

## 8) Qo'shimcha

```text
ignoreCase => katta/kichik harf farqini e'tiborsiz qoldirish uchun (flag)
```
