# 📸 InstaClone (frontend) — Organização de Tasks

### Frontend (UI do insta-clone)

### 1 - Setup do Projeto
- [x] Inicializar projeto (Vue)
- [x] Configurar estrutura de pastas
- [x] Configurar rotas do frontend (Vue Router)
- [x] Configurar gerenciamento de estado compartilhado com Pinia
- [x] Definir tema global (cores, fontes, espaçamentos no estilo Instagram)
- [ ] Configurar serviço HTTP (Axios) com interceptors pra JWT

### 2 - Autenticação
- [x] Tela de Login
- [x] Tela de Cadastro
- [x] Centralizar sessão autenticada em store global
- [x] Lógica de salvar/remover token no localStorage
- [x] Redirecionamento automático (logado → feed, deslogado → login)
- [x] Guard de rotas protegidas
- [SKIP] Configurar interceptor JWT no Axios

### 3 - Layout Principal
- [x] Navbar inferior (mobile) ou lateral (desktop) — Home, Explorar, Criar e Perfil
- [x] Layout responsivo base (mobile-first)
- [x] Usar slots no layout base para áreas de conteúdo dinâmico (header, main, footer)
- [x] Usar componentes dinâmicos (`<component :is>`) para navegação ou troca de views

### 4 - Feed
- [x] Componente de Post (imagem, legenda, likes, comentários, data)
- [x] Listagem do feed (posts de quem você segue)
- [x] Scroll infinito ou paginação
- [x] Centralizar feed, curtidas e comentários em store global
- [x] Ação de curtir/descurtir
- [x] Ação de comentar inline
- [x] Link pro perfil do autor

### 5 - Criar Post
- [x] Tela de upload de imagem
- [x] Preview da imagem
- [x] Campo de legenda
- [x] Botão de publicar
- [x] Feedback de sucesso/erro

### 6 - Perfil
- [ ] Tela de perfil (foto, bio, contadores: posts, seguidores, seguindo)
- [ ] Grid de posts do usuário
- [ ] Botão seguir/deixar de seguir (perfil alheio)
- [ ] Botão editar perfil (perfil próprio)
- [ ] Tela de editar perfil (foto, nome, bio)
- [ ] Lista de seguidores
- [ ] Lista de seguindo

### 8 - Detalhes do Post
- [ ] Tela individual do post
- [ ] Listagem de comentários paginada (com botão "carregar mais")
- [ ] Campo pra adicionar comentário
- [ ] Contagem de curtidas
- [ ] Botão de deletar (se for dono)
