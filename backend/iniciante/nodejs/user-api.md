# Desafio NodeJS Iniciante - User API

* [Propósito](#--prop-sito--)
* [Requisitos](#--requisitos--)
* [Opcionais (Fortemente Recomendados)](#--opcionais--fortemente-recomendados---)
* [Critérios de Avaliação](#--crit-rios-de-avalia--o--)

## **Propósito**

Este desafio tem como objetivo auxiliar pessoas desenvolvedoras que buscam oportunidades no mercado de trabalho ou desejam aprimorar suas habilidades em NodeJS. A UserAPI proporciona a chance de explorar autenticação, manipulação de banco de dados, criação de APIs RESTful, teste unitário, documentação com Swagger, middlewares, variáveis de ambiente, versionamento com Git e, opcionalmente, o uso de Docker.

## **Requisitos**

1. **Autenticação:**
    - Implemente um sistema de autenticação com JWT (JSON Web Tokens).
    - Utilize pacotes como **`jsonwebtoken`** para a geração e verificação de tokens.
    - Utilize a biblioteca **`bcrypt`** para garantir a segurança das senhas.
2. **Conexão com Banco de Dados:**
    - Utilize um banco de dados SQL, como PostgreSQL, e o pacote **`pg`** para estabelecer a conexão.
    - Crie uma tabela "users" com campos como ID, nome, e-mail, senha, etc.
    - Considere o uso do ORM **`Sequelize`** para facilitar a interação com o banco de dados.
3. **RESTful API:**
    - Desenvolva uma API RESTful com os seguintes casos de uso:
        1. **Registrar Usuário:**
            - **Ator Principal:** Novo Usuário.
            - **Fluxo Principal:**
                1. O usuário fornece nome, e-mail e senha.
                2. O sistema cria um novo registro de usuário no banco de dados.
        2. **Autenticar Usuário:**
            - **Ator Principal:** Sistema de Autenticação.
            - **Fluxo Principal:**
                1. O usuário fornece e-mail/senha.
                2. O sistema verifica as credenciais.
                3. Se válidas, o sistema gera um token JWT.
        3. **Obter Dados do Usuário Autenticado:**
            - **Ator Principal:** Usuário autenticado.
            - **Fluxo Principal:**
                1. O usuário envia uma solicitação para seus próprios dados.
                2. O sistema verifica o token JWT e retorna os dados.
        4. **Atualizar Dados do Usuário:**
            - **Ator Principal:** Usuário autenticado.
            - **Fluxo Principal:**
                1. O usuário envia uma solicitação para atualizar seus dados.
                2. O sistema verifica o token JWT e atualiza os dados.
        5. **Listar Usuários (Apenas para Administradores):**
            - **Ator Principal:** Administrador.
            - **Fluxo Principal:**
                1. O administrador solicita a lista de usuários.
                2. O sistema verifica o token JWT e retorna a lista (se o usuário for um administrador).
        6. **Excluir Usuário (Apenas para Administradores):**
            - **Ator Principal:** Administrador.
            - **Fluxo Principal:**
                1. O administrador solicita a exclusão de um usuário.
                2. O sistema verifica o token JWT e exclui o usuário do banco de dados (se o usuário for um administrador).
    - Considere alternativas ao framework Express.js, como Fastify ou Koa.js, para criar as rotas.
    - Utilize o middleware **`body-parser`** para facilitar o tratamento de dados JSON nas requisições.
    - Utilize middlewares para validação de token JWT em rotas protegidas e para tratamento de erros.
4. **Uso de Middlewares:**
    - Implemente um middleware para autenticação baseada em JWT.
    - Crie um middleware para tratamento de erros, fornecendo mensagens amigáveis e códigos HTTP apropriados.
    - Exemplo: Middleware de Autenticação
        
        ```jsx
        javascriptCopy code
        const jwt = require('jsonwebtoken');
        
        function authenticateJWT(req, res, next) {
          const token = req.header('Authorization');
          if (!token) return res.status(401).json({ message: 'Unauthorized' });
        
          jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
            if (err) return res.status(403).json({ message: 'Forbidden' });
            req.user = user;
            next();
          });
        }
        
        // Uso do Middleware
        app.get('/api/private', authenticateJWT, (req, res) => {
          // Rota protegida
          res.json({ message: 'Authenticated' });
        });
        
        ```
        
5. **Tratamento de Erro:**
    - Implemente um tratamento de erro consistente em toda a aplicação.
    - Forneça mensagens de erro claras e códigos HTTP apropriados em caso de falhas.
6. **Variáveis de Ambiente:**
    - Utilize o pacote **`dotenv`** para carregar variáveis de ambiente a partir de um arquivo **`.env`**.
    - Exemplo:
        - Crie um arquivo **`.env`** na raiz do projeto:
            
            ```makefile
            makefileCopy code
            PORT=3000
            DATABASE_URL=postgres://usuario:senha@localhost:5432/nome-do-banco
            JWT_SECRET=seuSegredoJWT
            
            ```
            
7. **Git:**
    - Inicie um repositório Git para o projeto.
    - Faça commits incrementais, mantendo uma boa mensagem de commit.
    - Crie um arquivo **`.gitignore`** para excluir arquivos desnecessários do repositório.
8. **README Detalhado:**
    - Forneça um README detalhado explicando o propósito do projeto, como configurar o ambiente de desenvolvimento e iniciar o projeto.
    - Inclua exemplos claros de como realizar as principais operações, como registro, login, e manipulação de usuários.
    - Destaque as dependências e versões necessárias.
    - Forneça informações sobre variáveis de ambiente essenciais.

## **Opcionais (Fortemente Recomendados)**

1. **Uso de Docker:**
    - Considere a criação de um arquivo **`Dockerfile`** para facilitar a execução do aplicativo em um contêiner Docker.
    - Utilize o **`docker-compose`** para orquestrar múltiplos serviços, como o aplicativo Node.js e o banco de dados PostgreSQL.
    - Inclua instruções claras no README sobre como usar o Docker para configurar e executar o ambiente.
2. **Documentação de Tecnologias Utilizadas:**
    - Crie um documento opcional listando as tecnologias usadas no projeto.
    - Discorra sobre cada tecnologia, explicando o que é, para que serve e forneça exemplos.
3. **Testes Unitários:**
    - Escreva testes unitários utilizando Mocha ou Jest.
    - Utilize a biblioteca **`supertest`** para testar as requisições à API.
    - Considere o uso de **`sinon`** para criar stubs e espiões durante os testes.

## **Critérios de Avaliação**

- **Funcionalidade:** O sistema deve autenticar usuários, interagir com o banco de dados e oferecer operações CRUD através da API.
- **Segurança:** Garanta que a autenticação seja segura, e as senhas estejam devidamente protegidas.
- **Organização do Código:** Estruture o código de maneira modular e organizada.
- **Documentação:** Inclua comentários relevantes, documentação explicativa e utilize o Swagger para facilitar a compreensão da API.
- **Testes Unitários:** Certifique-se de que os testes cubram os principais cenários de uso e possíveis falhas.
- **Conexão com o Banco de Dados:** A conexão deve ser segura, e as operações no banco de dados devem ser eficientes.
- **Uso de Middlewares:** Demonstre habilidade na implementação e utilização de middlewares para autenticação e tratamento de erros.
- **Tratamento de Erro:** Implemente um tratamento de erro consistente em toda a aplicação.
- **Variáveis de Ambiente:** Utilize variáveis de ambiente para configurar o projeto de maneira flexível.
- **Git:** Mantenha um histórico de commits organizado, exclua arquivos desnecessários do repositório.
- **README Detalhado:** Forneça um guia claro e completo sobre como configurar, executar e interagir com o projeto.