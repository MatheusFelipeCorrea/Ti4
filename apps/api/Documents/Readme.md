# ⚙️ API — Backend

Servidor HTTP construído com **Node.js + Express** seguindo o padrão **MVC**
com camadas extras de **Service** e **Repository** para separação de
responsabilidades.

---

## 🗂️ Índice

- [Tecnologias](#-tecnologias)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Descrição das Camadas](#-descrição-das-camadas)
- [Fluxo de uma Requisição](#-fluxo-de-uma-requisição)
- [Rotas da API](#-rotas-da-api)
- [Regras de Negócio](#-regras-de-negócio)
- [Como Rodar](#-como-rodar)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)
- [Padrão de Erros](#-padrão-de-erros)

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|------------|-----|
| Node.js | Runtime |
| Express | Framework HTTP |
| Prisma | ORM / Banco de dados |
| Zod | Validação de dados |
| JWT | Autenticação |
| Bcrypt | Criptografia de senhas |
| Pino | Logs |
| Vitest | Testes |

---

## 📁 Estrutura de Pastas

```
apps/api/src/
│
├── 📄 server.js
├── 📄 app.js
│
├── 📁 models/
│   ├── 📄 Fazenda.js
│   ├── 📄 Safra.js
│   ├── 📄 Custo.js
│   ├── 📄 Venda.js
│   └── 📄 Cotacao.js
│
├── 📁 views/
│   ├── 📄 cotacao.view.js
│   ├── 📄 custo.view.js
│   ├── 📄 estoque.view.js
│   ├── 📄 fazenda.view.js
│   ├── 📄 relatorio.view.js
│   ├── 📄 safra.view.js
│   ├── 📄 simulacao.view.js
│   └── 📄 venda.view.js
│
├── 📁 controllers/
│   ├── 📄 cotacao.controller.js
│   ├── 📄 custo.controller.js
│   ├── 📄 estoque.controller.js
│   ├── 📄 fazenda.controller.js
│   ├── 📄 relatorio.controller.js
│   ├── 📄 safra.controller.js
│   ├── 📄 simulacao.controller.js
│   └── 📄 venda.controller.js
│
├── 📁 services/
│   ├── 📄 cotacao.service.js
│   ├── 📄 custo.service.js
│   ├── 📄 estoque.service.js
│   ├── 📄 fazenda.service.js
│   ├── 📄 relatorio.service.js
│   ├── 📄 safra.service.js
│   ├── 📄 simulacao.service.js
│   └── 📄 venda.service.js
│
├── 📁 repositories/
│   ├── 📄 custo.repository.js
│   ├── 📄 estoque.repository.js
│   ├── 📄 fazenda.repository.js
│   ├── 📄 safra.repository.js
│   └── 📄 venda.repository.js
│
├── 📁 routes/
│   ├── 📄 cotacao.routes.js
│   ├── 📄 custo.routes.js
│   ├── 📄 estoque.routes.js
│   ├── 📄 fazenda.routes.js
│   ├── 📄 relatorio.routes.js
│   ├── 📄 safra.routes.js
│   ├── 📄 simulacao.routes.js
│   ├── 📄 venda.routes.js
│   └── 📄 index.js
│
├── 📁 middlewares/
│   ├── 📄 auth.middleware.js
│   ├── 📄 error.middleware.js
│   ├── 📄 limitador.middleware.js
│   ├── 📄 validator.middleware.js
│   └── 📄 logger.middleware.js
│
├── 📁 schemas/
│   ├── 📄 custo.schema.js
│   ├── 📄 fazenda.schema.js
│   ├── 📄 safra.schema.js
│   ├── 📄 simulacao.schema.js
│   └── 📄 venda.schema.js
│
├── 📁 config/
│   ├── 📄 env.js
│   ├── 📄 cors.js
│   └── 📄 index.js
│
├── 📁 database/
│   ├── 📄 client.js
│   ├── 📁 migrations/
│   └── 📁 seeds/
│       └── 📄 admin.seed.js
│
├── 📁 shared/
│   ├── 📁 errors/
│   │   ├── 📄 AppError.js
│   │   └── 📄 index.js
│   └── 📁 utils/
│       ├── 📄 logger.js
│       ├── 📄 jwt.js
│       └── 📄 bcrypt.js
│
└── 📁 tests/
  ├── 📄 setup.js
  ├── 📁 unit/
  │   ├── 📄 custo.service.spec.js
  │   ├── 📄 estoque.service.spec.js
  │   ├── 📄 fazenda.service.spec.js
  │   ├── 📄 relatorio.service.spec.js
  │   ├── 📄 safra.service.spec.js
  │   └── 📄 venda.service.spec.js
  └── 📁 integration/
      ├── 📄 estoque.spec.js
      ├── 📄 fazenda.spec.js
      ├── 📄 safra.spec.js
      └── 📄 venda.spec.js
```

---

## 📖 Descrição das Camadas

---

### 📄 `server.js`
> Ponto de entrada da aplicação

```
→ Importa o app.js
→ Sobe o servidor na porta definida no .env
→ Loga confirmação no console
```

---

### 📄 `app.js`
> Configura e monta o Express

```
→ Registra middlewares globais (helmet, cors, json)
→ Registra todas as rotas com prefixo /api
→ Registra o error.middleware (sempre por último)
```

---

### 📁 `models/` — M do MVC
> Define a **estrutura dos dados** da aplicação

```
Fazenda.js
→ id, nome, tipo (propria | arrendada), localizacao, criadoEm

Safra.js
→ id, fazendaId, cultura (soja | milho | cafe)
→ area, sacas, ano, criadoEm

Custo.js
→ id, safraId
→ tipo (adubo | sementes | combustivel | diesel | manutencao)
→ valor, descricao, criadoEm

Venda.js
→ id, safraId, quantidade, valor, data, criadoEm

Cotacao.js
→ id, valor, fonte, atualizadoEm

✅ Define a "forma" dos dados da aplicação
✅ Complementa o schema do Prisma
❌ Sem regra de negócio
❌ Sem acesso direto ao banco
```

---

### 📁 `views/` — V do MVC
> **Formata o JSON** de resposta — controla o que é exposto ao frontend

```
fazenda.view.js
→ render(fazenda)        → formata um único registro
→ renderMany(fazendas)   → formata uma lista

safra.view.js
→ render(safra)
→ renderMany(safras)

custo.view.js
→ render(custo)
→ renderMany(custos)

venda.view.js
→ render(venda)
→ renderMany(vendas)

estoque.view.js
→ render(estoque)        → saldo de sacas disponíveis

cotacao.view.js
→ render(cotacao)        → valor do dólar e horário de atualização

relatorio.view.js
→ renderCustosVsVendas(dados)    → RF07 gráfico custos x vendas
→ renderLucroPorSafra(dados)     → RF09 lucro por safra
→ renderCustosPorCultura(dados)  → RF10 custos por cultura
→ renderMinPreco(dados)          → RF11 preço mínimo de venda

simulacao.view.js
→ render(simulacao)      → resultado da simulação de venda

✅ Padroniza o formato de todas as respostas
✅ Remove campos sensíveis antes de responder
❌ Nunca expõe dados internos desnecessários
```

---

### 📁 `controllers/` — C do MVC
> **Recebe a requisição**, chama o service e **retorna a resposta**

```
fazenda.controller.js
→ getAll          GET    /api/fazendas
→ getPorId        GET    /api/fazendas/:id
→ create          POST   /api/fazendas
→ update          PUT    /api/fazendas/:id
→ delete          DELETE /api/fazendas/:id

safra.controller.js
→ getAll          GET    /api/safras
→ getPorId        GET    /api/safras/:id
→ getPorFazenda   GET    /api/safras/fazenda/:fazendaId
→ create          POST   /api/safras
→ update          PUT    /api/safras/:id
→ delete          DELETE /api/safras/:id

custo.controller.js
→ getAll          GET    /api/custos
→ getPorSafra     GET    /api/custos/safra/:safraId
→ create          POST   /api/custos
→ update          PUT    /api/custos/:id
→ delete          DELETE /api/custos/:id

venda.controller.js
→ getAll          GET    /api/vendas
→ getPorSafra     GET    /api/vendas/safra/:safraId
→ create          POST   /api/vendas
→ update          PUT    /api/vendas/:id
→ delete          DELETE /api/vendas/:id

estoque.controller.js
→ getAll          GET    /api/estoque
→ getPorSafra     GET    /api/estoque/safra/:safraId

cotacao.controller.js
→ getDollar       GET    /api/cotacao/dollar

relatorio.controller.js
→ custosVsVendas     GET  /api/relatorios/custos-vs-vendas
→ lucroPorSafra      GET  /api/relatorios/lucro/:safraId
→ custosPorCultura   GET  /api/relatorios/custos-por-cultura
→ minPreco           GET  /api/relatorios/min-preco

simulacao.controller.js
→ simularVenda    POST   /api/simulacao/venda

✅ Recebe req e res
✅ Chama o service correto
✅ Retorna resposta usando a view
✅ Erros sempre com try/catch → next(error)
❌ Sem regra de negócio
❌ Sem acesso direto ao banco
```

---

### 📁 `services/`
> **Regras de negócio** — coração da aplicação

```
fazenda.service.js
→ Valida tipo obrigatório (propria | arrendada)        → Restrição 1
→ Bloqueia exclusão se tiver safras vinculadas         → RNF06

safra.service.js
→ Valida se a fazenda existe antes de criar
→ Valida cultura (soja | milho | cafe)

custo.service.js
→ Valida se a safra existe antes de criar              → Restrição 3

venda.service.js
→ Busca saldo atual do estoque
→ Bloqueia se quantidade > estoque disponível          → Restrição 2

estoque.service.js
→ Calcula: sacas_produzidas - sacas_vendidas           → RF08

cotacao.service.js
→ Verifica se existe cache válido
→ Busca na API externa se cache estiver vencido
→ Salva novo valor no cache com timestamp
→ Atualiza em menos de 2 segundos ao reconectar        → RNF03

relatorio.service.js
→ Soma custos e vendas agrupados por safra             → RF07
→ Calcula lucro por safra: vendas - custos             → RF09
→ Soma custos agrupados por cultura                    → RF10
→ Calcula preço mínimo: custos ÷ sacas produzidas      → RF11
→ Todos aceitam filtro por data de início e fim        → RF12

simulacao.service.js
→ Busca saldo atual do estoque
→ Busca cotação atual do dólar
→ Calcula valor bruto: estoque × cotação               → RF06

✅ Toda regra de negócio fica aqui
✅ Chama o repository para acessar o banco
✅ Lança erros com AppError quando algo é inválido
❌ Não conhece req/res
❌ Sem acesso direto ao banco
```

---

### 📁 `repositories/`
> **Única camada que fala com o banco** de dados

```
fazenda.repository.js
→ buscarTodos
→ buscarPorId
→ buscarComSafras       → traz fazenda com suas safras vinculadas
→ create
→ update
→ delete

safra.repository.js
→ buscarTodos
→ buscarPorId
→ buscarPorFazenda
→ create
→ update
→ delete

custo.repository.js
→ buscarTodos
→ buscarPorSafra
→ create
→ update
→ delete

venda.repository.js
→ buscarTodos
→ buscarPorSafra
→ create
→ update
→ delete

estoque.repository.js
→ totalSacasPorSafra    → soma total de sacas produzidas
→ totalVendidasPorSafra → soma total de sacas já vendidas

✅ Toda query de banco fica aqui
✅ Se trocar de banco, só mexe aqui
❌ Sem regra de negócio
❌ Sem req/res
```

---

### 📁 `routes/`
> Define as **URLs** e conecta aos controllers

```
fazenda.routes.js     → rotas de /api/fazendas
safra.routes.js       → rotas de /api/safras
custo.routes.js       → rotas de /api/custos
venda.routes.js       → rotas de /api/vendas
estoque.routes.js     → rotas de /api/estoque
cotacao.routes.js     → rotas de /api/cotacao
relatorio.routes.js   → rotas de /api/relatorios
simulacao.routes.js   → rotas de /api/simulacao

index.js
→ Agrupa todas as rotas em um único lugar
→ É o único arquivo registrado no app.js

✅ Aplica middlewares específicos por rota
✅ Chama o controller correto
```

---

### 📁 `middlewares/`
> Funções que rodam **entre a requisição e o controller**

```
auth.middleware.js
→ Verifica se o token JWT existe e é válido
→ Bloqueia com 401 se inválido ou ausente
→ Anexa os dados do usuário no req

error.middleware.js
→ Captura TODOS os erros da aplicação
→ Retorna resposta padronizada com status e mensagem
→ DEVE ser o último middleware registrado no app.js
→ Loga o erro com o logger

validator.middleware.js
→ Recebe um schema Zod como parâmetro
→ Valida o req.body antes de chegar no controller
→ Retorna 400 com mensagem clara se dados inválidos

limitador.middleware.js
→ Limita quantidade de requisições por IP
→ Protege contra ataques de força bruta
→ Configurável por rota (login mais restrito)

logger.middleware.js
→ Loga toda requisição que chega
→ Registra: método, URL, status e tempo de resposta
```

---

### 📁 `schemas/`
> **Validação dos dados** de entrada com Zod

```
fazenda.schema.js
→ nome: string obrigatório
→ tipo: enum (propria | arrendada) obrigatório

safra.schema.js
→ fazendaId: número obrigatório
→ cultura: enum (soja | milho | cafe) obrigatório
→ area: número obrigatório
→ sacas: número obrigatório
→ ano: número obrigatório

custo.schema.js
→ safraId: número obrigatório
→ tipo: enum (adubo | sementes | combustivel | diesel | manutencao)
→ valor: número obrigatório
→ descricao: string opcional

venda.schema.js
→ safraId: número obrigatório
→ quantidade: número obrigatório
→ valor: número obrigatório
→ data: data obrigatório

simulacao.schema.js
→ safraId: número obrigatório

✅ Garante que dados inválidos nem chegam no controller
✅ Retorna mensagens de erro claras e padronizadas
✅ Sempre usado junto com o validator.middleware
```

---

### 📁 `config/`
> **Configurações técnicas** da aplicação

```
env.js
→ Valida se todas as variáveis de ambiente existem
→ A aplicação não sobe se faltar alguma variável

cors.js
→ Define quais origens podem acessar a API
→ Configurado via variável de ambiente CORS_ORIGIN

index.js
→ Exporta todas as configurações juntas
```

---

### 📁 `database/`
> Tudo relacionado ao **banco de dados**

```
client.js
→ Instância do Prisma pronta pra usar em toda a aplicação
→ Importado pelos repositories

migrations/
→ Histórico de todas as alterações no banco
→ Criar tabela, adicionar coluna, alterar campo...
→ NUNCA editar uma migration já executada em produção

seeds/
admin.seed.js
  → Cria o usuário administrador padrão
  → Executado uma única vez ao configurar o ambiente
```

---

### 📁 `shared/`
> Código **reutilizado em todo o backend**

```
errors/
AppError.js
  → Classe de erro customizado da aplicação
  → Recebe mensagem e statusCode
  → Lançado nos services quando algo é inválido
  → Capturado e tratado pelo error.middleware

utils/
logger.js
  → Instância configurada do Pino
  → Substitui o console.log em toda a aplicação
  → Usado no logger.middleware e error.middleware

jwt.js
  → generateToken(payload)   → gera um token JWT
  → verifyToken(token)       → valida e retorna os dados

bcrypt.js
  → hash(password)           → gera o hash da senha
  → compare(password, hash)  → compara senha com hash
```

---

### 📁 `tests/`
> **Testes automatizados** da aplicação

```
setup.js
→ Configurações globais antes de rodar os testes
→ Conexão com banco de teste
→ Limpeza de dados entre cada teste

unit/
→ Testa funções isoladas de cada service
→ Sem banco real — usa mock do repository
→ Rápido de rodar

fazenda.service.spec.js
  → testa bloqueio de exclusão com safras vinculadas
  → testa validação de tipo (propria | arrendada)

safra.service.spec.js
  → testa validação de cultura
  → testa vínculo com fazenda existente

custo.service.spec.js
  → testa validação de safra existente antes de criar

venda.service.spec.js
  → testa bloqueio por estoque insuficiente

estoque.service.spec.js
  → testa cálculo correto do saldo de sacas

relatorio.service.spec.js
  → testa cálculos de lucro e preço mínimo

integration/
→ Testa o fluxo completo da rota até o banco
→ Usa banco de teste real

fazenda.spec.js    → CRUD completo + regras de exclusão
safra.spec.js      → CRUD + vínculo com fazenda
venda.spec.js      → criação + validação de estoque
estoque.spec.js    → cálculo real com dados no banco
```

---

## 🔄 Fluxo de uma Requisição

```
                    REQUEST
                       │
                       ▼
                ┌────────────┐
                │   routes   │
                │  index.js  │  agrupa todas as rotas
                └─────┬──────┘
                       │
                       ▼
       ┌───────────────────────────────┐
       │           middlewares         │
       │                               │
       │  1. logger.middleware         │ loga a requisição
       │  2. auth.middleware           │ token válido?
       │  3. validator.middleware      │ body válido?
       └───────────────┬───────────────┘
                       │
                       ▼
              ┌─────────────────┐
              │   controller    │◄── C do MVC
              │                 │
              │ recebe req/res  │
              │ chama o service │
              │ retorna resposta│
              └────────┬────────┘
                       │
                       ▼
               ┌───────────────┐
               │    service    │
               │               │
               │ regra de      │
               │ negócio       │
               │ lança AppError│
               └───────┬───────┘
                       │
                       ▼
              ┌─────────────────┐
              │   repository    │
              │                 │
              │ única camada    │
              │ que acessa      │
              │ o banco         │
              └────────┬────────┘
                       │
                       ▼
                 ┌──────────┐
                 │  model   │◄── M do MVC
                 │          │
                 │ estrutura│
                 │ dos dados│
                 └────┬─────┘
                      │
                      ▼
             ┌──────────────────┐
             │      view        │◄── V do MVC
             │                  │
             │ formata o JSON   │
             │ remove campos    │
             │ sensíveis        │
             └────────┬─────────┘
                      │
                      ▼
                   RESPONSE

─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
Se ocorrer erro em qualquer etapa:

service lança AppError
     │
     ▼
controller → next(error)
     │
     ▼
error.middleware
→ loga o erro
→ retorna JSON padronizado
─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
```

---

## 🛣️ Rotas da API

```
Todas as rotas seguem o prefixo /api

FAZENDAS
GET    /api/fazendas
GET    /api/fazendas/:id
POST   /api/fazendas
PUT    /api/fazendas/:id
DELETE /api/fazendas/:id

SAFRAS
GET    /api/safras
GET    /api/safras/:id
GET    /api/safras/fazenda/:fazendaId
POST   /api/safras
PUT    /api/safras/:id
DELETE /api/safras/:id

CUSTOS
GET    /api/custos
GET    /api/custos/safra/:safraId
POST   /api/custos
PUT    /api/custos/:id
DELETE /api/custos/:id

VENDAS
GET    /api/vendas
GET    /api/vendas/safra/:safraId
POST   /api/vendas
PUT    /api/vendas/:id
DELETE /api/vendas/:id

ESTOQUE
GET    /api/estoque
GET    /api/estoque/safra/:safraId

COTAÇÃO
GET    /api/cotacao/dollar

RELATÓRIOS
GET    /api/relatorios/custos-vs-vendas
GET    /api/relatorios/lucro/:safraId
GET    /api/relatorios/custos-por-cultura
GET    /api/relatorios/min-preco

Todos aceitam: ?dataInicio=&dataFim=

SIMULAÇÃO
POST   /api/simulacao/venda
```

---

## ⚙️ Regras de Negócio

```
Restrição 1 — Tipo de fazenda obrigatório
→ Toda fazenda deve ser (propria | arrendada)
→ Validado no schema antes de chegar no service

Restrição 2 — Bloqueio de venda por estoque
→ Busca saldo atual: sacas_produzidas - sacas_vendidas
→ Se quantidade > saldo disponível → AppError 400

Restrição 3 — Custo deve ter safra vinculada
→ Verifica se a safra existe antes de criar o custo
→ Se não existir → AppError 404

RNF06 — Bloqueio de exclusão de fazenda
→ Verifica se existem safras vinculadas antes de deletar
→ Se existir → AppError 400 com mensagem explicativa
```

---

## ▶️ Como Rodar

```bash
# Instalar dependências
npm install

# Rodar em desenvolvimento
npm run dev

# Rodar em produção
npm start

# Rodar os testes
npm test

# Rodar migrations do banco
npx prisma migrate dev

# Popular o banco com dados iniciais
npm run seed
```

---

## 🔑 Variáveis de Ambiente

Copie o `.env.example` e crie seu `.env`:

```bash
cp .env.example .env
env
# Servidor
PORT=3333
NODE_ENV=development

# Banco de dados
DATABASE_URL="postgresql://user:password@localhost:5432/dbname"

# JWT
JWT_SECRET=sua_chave_secreta_aqui
JWT_EXPIRES_IN=7d

# CORS
CORS_ORIGIN=http://localhost:5173
```

---

## ⚠️ Padrão de Erros

Todos os erros retornam o mesmo formato:

```json
{
"status": "error",
"message": "Descrição clara do que aconteceu"
}
```

| Código | Situação |
|--------|----------|
| 400 | Dados inválidos ou regra de negócio violada |
| 401 | Não autenticado |
| 403 | Sem permissão |
| 404 | Registro não encontrado |
| 409 | Conflito (ex: e-mail já cadastrado) |
| 500 | Erro interno do servidor |