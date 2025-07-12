# Star Wars API Wrapper - Backend Challenge

Este projeto é uma API desenvolvida com **FastAPI** que atua como um _wrapper_ da [Star Wars API (SWAPI)](https://swapi.py4e.com), com autenticação via JWT, filtros dinâmicos, ordenação e deploy serverless via **AWS Lambda + API Gateway**.

## 🚀 Tecnologias Utilizadas

- **FastAPI** - Framework web moderno e performático
- **Python 3.11+** - Linguagem principal
- **JWT (JSON Web Token)** - Autenticação segura via token
- **httpx + asyncio** - Requisições assíncronas performáticas
- **pytest** - Testes unitários automatizados
- **AWS Lambda + API Gateway** - Deploy serverless
- **dotenv** - Gerenciamento de variáveis de ambiente

---

## 🔧 Funcionalidades

### Endpoints implementados:

#### 1. **/token**

- `POST`: Gera um token JWT válido para acesso aos endpoints protegidos.

#### 2. **/starships**

- Lista naves espaciais com filtros:

  - `?name=...`
  - `?order_by=hyperdrive_rating|cost_in_credits`
  - `?direction=asc|desc`

#### 3. **/planets**

- Lista planetas com:

  - `?name=...`
  - `?order_by=population|diameter`
  - `?direction=asc|desc`

#### 4. **/characters**

- Lista personagens com:

  - `?name=...`
  - `?order_by=height|mass`
  - `?direction=asc|desc`

#### 5. **/films**

- Lista filmes com:

  - `?title=...`
  - `?order_by=release_date|episode_id`
  - `?direction=asc|desc`

Todos os endpoints retornam dados enriquecidos com informações de entidades relacionadas (ex: personagens de um filme, pilotos de uma nave).

---

## ✅ Execução local

```bash
# 1. Clone o repositório
git clone https://github.com/DanielJardiim/starwars-api.git
cd starwars-api

# 2. Crie o ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate    # Windows

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Defina as variáveis de ambiente no .env
```

### .env

```
BASE_URL=https://swapi.py4e.com/api
SECRET_KEY=chaveultrasecreta
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

### 5. Rode o servidor local

```bash
uvicorn app.main:app --reload
```

Acesse: [http://localhost:8000/docs](http://localhost:8000/docs)

---

## ✅ Rodando os testes

```bash
pytest
```

---

## 🌌 Deploy na AWS

- Empacotamento com `Mangum`
- Integração com **API Gateway**
- Upload via **AWS Console ou SAM CLI**

---

## 📏 Diagrama de Arquitetura

```mermaid
flowchart TD
    A[Usuário (Frontend ou API Client)]
    A --> B[API Gateway (AWS)]
    B --> C[AWS Lambda (FastAPI)]
    C --> D[FastAPI App]

    subgraph FastAPI Interno
        D --> E[Auth (JWT)]
        D --> F[Rotas: /films, /planets, /characters, /starships]
        F --> G[Serviço SWAPI Client]
    end

    G --> H[SWAPI (https://swapi.py4e.com)]
```

---

## 📅 Autor

**Daniel Jardim Nunes**

---

## 🔗 Licença

MIT License
