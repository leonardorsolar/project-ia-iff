# Configuração do Ambiente - Projeto poo-user

## 📂 Repositório GitHub

### Configuração Inicial

-   **Nome:** `poo-user`
-   **Visibilidade:** Público
-   **Descrição:** "Sistema de registro de usuários desenvolvido em Python com FastAPI - Projeto acadêmico de POO"
-   **Incluir:** README.md, .gitignore (Python template)

### Estrutura do Repositório

```
poo-user/
├── .gitignore                  # Arquivos ignorados pelo Git
├── README.md                   # Documentação do projeto
├── pyproject.toml              # Configuração Poetry + dependências
├── .env.example                # Exemplo de variáveis de ambiente
├── .flake8                     # Configuração do linter
├── pytest.ini                 # Configuração dos testes
├── app/                        # Código da aplicação
└── tests/                      # Testes automatizados
```

## 💻 IDE e Configuração VS Code

### Extensões Recomendadas

```json
{
    "recommendations": [
        "ms-python.python",
        "ms-python.flake8",
        "ms-python.black-formatter",
        "ms-vscode.vscode-json",
        "redhat.vscode-yaml",
        "bradlc.vscode-tailwindcss"
    ]
}
```

### Settings.json (VS Code)

```json
{
    "python.defaultInterpreterPath": ".venv/bin/python",
    "python.linting.enabled": true,
    "python.linting.flake8Enabled": true,
    "python.formatting.provider": "black",
    "python.formatting.blackArgs": ["--line-length=88"],
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.organizeImports": true
    }
}
```

## 📦 Gerenciamento de Dependências com Poetry

### pyproject.toml

```toml
[tool.poetry]
name = "poo-user"
version = "0.1.0"
description = "Sistema de registro de usuários com FastAPI"
authors = ["Seu Nome <seuemail@email.com>"]
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.8"
fastapi = "^0.104.1"
uvicorn = {extras = ["standard"], version = "^0.24.0"}
sqlalchemy = "^2.0.23"
pydantic = {extras = ["email"], version = "^2.5.0"}
python-multipart = "^0.0.6"
python-dotenv = "^1.0.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.4.3"
pytest-asyncio = "^0.21.1"
httpx = "^0.25.2"
flake8 = "^6.1.0"
black = "^23.11.0"
isort = "^5.12.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

[tool.black]
line-length = 88
target-version = ['py38']

[tool.isort]
profile = "black"
multi_line_output = 3
line_length = 88
```

### Comandos Poetry Essenciais

```bash
# Instalar Poetry (se não tiver)
curl -sSL https://install.python-poetry.org | python3 -

# Inicializar projeto
poetry init

# Instalar dependências
poetry install

# Ativar ambiente virtual
poetry shell

# Adicionar nova dependência
poetry add nome-da-dependencia

# Adicionar dependência de desenvolvimento
poetry add --group dev nome-da-dependencia

# Rodar comandos no ambiente virtual
poetry run python app/main.py
poetry run pytest
```

## 🧪 Configuração de Testes com pytest

### pytest.ini

```ini
[tool:pytest]
testpaths = tests
python_files = test_*.py
python_classes = Test*
python_functions = test_*
addopts =
    -v
    --tb=short
    --strict-markers
    --disable-warnings
    --cov=app
    --cov-report=term-missing
    --cov-report=html
```

### Estrutura de Testes

```
tests/
├── __init__.py
├── conftest.py                 # Configurações e fixtures
├── test_models/
│   ├── __init__.py
│   └── test_user.py
├── test_repositories/
│   ├── __init__.py
│   └── test_user_repository.py
├── test_services/
│   ├── __init__.py
│   └── test_user_service.py
└── test_controllers/
    ├── __init__.py
    └── test_user_controller.py
```

### conftest.py (Fixtures globais)

```python
import pytest
from fastapi.testclient import TestClient
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

from app.main import app
from app.database.connection import get_db
from app.models.user import Base

# Banco de teste em memória
SQLALCHEMY_DATABASE_URL = "sqlite:///./test.db"
engine = create_engine(SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False})
TestingSessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

@pytest.fixture(scope="function")
def db_session():
    Base.metadata.create_all(bind=engine)
    session = TestingSessionLocal()
    try:
        yield session
    finally:
        session.close()
        Base.metadata.drop_all(bind=engine)

@pytest.fixture(scope="function")
def client(db_session):
    def override_get_db():
        try:
            yield db_session
        finally:
            db_session.close()

    app.dependency_overrides[get_db] = override_get_db
    yield TestClient(app)
    app.dependency_overrides.clear()
```

## 🔍 Configuração de Linter com flake8

### .flake8

```ini
[flake8]
max-line-length = 88
extend-ignore =
    E203,  # whitespace before ':'
    E501,  # line too long (handled by black)
    W503,  # line break before binary operator
exclude =
    .git,
    __pycache__,
    .venv,
    .eggs,
    *.egg,
    build,
    dist
per-file-ignores =
    __init__.py:F401
```

### Comandos de Qualidade de Código

```bash
# Executar linter
poetry run flake8 app/

# Formatar código
poetry run black app/

# Organizar imports
poetry run isort app/

# Script completo de qualidade
poetry run black app/ && poetry run isort app/ && poetry run flake8 app/
```

## 🔐 Configuração de Variáveis de Ambiente

### .env.example

```env
# Database
DATABASE_URL=sqlite:///./users.db

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000
DEBUG=True

# Security (se implementar no futuro)
SECRET_KEY=your-secret-key-here

# Environment
ENVIRONMENT=development
```

### .env (arquivo real - não commitado)

```env
DATABASE_URL=sqlite:///./users.db
API_HOST=0.0.0.0
API_PORT=8000
DEBUG=True
SECRET_KEY=super-secret-development-key
ENVIRONMENT=development
```

### Carregamento no código

```python
# app/core/config.py
import os
from dotenv import load_dotenv

load_dotenv()

class Settings:
    DATABASE_URL: str = os.getenv("DATABASE_URL", "sqlite:///./users.db")
    API_HOST: str = os.getenv("API_HOST", "0.0.0.0")
    API_PORT: int = int(os.getenv("API_PORT", "8000"))
    DEBUG: bool = os.getenv("DEBUG", "True").lower() == "true"
    SECRET_KEY: str = os.getenv("SECRET_KEY", "dev-secret-key")

settings = Settings()
```

## 📋 Checklist de Configuração

### ✅ Repositório GitHub

-   [ ] Criar repositório `poo-user` público
-   [ ] Adicionar README.md inicial
-   [ ] Configurar .gitignore para Python
-   [ ] Fazer primeiro commit

### ✅ Ambiente Local

-   [ ] Instalar Poetry
-   [ ] Executar `poetry init`
-   [ ] Configurar pyproject.toml
-   [ ] Executar `poetry install`
-   [ ] Criar estrutura de pastas

### ✅ VS Code

-   [ ] Instalar extensões recomendadas
-   [ ] Configurar settings.json
-   [ ] Configurar interpretador Python do Poetry

### ✅ Qualidade de Código

-   [ ] Configurar .flake8
-   [ ] Testar linter: `poetry run flake8 --version`
-   [ ] Testar formatter: `poetry run black --version`

### ✅ Testes

-   [ ] Configurar pytest.ini
-   [ ] Criar estrutura de testes
-   [ ] Configurar conftest.py
-   [ ] Executar teste dummy: `poetry run pytest --version`

### ✅ Variáveis de Ambiente

-   [ ] Criar .env.example
-   [ ] Criar .env local
-   [ ] Configurar carregamento no código
-   [ ] Adicionar .env no .gitignore

## 🚀 Scripts de Desenvolvimento

### Makefile (opcional)

```makefile
.PHONY: install test lint format run

install:
	poetry install

test:
	poetry run pytest

lint:
	poetry run flake8 app/

format:
	poetry run black app/
	poetry run isort app/

quality: format lint

run:
	poetry run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

dev: quality test run
```

### Scripts no pyproject.toml

```toml
[tool.poetry.scripts]
dev = "uvicorn app.main:app --reload"
test = "pytest"
lint = "flake8 app/"
format = "black app/ && isort app/"
```

## 📚 README.md Inicial

````markdown
# poo-user

Sistema de registro de usuários desenvolvido em Python com FastAPI - Projeto acadêmico de Programação Orientada a Objetos.

## 🚀 Tecnologias

-   Python 3.8+
-   FastAPI
-   SQLAlchemy
-   SQLite
-   Poetry
-   Pytest

## 🛠️ Configuração

1. Clone o repositório:

```bash
git clone https://github.com/seuusuario/poo-user.git
cd poo-user
```
````

2. Instale as dependências:

```bash
poetry install
```

3. Configure variáveis de ambiente:

```bash
cp .env.example .env
```

4. Execute a aplicação:

```bash
poetry run uvicorn app.main:app --reload
```

5. Acesse a documentação:

-   Swagger UI: http://localhost:8000/docs
-   ReDoc: http://localhost:8000/redoc

## 🧪 Testes

```bash
poetry run pytest
```

## 📁 Estrutura do Projeto

```
app/
├── controllers/    # Controladores HTTP
├── services/       # Lógica de negócio
├── repositories/   # Acesso a dados
├── models/         # Modelos SQLAlchemy
├── schemas/        # Schemas Pydantic
└── core/          # Configurações
```

## 🎯 Funcionalidades

-   [x] Cadastro de usuários
-   [x] Listagem de usuários
-   [x] Validação de email único
-   [x] Documentação automática da API

## 📄 Licença

Este projeto é desenvolvido para fins acadêmicos.

````

## 🔄 Comandos de Workflow

### Setup Inicial Completo
```bash
# 1. Criar e entrar no diretório
mkdir poo-user && cd poo-user

# 2. Inicializar Git
git init
git remote add origin https://github.com/seuusuario/poo-user.git

# 3. Inicializar Poetry
poetry init

# 4. Instalar dependências
poetry install

# 5. Criar estrutura básica
mkdir -p app/{controllers,services,repositories,models,schemas,core,database,factories,routers}
mkdir -p tests/{test_controllers,test_services,test_repositories,test_models}

# 6. Primeiro commit
git add .
git commit -m "feat: configuração inicial do projeto"
git push -u origin main
````

### Workflow Diário

```bash
# Ativar ambiente virtual
poetry shell

# Executar qualidade de código
poetry run black app/ && poetry run isort app/ && poetry run flake8 app/

# Executar testes
poetry run pytest

# Rodar aplicação
poetry run uvicorn app.main:app --reload
```

---

**Ambiente configurado em:** Agosto 2025  
**Ferramentas:** Poetry, pytest, flake8, VS Code  
**Pronto para desenvolvimento!** 🚀
