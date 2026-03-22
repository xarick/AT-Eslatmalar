# Git Cheat Sheet (CP)

Bu fayl Git bilan kundalik ishlash uchun qisqa va amaliy qo'llanma.

## 1) Holatni tekshirish

```bash
git status          # Ishchi papkadagi o'zgarishlar holati
git diff            # Commit qilinmagan o'zgarishlar farqi
git diff --staged   # Staging'ga qo'shilgan o'zgarishlar farqi
git log --oneline --graph --decorate -n 15  # Qisqa commit tarixi
git show <commit>   # Bitta commit ichidagi o'zgarishlarni ko'rish uchun
```

## 2) Branch bilan ishlash

```bash
git branch                      # Lokal branchlarni ko'rish uchun
git branch -r                   # Remote branchlarni ko'rish uchun
git branch dev                  # dev branch yaratish uchun
git branch dev main             # main asosida dev branch yaratish uchun
git switch -c dev               # Yangi dev branch ochish va o'tish uchun
git switch main                 # Mavjud branchga o'tish uchun
git checkout dev                # Eski usulda dev branchga o'tish uchun
git branch -d dev               # Branchni o'chirish uchun (merge bo'lgan bo'lsa)
git branch -D dev               # Branchni majburan o'chirish uchun
```

## 3) Commit qilish oqimi

```bash
git add .                               # Barcha o'zgarishlarni staging'ga qo'shish uchun
git add <file>                          # Faqat bitta faylni qo'shish uchun
git commit -m "feat: add login page"   # Commit yaratish uchun
```

## 4) Push va pull

```bash
git push origin main               # Main branchni remote'ga yuborish uchun
git push -u origin dev             # Birinchi push va upstream ulash uchun
git push --all origin              # Barcha lokal branchlarni origin'ga yuborish uchun
git pull origin main               # Remote main'dan yangilanishlarni olish uchun
git fetch --all --prune            # Barcha remote ma'lumotlarni yangilash uchun
```

## 5) Repo klonlash

```bash
git clone <repo-url>                         # To'liq repo klonlash uchun
git clone -b <branch-name> <repo-url>        # Belgilangan branch bilan klonlash uchun
```

## 6) Remote (GitHub/GitLab) boshqaruvi

```bash
git remote -v                                        # Remote ro'yxatini ko'rish uchun
git remote add gitlab https://gitlab.com/user/repo.git
git remote remove gitlab
git remote remove origin                             # origin remote'ni olib tashlash uchun
```

GitHub repoga GitLab remote qo'shib parallel push qilish:

```bash
git remote add gitlab https://gitlab.com/user/repo.git
git push -u gitlab main
```

## 7) O'zgarishni qaytarish (restore/revert/reset)

### Fayl o'zgarishini bekor qilish (commitdan oldin)

```bash
git restore <file>     # Bitta fayldagi local o'zgarishni bekor qilish uchun
git restore .          # Barcha local o'zgarishni bekor qilish uchun
```

### Push qilingan commitni xavfsiz bekor qilish

```bash
git revert <commit-hash>
```

`revert` yangi commit yaratish va tarixni buzmasdan bekor qilish uchun.

### Oxirgi local commitni orqaga surish

```bash
git reset --soft HEAD~1   # Commitni ochib, o'zgarishlarni staging'da qoldirish uchun
git reset --mixed HEAD~1  # Commitni ochib, o'zgarishlarni working tree'da qoldirish uchun
git reset HEAD^           # Oxirgi commitni orqaga surib, o'zgarishlarni localda qoldirish uchun
```

### Xavfli buyruq (faqat aniq kerak bo'lsa)

```bash
git reset --hard origin/<branch>
```

Bu buyruq lokal commit va local o'zgarishlarni o'chirish uchun ishlaydi.

## 8) Stash (vaqtincha saqlash)

```bash
git stash push -m "wip: login page"    # O'zgarishlarni vaqtincha saqlash uchun
git stash list                          # Stashlar ro'yxatini ko'rish uchun
git stash show -p stash@{0}             # Stash ichini ko'rish uchun
git stash apply                         # Oxirgi stashni qo'llash uchun
git stash apply stash@{0}               # Stashni qo'llab, ro'yxatda saqlab qolish uchun
git stash pop                           # Stashni qo'llab, ro'yxatdan olib tashlash uchun
git stash drop stash@{0}                # Tanlangan stashni o'chirish uchun
```

## 9) Credential saqlash

```bash
git config --global credential.helper store
```

Bu usul login ma'lumotlarini diskda saqlash uchun.
