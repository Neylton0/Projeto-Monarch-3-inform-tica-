# 👑 Monarch - Sistema de Gestão de Tempo Gamificado

Um aplicativo web moderno e completo para gerenciar tarefas, usar a técnica Pomodoro e ganhar recompensas através de um sistema de gamificação com XP, níveis e conquistas.

![Monarch Landing Page](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)

---

## 🚀 Início Rápido

### Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Node.js** 18+ ([Download](https://nodejs.org/))
- **pnpm** 10+ ([Instalação](https://pnpm.io/installation))
- **Git** ([Download](https://git-scm.com/))

### Instalação a partir do GitHub

#### 1️⃣ Clone o Repositório

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/monarch.git

# Navegue até a pasta do projeto
cd monarch
```

#### 2️⃣ Instale as Dependências

```bash
# Instale todas as dependências do projeto
pnpm install
```

#### 3️⃣ Configure as Variáveis de Ambiente

O projeto usa autenticação OAuth do Manus. As variáveis de ambiente já estão configuradas no servidor Manus, mas se você quiser rodar localmente com suas próprias credenciais:

```bash
# Crie um arquivo .env.local na raiz do projeto
cp .env.example .env.local
```

**Variáveis necessárias** (já fornecidas pelo servidor Manus):
- `DATABASE_URL` - Conexão com o banco de dados
- `JWT_SECRET` - Chave para assinar tokens
- `VITE_APP_ID` - ID da aplicação OAuth
- `OAUTH_SERVER_URL` - URL do servidor OAuth

#### 4️⃣ Configure o Banco de Dados

```bash
# Execute as migrações do banco de dados
pnpm drizzle-kit generate
pnpm drizzle-kit migrate
```

#### 5️⃣ Inicie o Servidor de Desenvolvimento

```bash
# Inicie o servidor em modo desenvolvimento
pnpm dev
```

O servidor estará disponível em `http://localhost:3000`

---

## 📋 Funcionalidades Principais

### ✅ Lista de Tarefas
- Criar, editar, concluir e excluir tarefas
- Prioridades: Baixa, Média, Alta
- Categorias personalizáveis
- Filtros por prioridade e categoria
- XP automático por tarefa concluída

### ⏱️ Temporizador Pomodoro
- **Ciclo de foco**: 25 minutos
- **Pausa curta**: 5 minutos
- **Pausa longa**: 15 minutos (após 4 Pomodoros)
- Notificações ao fim de cada ciclo
- Persistência de sessões concluídas
- Ganho de XP por sessão completada

### ⭐ Sistema de XP e Níveis
- Ganhe XP completando tarefas e Pomodoros
- Evolua de nível a cada 100 XP
- Visualize seu progresso em tempo real
- Barra de progresso visual

### 🏆 Conquistas (Badges)
- 10+ badges desbloqueáveis
- Marcos: Primeiras tarefas, sequências diárias, Pomodoros completados
- Painel de conquistas com próximas metas
- Notificações ao desbloquear

### 🎯 Metas Diárias
- Defina metas de tarefas e Pomodoros
- Progresso em tempo real
- Recompensas XP ao atingir metas
- Atualização automática

### 📊 Dashboard
- Visão geral do progresso diário
- Nível atual e XP
- Próximas tarefas
- Conquistas recentes
- Gráficos de produtividade (últimos 7 dias)
- 5 abas: Visão Geral, Tarefas, Pomodoro, Conquistas, Estatísticas

### 🎨 Design Responsivo
- Tema claro e escuro
- Paleta roxa moderna
- Interface responsiva (mobile, tablet, desktop)
- Componentes shadcn/ui + Tailwind CSS

### 🔐 Autenticação
- Manus OAuth integrado
- Dados persistentes por usuário
- Logout seguro

---

## 🏗️ Arquitetura do Projeto

### Estrutura de Pastas

```
monarch/
├── client/                      # Frontend React
│   ├── src/
│   │   ├── pages/              # Páginas principais
│   │   │   ├── Home.tsx        # Landing page pública
│   │   │   ├── Dashboard.tsx   # Dashboard principal
│   │   │   └── NotFound.tsx    # Página 404
│   │   ├── components/         # Componentes reutilizáveis
│   │   │   ├── TasksList.tsx
│   │   │   ├── PomodoroTimer.tsx
│   │   │   ├── AchievementsPanel.tsx
│   │   │   ├── DailyGoalsPanel.tsx
│   │   │   ├── ProductivityChart.tsx
│   │   │   └── DashboardLayout.tsx
│   │   ├── contexts/           # React Contexts
│   │   │   └── ThemeContext.tsx
│   │   ├── hooks/              # Custom Hooks
│   │   ├── lib/
│   │   │   └── trpc.ts        # Cliente tRPC
│   │   ├── App.tsx             # Roteamento principal
│   │   ├── main.tsx            # Entry point
│   │   └── index.css           # Estilos globais
│   ├── public/                 # Assets públicos
│   └── index.html              # HTML principal
│
├── server/                      # Backend Express + tRPC
│   ├── routers.ts              # Procedures tRPC
│   ├── db.ts                   # Helpers do banco de dados
│   ├── storage.ts              # Helpers de armazenamento S3
│   ├── auth.logout.test.ts     # Testes de autenticação
│   ├── monarch.test.ts         # Testes principais
│   └── _core/                  # Configurações internas
│       ├── index.ts            # Servidor Express
│       ├── context.ts          # Contexto tRPC
│       ├── trpc.ts             # Setup tRPC
│       ├── oauth.ts            # Autenticação OAuth
│       ├── env.ts              # Variáveis de ambiente
│       └── ...
│
├── drizzle/                     # Banco de dados
│   ├── schema.ts               # Definição das tabelas
│   ├── relations.ts            # Relações entre tabelas
│   └── migrations/             # Migrações SQL
│
├── shared/                      # Código compartilhado
│   ├── const.ts                # Constantes
│   └── types.ts                # Tipos TypeScript
│
├── package.json                # Dependências do projeto
├── tsconfig.json               # Configuração TypeScript
├── vite.config.ts              # Configuração Vite
├── vitest.config.ts            # Configuração Vitest
└── drizzle.config.ts           # Configuração Drizzle ORM
```

### Stack Tecnológico

**Frontend:**
- React 19 com TypeScript
- Vite para build rápido
- Tailwind CSS 4 para estilos
- shadcn/ui para componentes
- Wouter para roteamento
- tRPC para chamadas RPC tipadas
- Framer Motion para animações

**Backend:**
- Express.js para servidor HTTP
- tRPC para procedures tipadas
- Drizzle ORM para banco de dados
- MySQL/TiDB para persistência
- Manus OAuth para autenticação

**Testing:**
- Vitest para testes unitários
- Cobertura de funcionalidades principais

---

## 🛠️ Desenvolvimento

### Comandos Disponíveis

```bash
# Iniciar servidor de desenvolvimento
pnpm dev

# Build para produção
pnpm build

# Iniciar servidor de produção
pnpm start

# Executar testes
pnpm test

# Verificar tipos TypeScript
pnpm check

# Formatar código
pnpm format

# Gerar migrações do banco
pnpm drizzle-kit generate

# Executar migrações
pnpm drizzle-kit migrate
```

### Fluxo de Desenvolvimento

#### 1. Adicionar Nova Tabela no Banco

```typescript
// drizzle/schema.ts
export const minhaTabela = mysqlTable("minha_tabela", {
  id: int("id").autoincrement().primaryKey(),
  nome: varchar("nome", { length: 255 }).notNull(),
  createdAt: timestamp("createdAt").defaultNow().notNull(),
});
```

#### 2. Gerar Migração

```bash
pnpm drizzle-kit generate
```

#### 3. Executar Migração

```bash
pnpm drizzle-kit migrate
```

#### 4. Criar Helper no Banco

```typescript
// server/db.ts
export async function obterMinhaTabela(id: number) {
  const db = await getDb();
  return await db.select().from(minhaTabela).where(eq(minhaTabela.id, id));
}
```

#### 5. Criar Procedure tRPC

```typescript
// server/routers.ts
export const appRouter = router({
  minhaFeature: router({
    obter: protectedProcedure
      .input(z.object({ id: z.number() }))
      .query(async ({ input, ctx }) => {
        return await obterMinhaTabela(input.id);
      }),
  }),
});
```

#### 6. Usar no Frontend

```typescript
// client/src/pages/MeuComponente.tsx
const { data } = trpc.minhaFeature.obter.useQuery({ id: 1 });
```

#### 7. Escrever Testes

```typescript
// server/minha-feature.test.ts
describe("minhaFeature", () => {
  it("deve obter dados", async () => {
    const caller = appRouter.createCaller(ctx);
    const resultado = await caller.minhaFeature.obter({ id: 1 });
    expect(resultado).toBeDefined();
  });
});
```

---

## 🗄️ Banco de Dados

### Tabelas Principais

| Tabela | Descrição |
|--------|-----------|
| `users` | Usuários autenticados |
| `tasks` | Tarefas criadas pelos usuários |
| `pomodoroSessions` | Sessões Pomodoro completadas |
| `dailyGoals` | Metas diárias dos usuários |
| `userStats` | Estatísticas agregadas (XP, nível) |
| `achievements` | Definição de conquistas disponíveis |
| `userAchievements` | Conquistas desbloqueadas por usuário |
| `xpHistory` | Histórico de ganho de XP |

### Conexão com o Banco

A conexão é estabelecida automaticamente via `DATABASE_URL`. Para desenvolvimento local:

```bash
# Exemplo de DATABASE_URL
DATABASE_URL="mysql://usuario:senha@localhost:3306/monarch"
```

---

## 🧪 Testes

O projeto inclui testes unitários com Vitest:

```bash
# Executar todos os testes
pnpm test

# Executar testes em modo watch
pnpm test --watch

# Executar testes com cobertura
pnpm test --coverage
```

### Testes Inclusos

- ✅ Cálculo de XP por tarefa
- ✅ Evolução de nível
- ✅ Desbloqueio de conquistas
- ✅ Progresso de metas diárias
- ✅ Ciclos Pomodoro
- ✅ Autenticação e logout

---

## 🎨 Personalizando o Tema

### Paleta de Cores

Os temas claro e escuro estão definidos em `client/src/index.css`:

```css
/* Tema Claro */
@media (prefers-color-scheme: light) {
  :root {
    --background: 0 0% 100%;
    --foreground: 280 20% 20%;
    --primary: 280 100% 50%;
    --accent: 280 80% 60%;
  }
}

/* Tema Escuro */
@media (prefers-color-scheme: dark) {
  :root {
    --background: 280 20% 10%;
    --foreground: 0 0% 95%;
    --primary: 280 100% 60%;
    --accent: 280 80% 50%;
  }
}
```

Para mudar as cores, edite os valores CSS acima.

### Adicionar Novo Tema

1. Crie novas variáveis CSS em `index.css`
2. Adicione um contexto em `ThemeContext.tsx`
3. Use `useTheme()` para alternar

---

## 🚀 Deploy

### Opção 1: Manus (Recomendado)

O projeto está pronto para deploy no Manus:

1. Acesse o Management UI
2. Clique em **Publish** (requer checkpoint)
3. Seu site estará disponível em `monarchtm-m2rghkdh.manus.space`

### Opção 2: Vercel

```bash
# Instale Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### Opção 3: Railway

```bash
# Instale Railway CLI
npm i -g @railway/cli

# Deploy
railway up
```

### Opção 4: Docker

```bash
# Build da imagem
docker build -t monarch .

# Executar container
docker run -p 3000:3000 monarch
```

---

## 📚 Documentação Adicional

### Autenticação

O Monarch usa Manus OAuth para autenticação:

```typescript
// Obter usuário autenticado
const { user } = useAuth();

// Fazer logout
const { logout } = useAuth();
await logout();

// Obter URL de login
const loginUrl = getLoginUrl();
```

### Armazenamento de Arquivos

Arquivos são armazenados no S3 via helpers:

```typescript
import { storagePut, storageGet } from "./server/storage";

// Upload
const { url } = await storagePut("arquivo.txt", dados, "text/plain");

// Download (presigned URL)
const { url } = await storageGet("arquivo.txt");
```

### Notificações

Enviar notificações para o dono do projeto:

```typescript
import { notifyOwner } from "./server/_core/notification";

await notifyOwner({
  title: "Nova Tarefa Concluída",
  content: "Usuário completou uma tarefa importante",
});
```

---

## 🐛 Troubleshooting

### Erro: "Cannot find module 'drizzle-orm'"

```bash
pnpm install
```

### Erro: "Database connection failed"

Verifique se `DATABASE_URL` está configurado corretamente:

```bash
echo $DATABASE_URL
```

### Erro: "Port 3000 already in use"

Use uma porta diferente:

```bash
PORT=3001 pnpm dev
```

### Erro: "OAuth callback failed"

Certifique-se de que `VITE_APP_ID` e `OAUTH_SERVER_URL` estão corretos.

---

## 📖 Recursos Úteis

- [React Documentation](https://react.dev)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [tRPC Documentation](https://trpc.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Drizzle ORM Documentation](https://orm.drizzle.team/docs/overview)
- [Vitest Documentation](https://vitest.dev)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um fork do repositório
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

---

## 📝 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

## 👤 Autor

**Monarch Team**

- 🌐 Website: [monarchtm-m2rghkdh.manus.space](https://monarchtm-m2rghkdh.manus.space)
- 📧 Email: contato@monarch.local

---

## 🙏 Agradecimentos

- [React](https://react.dev) - Biblioteca UI
- [Tailwind CSS](https://tailwindcss.com) - Framework CSS
- [shadcn/ui](https://ui.shadcn.com) - Componentes UI
- [tRPC](https://trpc.io) - RPC Framework
- [Drizzle ORM](https://orm.drizzle.team) - ORM para Node.js

---

## 📞 Suporte

Se encontrar problemas ou tiver dúvidas:

1. Verifique a seção [Troubleshooting](#-troubleshooting)
2. Abra uma [Issue](https://github.com/seu-usuario/monarch/issues)
3. Consulte a [Documentação](#-documentação-adicional)

---

**Desenvolvido com ❤️ usando React, TypeScript e Tailwind CSS**

**Versão**: 1.0.0 | **Última atualização**: Junho 2026
