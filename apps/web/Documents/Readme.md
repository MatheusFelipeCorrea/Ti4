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
    ├── 📄 favicon.ico   → ícone da aba do navegador
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
→ Exibe: nome do usuário logado

Sidebar/
→ Navegação lateral
→ Links para todas as páginas do sistema
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
→ Tela inicial do sistema
→ Exibe: gráfico custos x vendas (RF07)
→ Exibe: saldo de sacas em estoque (RF08)
→ Exibe: cotação do dólar (RF05)
→ Rota: /

Fazendas/
→ Listagem de fazendas cadastradas
→ Ações: criar, editar, deletar
→ Rota: /fazendas

Safras/
→ Listagem de safras por fazenda
→ Ações: criar, editar, deletar
→ Rota: /safras

Custos/
→ Listagem de custos por safra
→ Ações: criar, editar, deletar
→ Rota: /custos

Vendas/
→ Listagem de vendas por safra
→ Ações: criar, editar, deletar
→ Rota: /vendas

Estoque/
→ Saldo de sacas disponíveis por safra
→ Calculado: sacas produzidas - sacas vendidas
→ Rota: /estoque

Relatorios/
→ Relatórios financeiros com filtro por data
→ Exibe: lucro por safra (RF09)
→ Exibe: custos por cultura (RF10)
→ Exibe: preço mínimo de venda (RF11)
→ Rota: /relatorios

Simulacao/
→ Simulação de venda
→ Calcula: estoque × cotação do dólar (RF06)
→ Máximo 4 cliques a partir do dashboard (RNF02)
→ Rota: /simulacao

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
→ Só renderiza o conteúdo da página

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
→ isAuthenticated: true | false
→ setUser(user)  → salva o usuário
→ clearUser()    → limpa ao fazer logout

slices/uiSlice.js
→ Controla sidebar aberta ou fechada
→ Controla tema (dark | light)

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

safra.service.js
→ buscarTodas()                    → GET    /api/safras
→ buscarPorFazenda(fazendaId)      → GET    /api/safras/fazenda/:fazendaId
→ criar(dados)                     → POST   /api/safras
→ atualizar(id, dados)             → PUT    /api/safras/:id
→ deletar(id)                      → DELETE /api/safras/:id

custo.service.js
→ buscarTodos()                    → GET    /api/custos
→ buscarPorSafra(safraId)          → GET    /api/custos/safra/:safraId
→ criar(dados)                     → POST   /api/custos
→ atualizar(id, dados)             → PUT    /api/custos/:id
→ deletar(id)                      → DELETE /api/custos/:id

venda.service.js
→ buscarTodas()                    → GET    /api/vendas
→ buscarPorSafra(safraId)          → GET    /api/vendas/safra/:safraId
→ criar(dados)                     → POST   /api/vendas
→ atualizar(id, dados)             → PUT    /api/vendas/:id
→ deletar(id)                      → DELETE /api/vendas/:id

estoque.service.js
→ buscarTodos()                    → GET    /api/estoque
→ buscarPorSafra(safraId)          → GET    /api/estoque/safra/:safraId

cotacao.service.js
→ buscarDolar()                    → GET    /api/cotacao/dollar

relatorio.service.js
→ buscarCustosVsVendas(filtros)    → GET    /api/relatorios/custos-vs-vendas
→ buscarLucroPorSafra(id, filtros) → GET    /api/relatorios/lucro/:safraId
→ buscarCustosPorCultura(filtros)  → GET    /api/relatorios/custos-por-cultura
→ buscarPrecoMinimo(filtros)       → GET    /api/relatorios/min-preco

simulacao.service.js
→ simularVenda(dados)              → POST   /api/simulacao/venda

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
→ useGetFazendas()      → lista todas as fazendas
→ useGetFazenda(id)     → busca uma fazenda
→ useCreateFazenda()    → cria fazenda
→ useUpdateFazenda()    → atualiza fazenda
→ useDeleteFazenda()    → deleta fazenda

useSafraQueries.js
→ useGetSafras()
→ useGetSafrasPorFazenda(fazendaId)
→ useCreateSafra()
→ useUpdateSafra()
→ useDeleteSafra()

useCustoQueries.js
→ useGetCustos()
→ useGetCustosPorSafra(safraId)
→ useCreateCusto()
→ useUpdateCusto()
→ useDeleteCusto()

useVendaQueries.js
→ useGetVendas()
→ useGetVendasPorSafra(safraId)
→ useCreateVenda()
→ useUpdateVenda()
→ useDeleteVenda()

useEstoqueQueries.js
→ useGetEstoque()
→ useGetEstoquePorSafra(safraId)

useCotacaoQueries.js
→ useGetCotacaoDolar()   → busca cotação em tempo real

useRelatorioQueries.js
→ useGetCustosVsVendas(filtros)
→ useGetLucroPorSafra(safraId, filtros)
→ useGetCustosPorCultura(filtros)
→ useGetPrecoMinimo(filtros)

useSimulacaoQueries.js
→ useSimularVenda()

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
    SAFRAS: '/safras',
    CUSTOS: '/custos',
    VENDAS: '/vendas',
    ESTOQUE: '/estoque',
    RELATORIOS: '/relatorios',
    SIMULACAO: '/simulacao',
  }

api.js
→ API = {
    AUTH: { LOGIN: '/auth/login', CADASTRO: '/auth/cadastro' },
    FAZENDAS: '/fazendas',
    SAFRAS: '/safras',
    CUSTOS: '/custos',
    VENDAS: '/vendas',
    ESTOQUE: '/estoque',
    COTACAO: '/cotacao/dollar',
    RELATORIOS: '/relatorios',
    SIMULACAO: '/simulacao/venda',
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
 ex: useGetFazendas()
        │
        ▼
 service (axios)
 ex: fazenda.service.js
        │
        ▼
══════ HTTP ══════
   /api/fazendas
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

PRIVADAS (MainLayout — com menu)
/           → dashboard
/fazendas   → fazendas
/safras     → safras
/custos     → custos
/vendas     → vendas
/estoque    → estoque
/relatorios → relatórios
/simulacao  → simulação de venda
```

---

## ▶️ Como Rodar

```bash
# Instalar dependências
npm install

# Rodar em desenvolvimento
npm run dev

# Gerar build de produção
npm run build

# Rodar os testes
npm test

# Rodar o lint
npm run lint
```

---

## 🔑 Variáveis de Ambiente

Copie o `.env.example` e crie seu `.env`:

```bash
cp .env.example .env
env
VITE_API_URL=http://localhost:3333/api
`

---