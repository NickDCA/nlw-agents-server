# NLW Agents - Servidor

Este é o backend da aplicação NLW Agents, desenvolvido durante o evento Next Level Week da Rocketseat. A aplicação utiliza uma stack moderna focada em performance e integra capacidades de IA com o uso de vetores no banco de dados.

## Tecnologias Utilizadas

O projeto foi construído com as seguintes tecnologias e padrões:

-   **Node.js & TypeScript**: Ambiente de execução e linguagem principal.
-   **Fastify**: Framework web focado em alta performance e baixo overhead.
-   **Drizzle ORM**: Toolkit para interagir com o banco de dados de forma type-safe.
-   **PostgreSQL**: Banco de dados relacional robusto.
-   **pgvector**: Extensão para PostgreSQL que permite o armazenamento e busca de vetores, essencial para aplicações de IA e embeddings.
-   **Docker & Docker Compose**: Para containerização e orquestração do ambiente de desenvolvimento, garantindo consistência.
-   **Biome**: Ferramenta integrada para lint e formatação de código, substituindo o combo ESLint + Prettier.

## Setup e Configuração

Siga os passos abaixo para configurar e executar o projeto em seu ambiente local.

### Pré-requisitos

-   **Node.js** (versão 18 ou superior)
-   **Docker** e **Docker Compose**
-   Um gerenciador de pacotes como **npm**, **yarn** ou **pnpm**

### 1. Instalação

Primeiro, clone o repositório e instale as dependências do projeto.

```bash
# Navegue até a pasta do servidor
cd nlw-agents/server

# Instale as dependências
npm install
```

### 2. Variáveis de Ambiente

Crie um arquivo `.env` na raiz da pasta `server`, utilizando o `.env.example` como base.

**`.env`**

```env
DATABASE_URL="postgresql://docker:docker@localhost:5434/agents?schema=public"
```

Este é o connection string que a sua aplicação usará para se conectar ao banco de dados PostgreSQL que será executado via Docker.

### 3. Banco de Dados

O ambiente de banco de dados é gerenciado pelo Docker Compose.

**a. Inicie o container do PostgreSQL:**

O comando abaixo irá iniciar um container com PostgreSQL 17 e a extensão `pgvector` já habilitada, conforme definido no `docker-compose.yml`.

```bash
docker-compose up -d
```

> O script `docker/setup.sql` é executado automaticamente na inicialização do container para garantir que a extensão `pgvector` esteja ativa.

**b. Execute as Migrações:**

Com o banco de dados em execução, aplique as migrações do schema utilizando o Drizzle ORM.

```bash
npx drizzle-kit migrate
```

## Executando a Aplicação

Para iniciar o servidor em modo de desenvolvimento, execute:

```bash
npm run dev
```

O servidor estará disponível em `http://localhost:3333`.

## Lint e Formatação

Este projeto utiliza o **Biome** para garantir a qualidade e a consistência do código. Para verificar e aplicar as regras de formatação e lint, execute:

```bash
npx @biomejs/biome check --apply .
```
