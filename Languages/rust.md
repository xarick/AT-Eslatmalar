# Rust
Bu fayl Rust bilan ishlash uchun qisqa va amaliy buyruqlar to'plami.

## 1) `rustc` bilan oddiy ishga tushirish

```bash
rustc main.rs          # Bitta faylni compile qilish uchun
./main                 # Compile bo'lgan binary'ni ishga tushirish uchun
```

## 2) Cargo bilan yangi loyiha yaratish

Binary loyiha:

```bash
cargo new hello_world   # Yangi binary loyiha yaratish uchun
cd hello_world          # Loyiha papkasiga kirish uchun
```

Library loyiha:

```bash
cargo new --lib hello_lib   # Yangi library loyiha yaratish uchun
cd hello_lib                # Loyiha papkasiga kirish uchun
```

Test uchun library loyiha:

```bash
cargo new --lib hello_test   # Test uchun library loyiha yaratish uchun
cd hello_test                # Loyiha papkasiga kirish uchun
cargo test                   # Testlarni ishga tushirish uchun
```

## 3) Asosiy Cargo buyruqlari

```bash
cargo build          # Loyihani compile qilish uchun
cargo run            # Build va run ni birga bajarish uchun
cargo check          # Tez tekshiruv (full buildsiz) uchun
```

## 4) Dependency boshqaruvi

```bash
cargo add tokio      # Loyihaga dependency qo'shish uchun
```

## 5) `cargo-modules` bilan modul tahlili

Avval o'rnatish:

```bash
cargo install cargo-modules   # cargo-modules'ni global o'rnatish uchun
```

Keyin ishlatish:

```bash
cargo modules structure       # Modul strukturasi ko'rish uchun
cargo modules dependencies    # Modul bog'liqliklarini ko'rish uchun
cargo modules orphans         # Ishlatilmayotgan modullarni topish uchun
```
