# 🌐 API de Microsserviços: Gestão de Usuários e Clientes

Uma API robusta baseada em arquitetura de microsserviços, desenvolvida em Node.js. Este projeto demonstra a separação de domínios (Autenticação, Usuários e Recursos), conteinerização com Docker e um pipeline completo de CI/CD para deploy automatizado na AWS.

---

## 🛠️ Tecnologias e Infraestrutura

**Backend & Testes:**
* Node.js & Express.js
* JWT (JSON Web Tokens) para segurança e controle de sessão
* Jest & Supertest para testes automatizados

**DevOps & Cloud (AWS):**
* **Docker & Docker Compose:** Para orquestração do ambiente de desenvolvimento local.
* **GitHub Actions:** Pipeline de CI/CD configurado para build e deploy automatizados.
* **Amazon ECR:** Repositório privado para as imagens Docker.
* **Amazon ECS (Fargate):** Orquestração dos containers em nuvem (Serverless).
* **Application Load Balancer (ALB):** Roteamento inteligente de requisições baseado no *path* da URL (`/auth`, `/users`, `/clients`).
* **Amazon RDS:** Banco de dados relacional (MySQL) altamente disponível.

---

## 🏗️ Topologia dos Serviços

O sistema é modular e dividido em três aplicações independentes:

1. **Auth Service (Porta 3001):** Gateway de segurança. Valida credenciais e emite o token JWT assinado.
2. **User Service (Porta 3002):** Serviço de domínio para listagem e consulta detalhada dos perfis de usuários cadastrados no sistema.
3. **Resource Service (Porta 3003):** Serviço de domínio de negócios focado no gerenciamento (CRUD) do portfólio de Clientes.

---

## 🚀 Como Executar o Projeto Localmente

O ambiente de desenvolvimento está totalmente conteinerizado, facilitando a execução em qualquer máquina.

### 1. Variáveis de Ambiente
Certifique-se de configurar as credenciais no seu arquivo `docker-compose.yml` ou em um arquivo `.env` na raiz do projeto.

### 2. Subindo a Infraestrutura

Abra o terminal na raiz do projeto e execute:

```bash
docker-compose up --build

```

*Este comando fará o build das três imagens Node.js e subirá o banco de dados MySQL simultaneamente.*

---

## 📌 Documentação de Rotas (Endpoints)

> **⚠️ Importante:** Para acessar as rotas do **User Service** e do **Resource Service**, é obrigatório enviar o token JWT gerado pelo Auth Service no cabeçalho da requisição:
> `Authorization: Bearer <SEU_TOKEN_AQUI>`

### 🔐 Auth Service

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `POST` | `/auth/register` | Cria um novo usuário de acesso. |
| `POST` | `/auth/login` | Autentica e retorna o JWT. |

**Exemplo de Body (JSON) para Login/Register:**

```json
{
  "name": "Admin",
  "email": "admin@empresa.com",
  "password": "senha_segura_123"
}

```

### 👤 User Service

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `GET` | `/users` | Retorna um array com todos os usuários do sistema. |
| `GET` | `/users/:id` | Retorna os dados de um usuário específico pelo ID. |

### 🏢 Resource Service (Clientes)

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `POST` | `/clients` | Cadastra um novo cliente na base de dados. |
| `GET` | `/clients` | Lista todos os clientes cadastrados. |
| `PUT` | `/clients/:id` | Atualiza as informações de um cliente existente. |

**Exemplo de Body (JSON) para POST/PUT Clientes:**

```json
{
  "name": "Empresa XPTO Ltda",
  "email": "contato@xpto.com",
  "cpf": "123.456.789-00"
}

```

---

## 🧪 Suíte de Testes

Os testes unitários e de integração foram construídos com Jest. Para executá-los:

1. Navegue até a pasta do serviço alvo (ex: `cd auth-service`).
2. Instale as dependências (caso seja a primeira vez):
```bash
npm install

```


3. Rode os testes:
```bash
npm test

```

## 👨‍💻 Autores 
<div>
  <table style="margin: 0 auto;">
    <tr>
      <td><a href="https://github.com/DavidPotentini"><img loading="lazy" src="https://avatars.githubusercontent.com/u/106561154?v=4" width="115"><br><sub>David Potentini</sub></a></td>
      <td><a href="https://github.com/Layonj300"><img loading="lazy" src="https://avatars.githubusercontent.com/u/106559843?v=4" width="115"><br><sub>Layon Reis</sub></a></td>
    </tr>
  </table>
</div>
