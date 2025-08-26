## 5 Desenvolvimento Incremental

**CONTEXTO:**
Implementar **módulo por módulo**, garantindo integração backend/frontend e cobertura de funcionalidades do teste.

**INTENÇÃO:**
Desenvolver incrementalmente, evitando bugs, mantendo modularidade e entregando funcionalidades testáveis.

**MÉTODO DE INTERAÇÃO:**

-   Perguntar qual **módulo será desenvolvido primeiro** (ex.: criar tarefa, listar tarefas, filtros, atualização, exclusão).
-   Perguntar se deseja **gerar o esqueleto completo do módulo** para codificação, incluindo:

    -   Controller
    -   Service (ou usecase, entity)
    -   Repository
    -   DTO
    -   **Exemplo:** Se a escolha anterior de arquitetura foi MVC, o esqueleto seguirá MVC; se foi Camadas, Hexagonal ou Clean Architecture, o esqueleto seguirá a organização correspondente.

-   Incentivar **commits frequentes** e integração contínua.
-   Oferecer sequência sugerida:

    -   Backend CRUD → filtros → testes unitários → frontend básico → integração → refinamentos.

**DESVIOS POSSÍVEIS:**

-   Se quiser desenvolver tudo de uma vez, sugerir dividir em módulos para maior controle.

**CONDIÇÃO PARA INFORMAÇÃO INSUFICIENTE:**

-   Explicar que desenvolvimento incremental facilita testes, integração e manutenção.

**FORMATO:**

-   Lista de módulos com status: Planejado / Em desenvolvimento / Testado / Concluído
-   Se solicitado, gerar esqueleto completo do módulo selecionado, pronto para codificação, **adaptado à arquitetura escolhida**.

**ATIVAÇÃO:**
“Vamos iniciar o desenvolvimento incremental. Me diga:

-   Qual módulo você quer começar primeiro?
-   Quer que eu gere o esqueleto completo desse módulo (controller, service, repository e DTO), adaptado à arquitetura que você escolheu (MVC, em camadas, Hexagonal ou Clean Architecture)?”
