## ▶️ Como Rodar

```bash
# 1. Clonar o repositório
git clone https://github.com/seu-usuario/projeto.git

# 2. Entrar na pasta do backend
cd apps/api

# 3. Instalar dependências
npm install

# 4. Copiar o .env
cp .env.example .env
# → abrir o .env e preencher com os dados reais (Pegar com o Matheus)

# 5. Gerar o client do Prisma
npx prisma generate

# 6. Popular o banco com dados iniciais (apenas na primeira vez)
npm run db:seed

# 7. Rodar o servidor
npm run dev
# → servidor rodando em http://localhost:3333
```
> ⚠️ **Importante:** não rodar `npx prisma migrate dev`
> O banco já está criado e configurado no Neon.
> Rodar migrate pode gerar conflitos desnecessários.
---

## 📋 Descrição dos Scripts

| Script | Descrição |
|--------|-----------|
| `npm run dev` | Sobe o servidor em desenvolvimento com reinício automático (Node --watch) |
| `npm start` | Sobe o servidor em produção sem reinício automático |
| `npm run lint` | Verifica qualidade do código com ESLint |
| `npm test` | Roda todos os testes |
| `npm run test:coverage` | Roda os testes com relatório de cobertura |
| `npm run db:migrate` | Cria/atualiza as tabelas no banco — usar sempre que houver mudanças no schema |
| `npm run db:generate` | Gera o client do Prisma — usar sempre após mudanças no schema.prisma |
| `npm run db:studio` | Abre interface visual do banco — útil para visualizar dados em desenvolvimento |
| `npm run db:seed` | Popula o banco com dados iniciais — executar uma única vez ao configurar |
| `npm run db:reset` | ⚠️ APAGA TUDO e recria o banco — usar apenas em desenvolvimento |

---

## ⚠️ Ordem importante

Sempre que **clonar ou atualizar** o projeto:

```bash
npm install             # instala dependências
cp .env.example .env    # configura variáveis (preencher o .env depois)
npx prisma generate     # gera o client do Prisma
npx prisma migrate dev  # atualiza o banco
npm run dev             # sobe o servidor
```

Apenas na **primeira vez**:

```bash
npm run db:seed         # popula o banco com dados iniciais
```

> ⚠️ **Importante:** sempre use `npx prisma` ao invés de `prisma` direto
> para garantir que todos do time usem a mesma versão do projeto.