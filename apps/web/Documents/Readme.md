# 🌐 Web — Frontend

Interface construída com **React + Vite** estilizada com **Tailwind CSS**
seguindo uma arquitetura baseada em **componentes, páginas e camadas de dados**.

---

## 🗂️ Índice

- [Tecnologias](#-tecnologias)
- [Estrutura de Pastas](#-estrutura-de-pastas)
- [Descrição das Camadas](#-descrição-das-camadas)
- [Fluxo de Dados](#-fluxo-de-dados)
- [Rotas da Aplicação](#-rotas-da-aplicação)
- [Como Rodar](#-como-rodar)
- [Variáveis de Ambiente](#-variáveis-de-ambiente)

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|------------|-----|
| React 19 | Biblioteca de interface |
| Vite 6 | Bundler e servidor de desenvolvimento |
| Tailwind CSS v4 | Estilização |
| React Router DOM | Navegação entre páginas |
| TanStack Query | Gerenciamento de estado do servidor |
| Zustand | Gerenciamento de estado global |
| Axios | Requisições HTTP |
| Zod | Validação de dados |
| Recharts | Gráficos |
| Vitest | Testes |

---

## 📁 Estrutura de Pastas

```
apps/web/
├── 📄 .env
├── 📄 .env.example
├── 📄 .gitignore
├── 📄 eslint.config.js
├── 📄 index.html
├── 📄 package-lock.json
├── 📄 package.json
├── 📄 vite.config.js
│
├── 📁 public/
│   └── 📄 favicon.ico
│
└── 📁 src/
  ├── 📄 main.jsx
  ├── 📄 App.jsx
  ├── 📁 assets/
  ├── 📁 components/
  │   ├── 📁 ui/
  │   └── 📁 shared/
  ├── 📁 pages/
  ├── 📁 layouts/
  ├── 📁 routes/
  ├── 📁 hooks/
  ├── 📁 store/
  ├── 📁 services/
  ├── 📁 queries/
  ├── 📁 utils/
  ├── 📁 constants/
  └── 📁 styles/
```

---

## 📖 Descrição das Camadas

---

### 📄 Arquivos da Raiz

```
.env
→ Variáveis de ambiente da aplicação
→ Nunca versionar esse arquivo

.env.example
→ Modelo do .env para o time
→ Versionar esse arquivo

.gitignore
→ Arquivos ignorados pelo git
→ node_modules, .env, dist...

eslint.config.js
→ Regras de qualidade e padronização do código

index.html
→ HTML base da aplicação
→ Ponto de montagem do React (#root)

package.json
→ Dependências e scripts do projeto

vite.config.js
→ Configuração do Vite
→ Plugin do React e Tailwind
→ Aliases de importação (@components, @pages...)
→ Proxy para a API (/api → localhost:3333)
```

---

### 📄 `src/main.jsx`
> Ponto de entrada da aplicação

```
→ Renderiza o <App /> no DOM
→ Configura o QueryClientProvider (React Query)
→ Configura o BrowserRouter (rotas)
→ Importa o styles/globals.css
```

---

### 📄 `src/App.jsx`
> Componente raiz

```
→ Chama o componente de rotas
→ Providers globais (toast, tema...)
```

---

### 📁 `assets/`
> Arquivos estáticos da aplicação

```
images/  → logos, banners, ilustrações (.png .jpg .svg)
icons/   → ícones SVG próprios
fonts/   → fontes customizadas (.ttf .woff .woff2)

❌ Não colocar imagens que vêm de URL/API externa
```

---

### 📁 `components/ui/`
> Componentes visuais **genéricos** — base do design system

```
Button/
→ Botão padrão do sistema
→ Variações: primary, secondary, danger
→ Props: label, onClick, disabled, loading...

Input/
→ Campo de texto padrão
→ Props: label, placeholder, error, onChange...

Modal/
→ Janela modal reutilizável
→ Props: isOpen, onClose, title, children...

Select/
→ Campo de seleção (dropdown)
→ Props: options, value, onChange, placeholder...

Table/
→ Tabela de dados reutilizável
→ Props: columns, data, loading...

Badge/
→ Etiqueta colorida
→ Usado em: Própria | Arrendada | Soja | Milho | Café
→ Usado em: Pago | Pendente

Spinner/
→ Indicador de carregamento

✅ Estilizados com Tailwind
✅ Recebem tudo via props
✅ Reutilizáveis em qualquer parte do projeto
❌ Não acessam store
❌ Não fazem chamada de API
```

---

### 📁 `components/shared/`
> Componentes de **negócio** reutilizados em múltiplas páginas

```
Header/
→ Cabeçalho da aplicação
→ Exibe: nome do sistema, cotação do dólar em tempo real
→ Exibe: fazenda selecionada e nome do usuário logado

Sidebar/
→ Navegação lateral
→ Links para todas as páginas do sistema
→ Menus diferentes para ADMIN e FUNCIONARIO
→ Destaca a rota ativa

Footer/
→ Rodapé da aplicação

✅ Podem acessar store
✅ Conhecem o negócio da aplicação
❌ Não são páginas completas
```

---

### 📁 `pages/`
> Cada pasta representa **uma tela da aplicação**

```
Auth/Login/
→ Tela de login
→ Formulário: email e senha
→ Rota: /login

Auth/Cadastro/
→ Tela de cadastro
→ Formulário: nome, email e senha
→ Rota: /cadastro

Dashboard/
→ Painel financeiro principal (RF08)
→ Exibe: gráfico gastos x lucros
→ Exibe: saldo de sacas em estoque
→ Exibe: cotação do dólar em tempo real
→ Rota: /

Fazendas/
→ CRUD de fazendas (RF01)
→ Filtro global de fazenda (RF02)
→ Rota: /fazendas

Colheitas/
→ Controle de sacas colhidas (RF03)
→ Registro: cultura, quantidade, data, fazenda
→ Rota: /colheitas

Gastos/
→ Gestão de gastos (RF05)
→ Status: Pago | Pendente
→ Data de vencimento opcional
→ Filtro avançado (RF07)
→ Rota: /gastos

Lucros/
→ Registro de lucros de venda (RF06)
→ Informa: cultura, sacas, valor, comprador, data
→ Rota: /lucros

Estoque/
→ Saldo de sacas disponíveis
→ Calculado: sacas colhidas - sacas vendidas
→ Rota: /estoque

Lembretes/
→ Cadastro de lembretes (RF10)
→ Envia notificação via WhatsApp na data
→ Status: Pendente | Enviado | Cancelado
→ Rota: /lembretes

Insumos/
→ Registro diário de insumos (RF13)
→ Apenas FUNCIONARIO
→ item, quantidade, observações
→ Rota: /insumos

Relatorios/
→ Apenas ADMIN
→ Histórico de produção (RF04)
→ Filtro avançado de gastos (RF07)
→ Rota: /relatorios

Simulacao/
→ Calculadora de dívidas (RF09)
→ Total pago + pendente com cores
→ Calcula sacas necessárias para quitar
→ Rota: /simulacao

IA/
→ Apenas ADMIN
→ Insights gerados pelo Google Gemini (RF11)
→ Análise de gastos e comparativos
→ Rota: /ia

✅ Montam a tela usando components
✅ Buscam dados via queries
✅ Gerenciam estado local (useState)
❌ Não fazem fetch direto
❌ Lógica complexa vai para hooks
```

---

### 📁 `layouts/`
> Esqueletos visuais que **envolvem as páginas**

```
AuthLayout.jsx
→ Tela limpa sem menu
→ Usado em: /login e /cadastro

MainLayout.jsx
→ Tela completa com navegação
→ Renderiza: Header + Sidebar + conteúdo + Footer
→ Usado em todas as páginas logadas

✅ Definem a estrutura visual base
❌ Sem lógica de negócio
```

---

### 📁 `routes/`
> Configuração de **todas as rotas** da aplicação

```
index.jsx
→ Monta todas as rotas da aplicação
→ Rotas públicas usam AuthLayout
→ Rotas privadas usam MainLayout

PrivateRoute.jsx
→ Verifica se o usuário está logado
→ Se NÃO estiver → redireciona para /login

PublicRoute.jsx
→ Verifica se o usuário já está logado
→ Se JÁ estiver → redireciona para /

AdminRoute.jsx
→ Verifica se o usuário é ADMIN
→ Se NÃO for → redireciona para /dashboard
→ Protege: /relatorios e /ia
```

---

### 📁 `hooks/`
> Lógica **reutilizável** entre componentes

```
useDebounce.js
→ Atrasa a execução de uma função
→ Usado em buscas enquanto o usuário digita

useLocalStorage.js
→ Lê e escreve dados no localStorage
→ Persiste dados entre sessões do navegador

✅ Sempre começam com "use"
✅ Retornam dados e funções
❌ Não renderizam JSX
```

---

### 📁 `store/`
> Estado **global** da aplicação com Zustand

```
slices/authSlice.js
→ Armazena o usuário logado
→ Armazena o token JWT
→ role: ADMIN | FUNCIONARIO
→ isAuthenticated: true | false
→ setUser(user)  → salva o usuário
→ clearUser()    → limpa ao fazer logout

slices/uiSlice.js
→ Controla sidebar aberta ou fechada
→ Controla tema (dark | light)

slices/fazendaSlice.js
→ Armazena a fazenda selecionada (RF02)
→ Quando muda → todas as telas filtram por ela
→ Pode ser "todas" ou uma fazenda específica

index.js
→ Exporta todas as stores

✅ Dados que múltiplos componentes precisam
✅ Persiste entre navegações
❌ Não colocar dados que vêm da API
❌ Não colocar estado local de um componente só
```

---

### 📁 `services/`
> Toda **comunicação HTTP** com o backend

```
api.js
→ Instância configurada do axios
→ Define a baseURL via variável de ambiente
→ Interceptor: anexa o token JWT em toda requisição
→ Interceptor: trata erros globais (401 → logout, 500 → toast)

auth.service.js
→ login(dados)     → POST /api/auth/login
→ cadastro(dados)  → POST /api/auth/cadastro
→ logout()         → POST /api/auth/logout

fazenda.service.js
→ buscarTodas()           → GET    /api/fazendas
→ buscarPorId(id)         → GET    /api/fazendas/:id
→ criar(dados)            → POST   /api/fazendas
→ atualizar(id, dados)    → PUT    /api/fazendas/:id
→ deletar(id)             → DELETE /api/fazendas/:id

colheita.service.js
→ buscarTodas()                      → GET    /api/colheitas
→ buscarPorFazenda(fazendaId)        → GET    /api/colheitas/fazenda/:fazendaId
→ criar(dados)                       → POST   /api/colheitas
→ atualizar(id, dados)               → PUT    /api/colheitas/:id
→ deletar(id)                        → DELETE /api/colheitas/:id

gasto.service.js
→ buscarTodos()                      → GET    /api/gastos
→ buscarPorColheita(colheitaId)      → GET    /api/gastos/colheita/:colheitaId
→ criar(dados)                       → POST   /api/gastos
→ atualizar(id, dados)               → PUT    /api/gastos/:id
→ deletar(id)                        → DELETE /api/gastos/:id

lucro.service.js
→ buscarTodos()                      → GET    /api/lucros
→ buscarPorColheita(colheitaId)      → GET    /api/lucros/colheita/:colheitaId
→ criar(dados)                       → POST   /api/lucros
→ atualizar(id, dados)               → PUT    /api/lucros/:id
→ deletar(id)                        → DELETE /api/lucros/:id

estoque.service.js
→ buscarTodos()                      → GET    /api/estoque
→ buscarPorColheita(colheitaId)      → GET    /api/estoque/colheita/:colheitaId

cotacao.service.js
→ buscarDolar()                      → GET    /api/cotacao/dolar

relatorio.service.js
→ buscarGastosVsLucros(filtros)      → GET    /api/relatorios/gastos-vs-lucros
→ buscarHistoricoProducao(filtros)   → GET    /api/relatorios/historico-producao
→ buscarGastosPorTipo(filtros)       → GET    /api/relatorios/gastos-por-tipo

simulacao.service.js
→ buscarDividas()                    → GET    /api/simulacao/dividas
→ calcularSacas(dados)               → POST   /api/simulacao/calcular-sacas

lembrete.service.js
→ buscarTodos()                      → GET    /api/lembretes
→ buscarPorId(id)                    → GET    /api/lembretes/:id
→ criar(dados)                       → POST   /api/lembretes
→ atualizar(id, dados)               → PUT    /api/lembretes/:id
→ deletar(id)                        → DELETE /api/lembretes/:id

insumo.service.js
→ buscarTodos()                      → GET    /api/insumos
→ buscarPorFazenda(fazendaId)        → GET    /api/insumos/fazenda/:fazendaId
→ criar(dados)                       → POST   /api/insumos
→ deletar(id)                        → DELETE /api/insumos/:id

ia.service.js
→ gerarInsights()                    → GET    /api/ia/insights

✅ Toda comunicação HTTP fica aqui
✅ Retornam a promise diretamente
❌ Não tratam loading/error (isso é React Query)
❌ Não acessam store
```

---

### 📁 `queries/`
> **TanStack Query** — gerencia estado do servidor

```
useAuthQueries.js
→ useLogin()       → mutation de login
→ useCadastro()    → mutation de cadastro

useFazendaQueries.js
→ useGetFazendas()
→ useGetFazenda(id)
→ useCreateFazenda()
→ useUpdateFazenda()
→ useDeleteFazenda()

useColheitaQueries.js
→ useGetColheitas()
→ useGetColheitasPorFazenda(fazendaId)
→ useCreateColheita()
→ useUpdateColheita()
→ useDeleteColheita()

useGastoQueries.js
→ useGetGastos()
→ useGetGastosPorColheita(colheitaId)
→ useCreateGasto()
→ useUpdateGasto()
→ useDeleteGasto()

useLucroQueries.js
→ useGetLucros()
→ useGetLucrosPorColheita(colheitaId)
→ useCreateLucro()
→ useUpdateLucro()
→ useDeleteLucro()

useEstoqueQueries.js
→ useGetEstoque()
→ useGetEstoquePorColheita(colheitaId)

useCotacaoQueries.js
→ useGetCotacaoDolar()

useRelatorioQueries.js
→ useGetGastosVsLucros(filtros)
→ useGetHistoricoProducao(filtros)
→ useGetGastosPorTipo(filtros)

useSimulacaoQueries.js
→ useGetDividas()
→ useCalcularSacas()

useLembreteQueries.js
→ useGetLembretes()
→ useGetLembrete(id)
→ useCreateLembrete()
→ useUpdateLembrete()
→ useDeleteLembrete()

useInsumoQueries.js
→ useGetInsumos()
→ useGetInsumosPorFazenda(fazendaId)
→ useCreateInsumo()
→ useDeleteInsumo()

useIAQueries.js
→ useGerarInsights()

✅ Usa os services para buscar/enviar dados
✅ Gerencia loading, error e cache automaticamente
✅ Chamado dentro dos components e pages
❌ Não tem JSX
```

---

### 📁 `utils/`
> Funções **puras** de utilidade

```
formatters.js
→ formatarMoeda(valor)     → R$ 1.000,00
→ formatarData(data)       → 01/01/2026
→ formatarSacas(qtd)       → 1.000 sc
→ formatarDolar(valor)     → $ 5,87

validators.js
→ emailValido(email)       → true | false
→ campoObrigatorio(valor)  → true | false

masks.js
→ maskCPF(valor)           → 000.000.000-00
→ maskCNPJ(valor)          → 00.000.000/0000-00
→ maskTelefone(valor)      → (00) 00000-0000

✅ Funções puras (mesmo input = mesmo output)
✅ Sem efeitos colaterais
❌ Sem hooks, store ou chamadas HTTP
```

---

### 📁 `constants/`
> Valores **fixos** que não mudam

```
routes.js
→ ROTAS = {
    LOGIN: '/login',
    CADASTRO: '/cadastro',
    DASHBOARD: '/',
    FAZENDAS: '/fazendas',
    COLHEITAS: '/colheitas',
    GASTOS: '/gastos',
    LUCROS: '/lucros',
    ESTOQUE: '/estoque',
    LEMBRETES: '/lembretes',
    INSUMOS: '/insumos',
    RELATORIOS: '/relatorios',
    SIMULACAO: '/simulacao',
    IA: '/ia',
  }

api.js
→ API = {
    AUTH: { LOGIN: '/auth/login', CADASTRO: '/auth/cadastro' },
    FAZENDAS: '/fazendas',
    COLHEITAS: '/colheitas',
    GASTOS: '/gastos',
    LUCROS: '/lucros',
    ESTOQUE: '/estoque',
    COTACAO: '/cotacao/dolar',
    LEMBRETES: '/lembretes',
    INSUMOS: '/insumos',
    RELATORIOS: '/relatorios',
    SIMULACAO: '/simulacao',
    IA: '/ia/insights',
  }

✅ Evita magic strings espalhados no código
✅ Fácil de alterar em um só lugar
```

---

### 📁 `styles/`
> Estilos **globais** da aplicação

```
globals.css
→ @import "tailwindcss"
→ Estilos base globais

variables.css
→ Variáveis CSS customizadas
→ Complementa o Tailwind quando necessário
```

---

## 🔄 Fluxo de Dados

```
👤 Usuário interage com a tela
      │
      ▼
page / component
(estilizado com Tailwind)
      │
      ▼
query (TanStack Query)
ex: useGetColheitas()
      │
      ▼
service (axios)
ex: colheita.service.js
      │
      ▼
══════ HTTP ══════
 /api/colheitas
══════ HTTP ══════
      │
      ▼
React Query cache
atualiza os dados
      │
      ▼
componente re-renderiza
com os dados atualizados

─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
Se ocorrer erro:

React Query captura
      │
      ▼
interceptor do axios
      │
      ▼
trata o erro (toast, logout...)
─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
```

---

## 🛣️ Rotas da Aplicação

```
PÚBLICAS (AuthLayout — sem menu)
/login      → tela de login
/cadastro   → tela de cadastro

PRIVADAS (MainLayout — todos logados)
/           → dashboard (RF08)
/fazendas   → fazendas (RF01)
/colheitas  → colheitas (RF03)
/gastos     → gastos (RF05)
/lucros     → lucros (RF06)
/estoque    → estoque
/lembretes  → lembretes (RF10)
/simulacao  → calculadora de dívidas (RF09)

SÓ ADMIN (AdminRoute)
/relatorios → relatórios (RF04, RF07)
/ia         → insights IA (RF11)

SÓ FUNCIONARIO
/insumos    → registro de insumos (RF13)
```

---

## ▶️ Como Rodar

```bash
# Instalar dependências
npm install

# Copiar o .env
cp .env.example .env

# Rodar em desenvolvimento
npm run dev
# → http://localhost:5173

# Gerar build de produção
npm run build

# Rodar os testes
npm test

# Rodar o lint
npm run lint
```

---

## 📋 Scripts

| Script | Descrição |
|--------|-----------|
| `npm run dev` | Desenvolvimento com hot reload |
| `npm run build` | Build de produção |
| `npm run preview` | Preview do build |
| `npm test` | Testes |
| `npm run lint` | Lint |

---

## 🔑 Variáveis de Ambiente

Copie o `.env.example` e crie seu `.env`:

```bash
cp .env.example .env
env
VITE_API_URL=http://localhost:3333/api
`
```
