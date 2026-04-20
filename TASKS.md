# 📸 InstaClone (frontend) — Organização de Tasks

### Frontend (UI do insta-clone)

### 1 - Setup do Projeto
- [x] Inicializar projeto (Vue)
- [x] Configurar estrutura de pastas
- [x] Configurar rotas do frontend (Vue Router)
- [x] Definir tema global (cores, fontes, espaçamentos no estilo Instagram)
- [ ] Configurar serviço HTTP (Axios) com interceptors pra JWT

### 2 - Autenticação
- [x] Tela de Login
- [x] Tela de Cadastro
- [x] Lógica de salvar/remover token no localStorage
- [x] Redirecionamento automático (logado → feed, deslogado → login)
- [x] Guard de rotas protegidas
- [SKIP] Configurar interceptor JWT no Axios

### 3 - Layout Principal
- [x] Navbar inferior (mobile) ou lateral (desktop) — Home, Explorar, Criar, Notificações, Perfil
- [x] Layout responsivo base (mobile-first)
- [x] Usar slots no layout base para áreas de conteúdo dinâmico (header, main, footer)
- [x] Usar componentes dinâmicos (`<component :is>`) para navegação ou troca de views

### 4 - Feed
- [x] Componente de Post (imagem, legenda, likes, comentários, data)
- [x] Listagem do feed (posts de quem você segue)
- [x] Scroll infinito ou paginação
- [x] Ação de curtir/descurtir
- [x] Ação de comentar inline
- [x] Link pro perfil do autor

### 5 - Stories
- [ ] Barra de stories no topo do feed
- [ ] Visualizador de story (tela cheia, progresso, tap pra próximo)
- [ ] Indicador de "já visto" vs "novo"
- [ ] Tela de criação de story (upload de imagem)

### 6 - Criar Post
- [ ] Tela de upload de imagem
- [ ] Preview da imagem
- [ ] Campo de legenda
- [ ] Botão de publicar
- [ ] Feedback de sucesso/erro

### 7 - Perfil
- [ ] Tela de perfil (foto, bio, contadores: posts, seguidores, seguindo)
- [ ] Grid de posts do usuário
- [ ] Botão seguir/deixar de seguir (perfil alheio)
- [ ] Botão editar perfil (perfil próprio)
- [ ] Tela de editar perfil (foto, nome, bio)
- [ ] Lista de seguidores
- [ ] Lista de seguindo

### 8 - Explorar
- [ ] Grid de posts populares
- [ ] Barra de busca (buscar usuários por nome/username)
- [ ] Resultado de busca com link pro perfil

### 9 - Notificações
- [ ] Tela de listagem de notificações
- [ ] Tipos: curtida, comentário, novo seguidor
- [ ] Marcar como lida
- [ ] Polling a cada X segundos pra checar novas notificações (badge no ícone)

### 10 - Detalhes do Post
- [ ] Tela individual do post
- [ ] Listagem de comentários paginada (com botão "carregar mais")
- [ ] Campo pra adicionar comentário
- [ ] Contagem de curtidas
- [ ] Botão de deletar (se for dono)
