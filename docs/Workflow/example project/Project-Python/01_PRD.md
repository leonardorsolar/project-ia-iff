# PRD - Sistema de Registro de Usuários

## Visão Geral

Esta funcionalidade visa implementar um sistema básico de registro de usuários como parte de um estudo prático de operações CRUD (Create, Read, Update, Delete). O objetivo é desenvolver um backend que demonstre as melhores práticas de desenvolvimento, incluindo validação de dados, segurança básica e estruturação de APIs REST.

O sistema servirá como base de aprendizado para conceitos fundamentais como persistência de dados, validação de entrada, tratamento de erros e arquitetura de APIs.

## Escopo (In/Out)

### IN (Incluído):

-   Cadastro com email, nome e senha
-   Listagem de todos os usuários
-   Validação de email único

### OUT (Excluído):

-   Sistema de login/autenticação
-   Interface web (frontend)
-   Sistema de recuperação de senha
-   Criptografia de senha

## Personas

### Persona 1: Professor da Disciplina

-   Avaliará a implementação técnica das operações CRUD
-   Testará os endpoints da API para verificar funcionalidades
-   Analisará a qualidade do código e aderência às melhores práticas
-   Espera documentação clara dos endpoints

### Persona 2: Alunos (Colegas de Classe)

-   Podem testar o sistema durante apresentações ou demonstrações
-   Inserirão dados de teste nos formulários de cadastro
-   Verificarão se as validações estão funcionando corretamente
-   Utilizarão dados pessoais fictícios para testes

## Requisitos Funcionais

### RF001 - Criar Usuário (POST)

-   O sistema deve aceitar nome (obrigatório, mínimo 2 caracteres), email (formato válido, único) e senha (mínimo 6 caracteres)
-   Se email já existir, retornar erro 400 com mensagem apropriada
-   Em caso de sucesso, retornar status de sucesso (201) com dados do usuário criado
-   Validar formato de email antes de salvar no banco

### RF002 - Listar Usuários (GET)

-   A listagem deve retornar id, nome e email de todos os usuários
-   Não deve expor senhas na resposta
-   Retornar todos os usuários cadastrados sem paginação
-   Em caso de sucesso, retornar status 200

## Requisitos Não Funcionais

### RNF001 - Tecnologia

-   Linguagem: Python
-   Framework: FastAPI
-   Documentação automática da API com Swagger (integrada ao FastAPI)

### RNF002 - Performance

-   Tempo de resposta máximo de 2 segundos para qualquer operação
-   Sistema deve responder adequadamente para fins acadêmicos

### RNF003 - Qualidade

-   Código deve seguir boas práticas de estruturação
-   Documentação automática dos endpoints via Swagger/OpenAPI
-   Tratamento adequado de erros com mensagens claras

## Fluxo de Usuário

### FLUXO 1 - Cadastrar Usuário (POST /users)

1. API recebe requisição POST com dados (nome, email, senha)
2. Valida campos obrigatórios e formatos
3. Verifica se email já existe no banco de dados
4. Se validações passarem: salva usuário no banco
5. Retorna usuário criado (sem senha) com status 201

#### Cenários de Erro - Cadastro:

-   Campos inválidos → Retorna erro 422 com detalhes da validação
-   Email duplicado → Retorna erro 400 com mensagem "Email já cadastrado"

### FLUXO 2 - Listar Usuários (GET /users)

1. API recebe requisição GET
2. Busca todos os usuários no banco de dados
3. Filtra campos sensíveis (remove senhas)
4. Retorna lista de usuários com status 200

#### Cenário - Lista Vazia:

-   Se não há usuários → Retorna array vazio [] com status 200

## Métricas de Sucesso

### Critérios Técnicos:

-   Todas as operações CRUD funcionando corretamente (POST e GET implementados)
-   Validações retornando erros apropriados (400, 422) com mensagens claras
-   API documentada e acessível via Swagger/OpenAPI integrado ao FastAPI
-   Tempo de resposta dentro do limite estabelecido (máximo 2 segundos)

### Critérios Acadêmicos:

-   Demonstração funcional das operações durante apresentação
-   Código seguindo boas práticas de estruturação e organização
-   Documentação clara dos endpoints com exemplos de uso
-   Implementação demonstra compreensão dos conceitos CRUD

### Indicadores de Sucesso:

-   ✅ Usuários podem ser cadastrados com validações funcionais
-   ✅ Listagem retorna dados corretos sem expor senhas
-   ✅ Swagger UI permite testar todos os endpoints
-   ✅ Projeto demonstra aplicação prática dos conceitos estudados

## Anexos/Observações

### Observações Técnicas:

-   Usar SQLAlchemy para ORM (Object-Relational Mapping)
-   Implementar validação com Pydantic (nativo do FastAPI)
-   Estruturar projeto seguindo padrões de organização de código
-   Utilizar recursos nativos do FastAPI para documentação automática

### Referências:

-   Documentação oficial do FastAPI
-   Material da disciplina sobre APIs REST
-   Documentação do SQLAlchemy para modelagem de dados
-   Guias de boas práticas para estruturação de projetos Python

### Considerações do Projeto:

-   Projeto focado em aprendizado e demonstração de conceitos
-   Simplicidade priorizando clareza sobre complexidade
-   Código deve ser legível para avaliação acadêmica

---

**Documento gerado pelo ProductBuddy 🛠️**  
_Data: Agosto 2025_
