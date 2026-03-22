# FastAPI
Bu fayl `uv` bilan FastAPI loyihasini yaratish va yuritish bo'yicha amaliy eslatma.

## 1) `uv` o'rnatish

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh      # uv o'rnatish uchun
uv --help                                             # Buyruqlarni ko'rish uchun
```

## 2) Yangi FastAPI loyiha yaratish

```bash
uv init backend                                       # Yangi loyiha yaratish uchun
cd backend                                            # Loyiha papkasiga kirish uchun
uv python pin 3.12                                    # Python versiyasini mahkamlash uchun
```

Asosiy kutubxonalar:

```bash
uv add "fastapi[standard]" pydantic pydantic-settings
uv add sqlalchemy "psycopg[binary]" python-dotenv httpx redis alembic
uv add --dev ruff mypy pytest pytest-cov
uv sync                                               # Dependency'larni sinxronlash uchun
```

## 3) Loyihani ishga tushirish

`src/apps/api/main.py` bo'lsa:

```bash
uv run uvicorn --app-dir src apps.api.main:app --reload --host 0.0.0.0 --port 8000
```

`app/main.py` bo'lsa:

```bash
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

`src/app/main.py` bo'lsa:

```bash
uv run uvicorn --app-dir src app.main:app --reload --host 0.0.0.0 --port 8000
```

FastAPI CLI bilan:

```bash
uv run fastapi dev
```

## 4) `uv` bo'yicha foydali buyruqlar

```bash
uv pip install -e .                                  # Editable install uchun
uv init --python 3.12                                # Python versiyasi bilan init qilish uchun
uv add "requests==2.31.0"                            # Aniq versiyadagi paket qo'shish uchun
uv remove fastapi                                    # Paketni olib tashlash uchun
uv lock --upgrade-package fastapi                    # Bitta paketni yangilash uchun
uv lock --upgrade                                    # Lock faylni to'liq yangilash uchun
uv sync --frozen                                     # Lock bo'yicha qat'iy sinxronlash uchun
uv sync --frozen --no-dev                            # Prod/CI uchun dev paketlarsiz sinxronlash uchun
uv venv                                              # Virtual environment yaratish uchun
source .venv/bin/activate                            # Linux/macOS da venv aktivlashtirish uchun
uv tree                                              # Dependency daraxtini ko'rish uchun
uv run <script-name>                                 # Skript ishga tushirish uchun
uv pip compile pyproject.toml -o requirements.txt    # requirements.txt generatsiya qilish uchun
uv python pin 3.11                                   # Python versiyasini almashtirish uchun
```

## 5) Lint, type check, test

```bash
uv run ruff check .                                  # Lint tekshiruv uchun
uv run ruff format .                                 # Kodni formatlash uchun
uv run mypy app                                      # Type check uchun
uv run pytest -q                                     # Testlarni ishga tushirish uchun
```

## 6) `pyproject.toml` script namuna

```toml
[tool.uv.scripts]
dev = "uvicorn app.main:app --reload --host 0.0.0.0 --port 8000"
test = "pytest -v"
lint = "ruff check ."
typecheck = "mypy app"
```

Ishlatish:

```bash
uv run dev
uv run test
uv run lint
uv run typecheck
```

## 7) Alembic migratsiya

```bash
uv run alembic init alembic                          # Alembic init qilish uchun
uv run alembic revision --autogenerate -m "init"    # Migratsiya yaratish uchun
uv run alembic upgrade head                          # Oxirgi migratsiyagacha ko'tarish uchun
```

## 8) Auth/form uchun qo'shimcha paketlar

```bash
uv add passlib[argon2] argon2-cffi                  # Parol hash uchun
uv add python-jose[cryptography]                    # JWT token bilan ishlash uchun
uv add python-multipart                             # Form-data bilan ishlash uchun
```
