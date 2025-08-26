# PRD: Registro de Usuário

## Visão Geral

A funcionalidade **Registrar Usuário** será implementada para atender a um trabalho escolar.  
O objetivo é permitir o cadastro de usuários e oferecer operações básicas de **CRUD (Create, Read, Update, Delete)**.

Embora não haja um time ou cliente externo envolvido (apenas o autor do projeto), a implementação terá papel fundamental para demonstrar boas práticas de desenvolvimento de sistemas, incluindo persistência de dados, autenticação inicial e gerenciamento básico de usuários.

Essa iniciativa resolve o problema de **não ter um controle estruturado de usuários** dentro do sistema, garantindo que seja possível:

-   Adicionar novos usuários
-   Consultar dados já registrados
-   Alterar informações quando necessário
-   Excluir registros que não são mais úteis

## Escopo

**Escopo In (dentro):**

-   Cadastro de usuário com nome, e-mail e senha
-   Listagem de todos os usuários
-   Atualização de dados básicos
-   Exclusão de usuários

**Escopo Out (fora):**

-   Login com autenticação avançada (OAuth, Google, etc.)
-   Recuperação de senha
-   Perfis complexos com permissões diferenciadas
-   Integração com redes sociais

## Personas

-   **Professor** 👨‍🏫  
    Utilizará o sistema para avaliar a implementação do CRUD de usuários, validando se o registro, listagem, atualização e exclusão estão funcionando corretamente.

-   **Alunos da Sala** 👩‍🎓👨‍🎓  
    Poderão se registrar como usuários para testar a aplicação, interagir com o CRUD e compreender como funciona a gestão de dados em um sistema real.

-   **Desenvolvedor (Você)** 👨‍💻  
    Responsável por construir o sistema, gerenciar os dados e realizar ajustes técnicos conforme necessário. Também utilizará a aplicação para demonstrar as funcionalidades implementadas.

## Requisitos Funcionais

1. O sistema deve permitir o **cadastro de novos usuários** com nome, e-mail e senha.
2. O sistema deve permitir a **listagem de todos os usuários registrados**.
3. O sistema deve permitir a **edição dos dados** de um usuário já registrado.
4. O sistema deve permitir a **exclusão de um usuário**.
5. O sistema deve validar que o **e-mail seja único** (não pode haver duplicados).
6. O sistema deve validar que o **e-mail esteja em formato válido**.
7. O sistema deve validar que a **senha tenha no mínimo 6 caracteres**.
8. O sistema deve exibir **mensagens de erro claras** em caso de falha no cadastro, atualização ou exclusão.
9. O sistema deve impedir operações inválidas, como tentar excluir um usuário inexistente.
10. O sistema deve registrar e tratar erros inesperados, retornando uma resposta adequada sem quebrar a aplicação.

## Requisitos Não Funcionais

**Tecnologia:**

-   O sistema será desenvolvido em **Node.js com Express e TypeScript**.
-   O banco de dados será **SQLite**.
-   O sistema exporá uma **API REST documentada**, utilizando Swagger/OpenAPI.

**Performance:**

-   O CRUD deve responder em até **2 segundos** para operações básicas.
-   O sistema deve suportar pelo menos **20 usuários cadastrados simultaneamente**, suficiente para o contexto da turma.

**Qualidade:**

-   O código deve seguir **boas práticas de organização**, podendo utilizar **camadas claras ou MVC**.
-   O sistema deve retornar **mensagens claras de sucesso ou erro** para o usuário.
-   Deve haver **tratamento de erros** para evitar falhas inesperadas durante a operação da aplicação.

## Fluxo de Usuário

1. **Acesso ao sistema**

    - O aluno abre a aplicação para acessar a funcionalidade de registro.

2. **Preenchimento do formulário de cadastro**

    - O aluno insere **nome, e-mail e senha** nos campos correspondentes.

3. **Validação dos dados**

    - O sistema verifica se o **e-mail é único** e possui **formato válido**.
    - O sistema verifica se a **senha atende ao requisito mínimo de 6 caracteres**.

4. **Confirmação ou mensagem de erro**

    - Se os dados estiverem corretos, o usuário é cadastrado com sucesso e recebe uma **mensagem de confirmação**.
    - Se houver erro (e-mail duplicado, senha inválida, etc.), o sistema exibe **mensagem clara de erro** e permite correção.

5. **Listagem de usuários cadastrados**

    - O aluno pode visualizar todos os usuários registrados no sistema.

6. **Edição de dados**

    - O aluno seleciona um registro existente para **atualizar nome, e-mail ou senha**, com validação aplicada novamente.

7. **Exclusão de usuário**
    - O aluno pode **remover um registro**, recebendo confirmação antes da exclusão.

## Métricas de Sucesso

### Critérios Técnicos:

-   Todas as operações CRUD funcionando corretamente (POST e GET implementados)
-   Validações retornando erros apropriados (400, 422) com mensagens claras
-   API documentada e acessível via Swagger/OpenAPI integrado ao Node.js/Express + TypeScript
-   Tempo de resposta dentro do limite estabelecido (máximo 2 segundos)

### Critérios Acadêmicos:

-   Demonstração funcional das operações durante apresentação
-   Código seguindo boas práticas de estruturação e organização
-   Documentação clara dos endpoints com exemplos de uso
-   Implementação demonstra compreensão dos conceitos CRUD

### Indicadores de Sucesso:

-   Usuários podem ser cadastrados com validações funcionais
-   Listagem retorna dados corretos sem expor senhas
-   Swagger UI permite testar todos os endpoints
-   Projeto demonstra aplicação prática dos conceitos estudados

## Anexos / Observações

-   Estruturar o projeto seguindo **padrões de organização de código**.

**Referências:**

-   Documentação oficial **Node.js**
-   Material da disciplina sobre **APIs REST**
-   Guias de boas práticas para estruturação de projetos **Python** (para referência de organização e padrões de código)
