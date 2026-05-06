# InstaClone — Frontend (Vue 3)

## Sobre

O InstaClone é uma rede social inspirada no Instagram, construída como projeto final da disciplina. Este repositório contém o **frontend** da aplicação: uma SPA em Vue 3 que consome uma API RESTful externa (o backend do projeto vive em `../backend`).

A aplicação está integrada à API: autenticação por JWT, feed paginado por cursor, upload multipart de imagens e gerenciamento de seguidores/curtidas/comentários vêm todos do servidor. O único estado persistido localmente é o token de acesso, guardado em `localStorage` sob a chave `instaclone.token`.

## Stack

- **Vue 3** (`^3.5`) com `<script setup>`
- **Vite 8** como bundler/dev server
- **Vue Router 4** com histórico HTML5, guards globais e views lazy-loaded
- **Pinia 3** para estado compartilhado
- **Axios** como cliente HTTP, com interceptors de `Authorization` e `401`
- **Bootstrap 5** (reset/utilidades) + tema CSS próprio em [src/assets/styles/theme.css](src/assets/styles/theme.css)
- **Node.js** `^20.19.0 || >=22.12.0`

## Como Rodar

```bash
# instalar dependências
npm install

# subir em modo desenvolvimento (http://localhost:5173)
npm run dev

# build de produção para ./dist
npm run build

# pré-visualizar o build
npm run preview
```

### Variáveis de Ambiente

Copie [.env.example](.env.example) para `.env` e ajuste a URL da API se necessário:

```env
VITE_API_URL=http://localhost:8000/api
```

Quando a variável não é definida, o cliente HTTP em [src/services/api.js](src/services/api.js) usa `http://localhost:8000/api` como fallback.

### Docker

O projeto tem um build multi-stage ([Dockerfile](Dockerfile)) que gera os assets com Node e serve o `dist/` via Nginx. Para subir com Docker Compose:

```bash
docker compose up --build
```

O serviço fica exposto em `http://localhost:3000` ([compose.yaml](compose.yaml)). Passe `VITE_API_URL` para o build quando a API não estiver em `localhost:8000`.

## Estrutura do Código

```text
src/
  assets/styles/      tema e variáveis CSS globais
  components/
    feed/             PostCard, lista/form/item de comentários
    layout/           AppIcon
    profile/          AccountCard, avatar, header, cards de resumo e grid
  composables/        useImageUpload
  layouts/            AppLayout (área autenticada), AuthLayout (login/register)
  router/             rotas, guards e constantes de nomes/tipos de rota
  services/           clientes HTTP por domínio
  stores/             Pinia stores e helpers de perfil
  utils/              helpers de data
  views/
    app/              Feed, CreatePost, Discover, PostDetails, Profile,
                      EditProfile, ProfileConnections
    auth/             Login, Register
    NotFoundView
  App.vue             raiz (apenas <RouterView/>)
  main.js             bootstrap: Pinia, Router, configuração do axios
```

## Camada de Serviços

Todo acesso à API é centralizado em [src/services/](src/services/). O módulo [api.js](src/services/api.js) cria a instância Axios, injeta o token JWT no header `Authorization: Bearer ...` e dispara `clearSession()` no `auth` store quando a API responde com `401`. Também expõe o helper `extractErrorMessage` para traduzir respostas de erro da API em mensagens amigáveis.

Serviços disponíveis:

| Arquivo | Endpoints |
| --- | --- |
| [auth.service.js](src/services/auth.service.js) | `POST /auth/login`, `POST /auth/register`, `POST /auth/logout`, `GET /auth/me` |
| [users.service.js](src/services/users.service.js) | `GET /users/:username`, `PUT /users/me`, `POST /users/me/avatar`, `GET /users/search`, `GET /users/suggestions`, `GET /users/:id/posts` |
| [posts.service.js](src/services/posts.service.js) | `POST /posts`, `GET /posts/:id`, `PUT /posts/:id`, `DELETE /posts/:id` |
| [feed.service.js](src/services/feed.service.js) | `GET /feed` (paginação por cursor) |
| [likes.service.js](src/services/likes.service.js) | `POST /posts/:id/like`, `DELETE /posts/:id/like`, `GET /posts/:id/likes` |
| [comments.service.js](src/services/comments.service.js) | `GET/POST /posts/:id/comments`, `PUT/DELETE /comments/:id` |
| [follows.service.js](src/services/follows.service.js) | `POST /users/:id/follow`, `DELETE /users/:id/follow`, `GET /users/:id/followers`, `GET /users/:id/following`, `GET /users/:id/is-following` |

## Gerenciamento de Estado

O estado global fica em stores Pinia usados diretamente pelos componentes, normalmente com `storeToRefs` para manter reatividade:

- [stores/auth.js](src/stores/auth.js) — token, usuário autenticado, hidratação inicial via `GET /auth/me`, login/registro/logout e atualização do perfil.
- [stores/feed.js](src/stores/feed.js) — lista de posts do feed com paginação por cursor, criação/remoção de posts, curtidas, comentários e normalização de comentários.
- [stores/follows.js](src/stores/follows.js) — estado compartilhado de seguir/deixar de seguir, com `followingIds` e `pendingIds` em `Set`s substituídos a cada mutação para preservar a reatividade do Pinia.

Além dos stores, o helper [stores/profileUtils.js](src/stores/profileUtils.js) concentra normalização de usuários, `defaultAuthor()` e constantes de limite de perfil (`PROFILE_*_MAX_LENGTH`).

O composable [useImageUpload](src/composables/useImageUpload.js) concentra seleção de arquivo, preview via blob URL, validação de tipo/tamanho e limpeza do preview para as telas de criação de post e edição de perfil.

## Roteamento e Autenticação

As rotas estão definidas em [router/index.js](src/router/index.js), divididas em dois layouts:

- **`AppLayout`** (`meta.requiresAuth`): `/feed`, `/create`, `/discover`, `/posts/:postId`, `/profile`, `/profile/edit`, `/profile/list/:type`.
- **`AuthLayout`** (`meta.requiresGuest`): `/login`, `/register`.

Todas as views são lazy-loaded com `() => import(...)`, então cada tela vira seu próprio chunk no build; o build atual em `dist/` contém 24 arquivos JavaScript. Os nomes de rotas são centralizados em [router/routeNames.js](src/router/routeNames.js) por `ROUTE_NAMES`; os tipos válidos de lista de conexões ficam em `CONNECTION_LIST_TYPES`. Os nomes internos de rota e os paths usam inglês.

O `beforeEach` global hidrata a sessão na primeira navegação, redireciona para `/login` quando a rota exige autenticação e devolve o usuário logado ao feed caso tente acessar telas de convidado. Rotas desconhecidas caem em [NotFoundView](src/views/NotFoundView.vue).

## Telas Principais

- **Feed** — lista posts da rede do usuário com paginação por cursor e botão "Mostrar mais posts". Curtidas e envio de comentários atualizam o store imediatamente.
- **Criar Post** — tela de upload com preview da imagem, campo de legenda (limite de `POST_CAPTION_MAX_LENGTH = 2200`) e botão de publicar. A imagem é validada no cliente (JPG/PNG/WEBP, até 5 MB) e enviada via `multipart/form-data`; assim que a API confirma a criação, a publicação entra no topo do feed.
- **Descobrir** — lista sugestões de contas (`GET /users/suggestions`) com cards compartilhados por [AccountCard](src/components/profile/AccountCard.vue) e ação de seguir direto do card via `follows` store.
- **Detalhes do Post** — a tela individual de post exibe imagem, legenda, autor, data, contagem de curtidas e comentários usando [PostCommentList](src/components/feed/PostCommentList.vue), [PostCommentItem](src/components/feed/PostCommentItem.vue) e [PostCommentForm](src/components/feed/PostCommentForm.vue).
- **Perfil** — avatar, bio, contadores (posts/seguidores/seguindo), grade de posts do usuário, botão de seguir/deixar de seguir e atalho para editar o próprio perfil, com componentes próprios para header, cards de resumo e grid.
- **Editar Perfil** — atualiza nome, username, bio (`PUT /users/me`) e foto (`POST /users/me/avatar`) usando `useImageUpload`.
- **Conexões** (`/profile/list/:type`) — listagens paginadas de seguidores e seguidos, também usando `AccountCard` e o estado compartilhado de `follows`.
- **Login / Cadastro** — formulários que delegam para o `auth` store e já deixam a sessão ativa ao concluir.

## Layout Base

O [AppLayout](src/layouts/AppLayout.vue) monta uma sidebar de navegação (Home, Buscar, Criar, Perfil) e, quando a rota ativa é o feed, uma coluna lateral com a identidade do usuário e sugestões de contas para seguir. A área central troca de conteúdo via `<RouterView>` e adapta o modo de exibição (`feed`, `profile`, `default`) com base no `meta.navItem` da rota.

O ícone de coração usa [AppIcon](src/components/layout/AppIcon.vue) com a prop `filled`, garantindo que o estado curtido seja representado visualmente com preenchimento real.
