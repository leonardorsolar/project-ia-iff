# Planejamento Técnico - Sistema de Registro de Usuários

## Tecnologias Backend

### Linguagem e Framework

-   **Python 3.8+**
-   **FastAPI** - Framework moderno para APIs, com documentação automática e alta performance
-   **Uvicorn** - Servidor ASGI para rodar a aplicação FastAPI

### Dependências Principais

```txt
fastapi==0.104.1
uvicorn==0.24.0
sqlalchemy==2.0.23
pydantic==2.5.0
python-multipart==0.0.6
```

## Banco de Dados

### Sistema de Persistência

-   **SQLite** - Banco leve e ideal para desenvolvimento/estudo
-   **SQLAlchemy 2.0** - ORM moderno com suporte a async/await
-   **Alembic** (opcional) - Para migrações de banco de dados

### Modelagem

-   Tabela `users` com campos: id (PK), name, email (unique), password

## Documentação da API

### Ferramentas

-   **Swagger UI** - Documentação interativa automática (nativa do FastAPI)
-   **Redoc** - Documentação alternativa (também nativa do FastAPI)
-   **README.md** - Documentação do projeto com instruções de instalação e uso

### Endpoints Documentados

-   `POST /users` - Criar usuário
-   `GET /users` - Listar usuários
-   Schemas de request/response definidos com Pydantic

## Estrutura de Pastas - Arquitetura em Camadas com Repository

```
projeto_usuarios/
├── app/
│   ├── __init__.py
│   ├── main.py                 # Ponto de entrada da aplicação
│   ├── models/                 # Modelos SQLAlchemy
│   │   ├── __init__.py
│   │   └── user.py
│   ├── schemas/                # Schemas Pydantic (DTOs)
│   │   ├── __init__.py
│   │   └── user.py
│   ├── repositories/           # Camada de acesso a dados
│   │   ├── __init__.py
│   │   └── user_repository.py
│   ├── services/               # Lógica de negócio
│   │   ├── __init__.py
│   │   └── user_service.py
│   ├── controllers/            # Controladores (handlers)
│   │   ├── __init__.py
│   │   └── user_controller.py
│   ├── routers/                # Definição de rotas
│   │   ├── __init__.py
│   │   └── user_router.py
│   ├── database/               # Configuração do banco
│   │   ├── __init__.py
│   │   └── connection.py
│   └── core/                   # Configurações globais
│       ├── __init__.py
│       └── config.py
├── tests/                      # Testes (opcional)
│   ├── __init__.py
│   └── test_users.py
├── requirements.txt            # Dependências
├── README.md                   # Documentação do projeto
└── .gitignore                  # Arquivos ignorados pelo Git
```

## Responsabilidades por Camada

### Router (`user_router.py`)

-   Define endpoints HTTP
-   Validação inicial de dados via Pydantic
-   Chama controllers apropriados

### Controller (`user_controller.py`)

-   Recebe requisições HTTP
-   Chama services para lógica de negócio
-   Retorna respostas HTTP formatadas

### Service (`user_service.py`)

-   Contém lógica de negócio
-   Validações de regras (email único, etc.)
-   Orquestra chamadas ao repository

### Repository (`user_repository.py`)

-   Acesso direto ao banco de dados
-   Operações CRUD básicas
-   Queries SQLAlchemy

### Models (`user.py`)

-   Definição da estrutura da tabela
-   Modelo SQLAlchemy

### Schemas (`user.py`)

-   DTOs para entrada e saída de dados
-   Validação de dados com Pydantic

## Roadmap de Desenvolvimento - Sprints

### Sprint 1: Configuração e Base (2-3 dias)

**Objetivo:** Configurar ambiente e estrutura básica

**Tarefas:**

-   [ ] Configurar ambiente virtual Python
-   [ ] Instalar dependências (FastAPI, SQLAlchemy, etc.)
-   [ ] Criar estrutura de pastas
-   [ ] Configurar conexão com SQLite
-   [ ] Criar modelo User (SQLAlchemy)
-   [ ] Configurar aplicação FastAPI básica
-   [ ] Testar se servidor sobe corretamente

**Entregável:** Aplicação rodando com estrutura montada

### Sprint 2: CRUD Básico (3-4 dias)

**Objetivo:** Implementar operações fundamentais

**Tarefas:**

-   [ ] Criar schemas Pydantic (UserCreate, UserResponse)
-   [ ] Implementar UserRepository (create, get_all, get_by_email)
-   [ ] Implementar UserService (create_user, get_users)
-   [ ] Implementar UserController (create, list)
-   [ ] Criar rotas POST /users e GET /users
-   [ ] Testar endpoints via Swagger

**Entregável:** API funcionando com criar e listar usuários

### Sprint 3: Validações e Melhorias (2-3 dias)

**Objetivo:** Adicionar validações e tratamento de erros

**Tarefas:**

-   [ ] Implementar validação de email único
-   [ ] Adicionar tratamento de erros personalizados
-   [ ] Melhorar mensagens de erro
-   [ ] Validar tamanhos mínimos (nome 2+ chars, senha 6+ chars)
-   [ ] Testar cenários de erro
-   [ ] Garantir que senhas não aparecem nas respostas

**Entregável:** API robusta com validações completas

### Sprint 4: Documentação e Finalização (1-2 dias)

**Objetivo:** Documentar e preparar para entrega

**Tarefas:**

-   [ ] Escrever README completo com instruções
-   [ ] Documentar endpoints no Swagger com exemplos
-   [ ] Adicionar comentários no código
-   [ ] Criar arquivo requirements.txt final
-   [ ] Preparar demonstração
-   [ ] Testar instalação do zero

**Entregável:** Projeto completo e documentado para entrega

## Cronograma Estimado

**Total:** 8-12 dias de desenvolvimento

| Sprint   | Duração  | Foco Principal         |
| -------- | -------- | ---------------------- |
| Sprint 1 | 2-3 dias | Setup e estrutura      |
| Sprint 2 | 3-4 dias | Funcionalidades core   |
| Sprint 3 | 2-3 dias | Validações e robustez  |
| Sprint 4 | 1-2 dias | Documentação e entrega |

## Comandos Úteis para Desenvolvimento

```bash
# Criar ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Instalar dependências
pip install -r requirements.txt

# Rodar aplicação
uvicorn app.main:app --reload

# Acessar documentação
# http://localhost:8000/docs (Swagger)
# http://localhost:8000/redoc (ReDoc)
```

## Critérios de Aceite por Sprint

### Sprint 1 ✅

-   [ ] Aplicação FastAPI rodando
-   [ ] Estrutura de pastas criada
-   [ ] Banco SQLite conectando

### Sprint 2 ✅

-   [ ] POST /users funcionando
-   [ ] GET /users funcionando
-   [ ] Swagger documentando endpoints

### Sprint 3 ✅

-   [ ] Email único validado
-   [ ] Erros retornando 400/422 apropriados
-   [ ] Senhas não expostas na listagem

### Sprint 4 ✅

-   [ ] README com instruções claras
-   [ ] Código comentado e organizado
-   [ ] Demonstração preparada

---

**Planejamento criado em:** Agosto 2025  
**Estimativa total:** 8-12 dias  
**Foco:** Aprendizado e boas práticas
