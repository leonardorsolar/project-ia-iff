# PRD – Registrar Usuário

## Visão Geral

A funcionalidade **“Registrar Usuário”** tem como objetivo permitir que o usuário crie uma conta no sistema, servindo como estudo prático para aprendizado de desenvolvimento de projetos e aplicação de boas práticas de programação. Esta iniciativa busca ensinar conceitos de cadastro, validação de dados e estruturação de um fluxo completo de registro, oferecendo uma base sólida para futuros estudos e projetos mais complexos.

## Escopo (In / Out)

**In (dentro do escopo):**

-   Campos de cadastro (ex.: nome, e-mail, senha)
-   Validação de e-mail
-   Feedback de sucesso ou falha no cadastro

**Out (fora do escopo):**

-   Login de usuário
-   Recuperação de senha
-   Integração com redes sociais

## Personas

1. **Professor da disciplina**

    - Papel: Avaliar o projeto e verificar a aplicação de boas práticas no desenvolvimento.
    - Objetivos: Confirmar que o estudante entende os conceitos de POO e boas práticas de programação.
    - Necessidades: Ter acesso ao sistema para testar o registro de usuários e avaliar o funcionamento correto.

2. **Aluno (desenvolvedor)**

    - Papel: Criar e testar a funcionalidade de registro de usuários.
    - Objetivos: Aprender a desenvolver um projeto, aplicar boas práticas e compreender validação de dados e feedbacks.
    - Necessidades: Um ambiente de estudo funcional, com campos de cadastro, validação de e-mail e feedback de sucesso/falha.

## Requisitos Funcionais

1. O sistema deve permitir cadastrar **nome, e-mail e senha**.
2. O sistema deve **validar se o e-mail já está cadastrado** antes de concluir o registro.
3. O sistema deve **exibir mensagens de sucesso ou erro** após a tentativa de cadastro.

## Requisitos Não Funcionais

1. O sistema deve ser **responsivo** e funcionar em diferentes dispositivos (computador, tablet, celular).
2. O tempo de resposta do cadastro deve ser **rápido**, idealmente menor que 2 segundos.
3. Os dados do usuário devem ser **armazenados de forma segura**, garantindo confidencialidade e integridade.
4. O código deve seguir **boas práticas de programação**, incluindo clareza, organização, comentários quando necessário e padronização de nomes de variáveis e funções.

## Fluxo de Usuário

1. **Acessar página de cadastro:** O usuário abre a página ou tela de registro.
2. **Preencher formulário:** O usuário informa **nome, e-mail e senha**.
3. **Enviar formulário:** O usuário clica no botão de **cadastrar**.
4. **Validação de dados:** O sistema verifica se os campos estão preenchidos corretamente e se o e-mail já está cadastrado.
5. **Feedback ao usuário:**

    - Se o cadastro for **bem-sucedido**, exibe mensagem de sucesso.
    - Se houver **erro**, exibe mensagem informando o problema.

6. **Conclusão:** O usuário é notificado do resultado e o sistema se prepara para novas interações ou login futuro (fora do escopo atual).

## Métricas de Sucesso

1. O cadastro deve ser realizado com **100% de sucesso nos testes corretos**.
2. O **tempo médio de cadastro** deve ser inferior a 2 segundos.
3. Todas as **mensagens de erro** devem ser claras, corretas e informativas.
4. O código deve seguir **boas práticas de programação**, facilitando manutenção e compreensão.

## Anexos / Observações

1. **Referências e aprendizado:**

    - Materiais da disciplina de **Projeto Orientado a Objetos**.
    - Tutoriais sobre **validação de formulários** e boas práticas de programação.

2. **Notas de implementação:**

    - Utilizar **frameworks ou bibliotecas** que facilitem a validação de e-mail e feedback ao usuário.
    - Estruturar o código de forma modular para **reuso e manutenção**.

3. **Ideias futuras (fora do escopo atual):**

    - Implementar **login e recuperação de senha**.
    - Integração com **redes sociais** para cadastro rápido.
    - Implementar **campos adicionais**, como telefone ou endereço.

4. **Observações gerais:**

    - Este projeto é **individual** e tem caráter **educacional**, focando em aprendizado de boas práticas e estruturação de fluxo de cadastro.
