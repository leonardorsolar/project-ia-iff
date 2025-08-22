## 3 Modelagem e Design (Atualizado)

**CONTEXTO:**
Antes de codificar, é necessário criar **modelos de dados, diagrama de classes, estrutura de pastas, responsabilidades, padrões de projeto, uso de schemas/DTOs e tratamento de erros**.

**INTENÇÃO:**
Garantir arquitetura clara, modular e fácil de evoluir, contemplando **entidades de tarefas, status, filtragem, fluxo de dados, validação e manejo de exceções**.

**MÉTODO DE INTERAÇÃO:**

-   Solicitar descrição das **entidades e atributos** (ex.: Tarefa → título, descrição, status).

-   Perguntar sobre **relacionamentos** entre entidades se houver.

-   Perguntar sobre **separação de responsabilidades** (ex.: modelos, serviços, controladores).

-   Perguntar sobre **estrutura de pastas desejada**, com exemplos:

    -   **MVC:** Model, View, Controller
    -   **Camadas Simplificada (Service Layer):** Router, Controller, Service
    -   **Camadas com Repository:** Router, Controller, Service, Repository- separa lógica de negócio e persistência
    -   **Em Camadas:** apresentação, aplicação, domínio e infraestrutura – separa responsabilidades
    -   **Hexagonal:** isolamento da lógica de negócio de interfaces externas
    -   **Clean Architecture:** regras de negócio independentes de frameworks

-   Perguntar se deseja incluir **padrões de projeto** (exemplos para facilitar a escolha):

    -   **Singleton:** garantir uma única instância de uma classe
    -   **Factory:** criar objetos sem expor lógica de criação
    -   **Observer:** reagir a mudanças em objetos
    -   **Strategy:** permitir escolha de algoritmos dinamicamente

-   Perguntar se deseja aplicar **Princípios de Design**:

    -   **SOLID** (Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion)
    -   **DRY** (Don’t Repeat Yourself)
    -   **KISS** (Keep It Simple, Stupid)

-   Perguntar se a aplicação irá utilizar **schemas/DTOs para validação e transporte de dados**, com exemplos simples:

    -   **Com DTO/schema:** Python `pydantic.BaseModel`, TypeScript `interface` ou `class`, validação automática de tipos e campos.
    -   **Sem DTO/schema:** trabalhar diretamente com objetos/JSON, sem validação formal.

-   Perguntar **qual abordagem será utilizada para tratamento de erros/exceções**, com exemplos:

    -   **Imperativa tradicional:** try/catch (Java, C#) ou try/except (Python)
    -   **Funcional moderna:** Result / Either (Haskell, Rust, TypeScript funcional)

-   Oferecer exemplos visuais: diagrama de classes simples, estrutura de pastas backend/frontend.

**DESVIOS POSSÍVEIS:**

-   Se usuário não souber modelar, sugerir modelo CRUD básico com arquitetura MVC simples, padrões mínimos (Singleton ou Factory), DTOs simples e tratamento de erros tradicional.

**CONDIÇÃO PARA INFORMAÇÃO INSUFICIENTE:**

-   Explicar que sem modelagem clara, padrões de projeto, estratégia de tratamento de erros e validação via DTO/schema, o código pode se tornar confuso, difícil de manter e testar.

**FORMATO:**

-   Seção com: Modelos de dados, Diagrama de classes, Estrutura de pastas, Separação de responsabilidades, Padrões de projeto, Princípios de design, Uso de schemas/DTOs, Estratégia de tratamento de erros

**ATIVAÇÃO:**
“Vamos definir modelagem e design do projeto. Me diga:

-   Quais entidades e atributos a aplicação terá?
-   Como essas entidades se relacionam?
-   Como pretende organizar pastas e responsabilidades? (ex.: MVC, em camadas, hexagonal, clean architecture)
-   Deseja aplicar padrões de projeto? (ex.: Singleton, Factory, Observer, Strategy)
-   Deseja seguir princípios de design? (SOLID, DRY, KISS)
-   A aplicação irá utilizar schemas/DTOs para validação e transporte de dados ou será feita sem? (ex.: Python pydantic.BaseModel / TypeScript interface ou trabalhar direto com objetos)
-   Qual abordagem será utilizada para tratamento de erros/exceções? (Imperativa tradicional: try/catch ou try/except / Funcional moderna: Result / Either)”
