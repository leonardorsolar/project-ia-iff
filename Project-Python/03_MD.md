# Modelagem e Design - Sistema de Registro de Usuários

## Modelo de Dados

### Entidade User

```python
User {
    id: Integer (Primary Key, Auto Increment)
    name: String (Not Null, Min 2 chars)
    email: String (Not Null, Unique, Valid Email Format)
    password: String (Not Null, Min 6 chars)
    created_at: DateTime (Auto Generated)
    updated_at: DateTime (Auto Updated)
}
```

### Relacionamentos

-   **Nenhum relacionamento** - Entidade única e independente
-   Estrutura simples e focada no CRUD básico

## Diagrama de Classes

```
┌─────────────────────────────────┐
│           UserModel             │
├─────────────────────────────────┤
│ + id: int                       │
│ + name: str                     │
│ + email: str                    │
│ + password: str                 │
│ + created_at: datetime          │
│ + updated_at: datetime          │
└─────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│       UserRepository            │
├─────────────────────────────────┤
│ + create(user_data)             │
│ + get_all()                     │
│ + get_by_email(email)           │
│ + exists_by_email(email)        │
└─────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│        UserService              │
├─────────────────────────────────┤
│ + create_user(user_data)        │
│ + get_all_users()               │
│ + validate_email_unique(email)  │
└─────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│       UserController            │
├─────────────────────────────────┤
│ + create_user(request)          │
│ + list_users()                  │
└─────────────────────────────────┘
```

## Estrutura de Pastas Detalhada

```
app/
├── __init__.py
├── main.py                     # Ponto de entrada (FastAPI app)
│
├── models/                     # SQLAlchemy Models
│   ├── __init__.py
│   └── user.py                 # UserModel (ORM)
│
├── schemas/                    # Pydantic Schemas (DTOs)
│   ├── __init__.py
│   └── user.py                 # UserCreateSchema, UserResponseSchema
│
├── repositories/               # Data Access Layer
│   ├── __init__.py
│   ├── base_repository.py      # Interface base (se necessário)
│   └── user_repository.py      # UserRepository
│
├── services/                   # Business Logic Layer
│   ├── __init__.py
│   └── user_service.py         # UserService
│
├── controllers/                # HTTP Request Handlers
│   ├── __init__.py
│   └── user_controller.py      # UserController
│
├── routers/                    # Route Definitions
│   ├── __init__.py
│   └── user_router.py          # FastAPI Router
│
├── database/                   # Database Configuration
│   ├── __init__.py
│   └── connection.py           # Database connection (Singleton)
│
├── core/                       # Core Configuration
│   ├── __init__.py
│   ├── config.py               # App settings
│   └── exceptions.py           # Custom exceptions
│
└── factories/                  # Factory Pattern
    ├── __init__.py
    └── user_factory.py         # UserFactory
```

## Separação de Responsabilidades

### 🌐 Router Layer (`user_router.py`)

**Responsabilidade:** Definir endpoints HTTP

```python
# Apenas define rotas e delega para controllers
@router.post("/users", response_model=UserResponseSchema)
@router.get("/users", response_model=List[UserResponseSchema])
```

### 🎮 Controller Layer (`user_controller.py`)

**Responsabilidade:** Manipular requests/responses HTTP

```python
# Recebe dados HTTP, chama services, retorna HTTP responses
def create_user(user_data: UserCreateSchema) -> UserResponseSchema
def list_users() -> List[UserResponseSchema]
```

### 🏢 Service Layer (`user_service.py`)

**Responsabilidade:** Lógica de negócio e validações

```python
# Regras de negócio, validações, orquestração
def create_user(user_data: UserCreateSchema) -> UserResponseSchema
def validate_email_unique(email: str) -> bool
```

### 💾 Repository Layer (`user_repository.py`)

**Responsabilidade:** Acesso a dados

```python
# Operações CRUD no banco de dados
def create(user_data: dict) -> UserModel
def get_all() -> List[UserModel]
def get_by_email(email: str) -> Optional[UserModel]
```

### 📊 Model Layer (`user.py`)

**Responsabilidade:** Estrutura de dados

```python
# Definição da tabela e mapeamento ORM
class UserModel(Base):
    __tablename__ = "users"
    # campos da tabela
```

## Padrões de Projeto Aplicados

### 🏭 Factory Pattern (`user_factory.py`)

**Objetivo:** Criar instâncias de User de forma padronizada

```python
class UserFactory:
    @staticmethod
    def create_user_from_schema(user_data: UserCreateSchema) -> dict:
        """Cria dicionário de user a partir do schema"""
        return {
            "name": user_data.name.strip(),
            "email": user_data.email.lower().strip(),
            "password": user_data.password
        }

    @staticmethod
    def create_response_from_model(user_model: UserModel) -> UserResponseSchema:
        """Converte model para response schema"""
        return UserResponseSchema(
            id=user_model.id,
            name=user_model.name,
            email=user_model.email,
            created_at=user_model.created_at
        )
```

### 🔒 Singleton Pattern (`connection.py`)

**Objetivo:** Garantir uma única instância de conexão com BD

```python
class DatabaseConnection:
    _instance = None
    _engine = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

    def get_engine(self):
        if self._engine is None:
            self._engine = create_engine("sqlite:///users.db")
        return self._engine
```

### 📚 Repository Pattern (`user_repository.py`)

**Objetivo:** Isolar acesso aos dados da lógica de negócio

```python
class UserRepository:
    def __init__(self, db_session):
        self.db = db_session

    def create(self, user_data: dict) -> UserModel:
        """Cria usuário no banco"""

    def get_all(self) -> List[UserModel]:
        """Lista todos os usuários"""

    def get_by_email(self, email: str) -> Optional[UserModel]:
        """Busca usuário por email"""
```

## Princípios SOLID Aplicados

### 🎯 **S - Single Responsibility Principle**

**Cada classe tem uma única responsabilidade:**

-   `UserController`: Apenas manipula HTTP
-   `UserService`: Apenas lógica de negócio
-   `UserRepository`: Apenas acesso a dados
-   `UserFactory`: Apenas criação de objetos

### 🔓 **D - Dependency Inversion Principle**

**Depender de abstrações, não de implementações:**

```python
# Service depende de interface, não implementação concreta
class UserService:
    def __init__(self, user_repository: UserRepositoryInterface):
        self.user_repository = user_repository

# Interface define contrato
class UserRepositoryInterface(ABC):
    @abstractmethod
    def create(self, user_data: dict) -> UserModel:
        pass
```

## Schemas/DTOs com Pydantic

### 📥 Input Schema (`UserCreateSchema`)

```python
from pydantic import BaseModel, EmailStr, Field

class UserCreateSchema(BaseModel):
    name: str = Field(..., min_length=2, description="Nome do usuário")
    email: EmailStr = Field(..., description="Email único do usuário")
    password: str = Field(..., min_length=6, description="Senha do usuário")

    class Config:
        json_schema_extra = {
            "example": {
                "name": "João Silva",
                "email": "joao@email.com",
                "password": "123456"
            }
        }
```

### 📤 Output Schema (`UserResponseSchema`)

```python
from datetime import datetime

class UserResponseSchema(BaseModel):
    id: int
    name: str
    email: str
    created_at: datetime

    class Config:
        from_attributes = True  # Para compatibilidade com SQLAlchemy
```

## Estratégia de Tratamento de Erros

### 🚨 Custom Exceptions (`exceptions.py`)

```python
class UserAlreadyExistsError(Exception):
    """Erro quando email já está cadastrado"""
    def __init__(self, email: str):
        self.email = email
        super().__init__(f"Usuário com email {email} já existe")

class UserValidationError(Exception):
    """Erro de validação de dados do usuário"""
    pass

class DatabaseError(Exception):
    """Erro relacionado ao banco de dados"""
    pass
```

### 🛡️ Error Handling Pattern

```python
# No Service Layer
def create_user(self, user_data: UserCreateSchema) -> UserResponseSchema:
    try:
        # Validar email único
        if self.user_repository.get_by_email(user_data.email):
            raise UserAlreadyExistsError(user_data.email)

        # Criar usuário
        user_dict = UserFactory.create_user_from_schema(user_data)
        user_model = self.user_repository.create(user_dict)

        return UserFactory.create_response_from_model(user_model)

    except UserAlreadyExistsError:
        raise  # Re-raise para o controller tratar
    except Exception as e:
        raise DatabaseError(f"Erro ao criar usuário: {str(e)}")

# No Controller Layer
def create_user(self, user_data: UserCreateSchema):
    try:
        user = self.user_service.create_user(user_data)
        return {"status": "success", "data": user}
    except UserAlreadyExistsError as e:
        raise HTTPException(status_code=400, detail=str(e))
    except DatabaseError as e:
        raise HTTPException(status_code=500, detail="Erro interno do servidor")
```

## Fluxo de Dados Completo

```
📱 HTTP Request (POST /users)
    ↓
🌐 Router (user_router.py)
    ↓ (UserCreateSchema)
🎮 Controller (user_controller.py)
    ↓ (UserCreateSchema)
🏢 Service (user_service.py)
    ↓ (dict via Factory)
💾 Repository (user_repository.py)
    ↓ (UserModel)
🗄️ Database (SQLite)
    ↓ (UserModel)
💾 Repository
    ↓ (UserModel)
🏢 Service (via Factory)
    ↓ (UserResponseSchema)
🎮 Controller
    ↓ (JSON Response)
🌐 Router
    ↓
📱 HTTP Response
```

## Benefícios da Arquitetura Escolhida

### ✅ **Manutenibilidade**

-   Cada camada tem responsabilidade bem definida
-   Fácil de localizar e corrigir problemas
-   Código organizedo e legível

### ✅ **Testabilidade**

-   Cada camada pode ser testada independentemente
-   Mocks fáceis de implementar via interfaces
-   Testes unitários focados

### ✅ **Extensibilidade**

-   Novos recursos seguem o mesmo padrão
-   Fácil adicionar novas funcionalidades
-   Principios SOLID facilitam evolução

### ✅ **Escalabilidade**

-   Arquitetura suporta crescimento
-   Padrões facilitam trabalho em equipe
-   Base sólida para projetos maiores

---

**Modelagem criada em:** Agosto 2025  
**Padrões aplicados:** Factory, Singleton, Repository  
**Princípios:** SOLID (S + D), DRY, KISS
