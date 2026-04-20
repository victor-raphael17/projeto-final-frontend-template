# 📸 InstaClone (frontend) — Organização de Tasks

### Frontend (UI do insta-clone)

### 1 - Setup do Projeto
- [ ] Inicializar projeto (Vue)
- [ ] Configurar estrutura de pastas
- [ ] Configurar rotas do frontend (Vue Router)
- [ ] Configurar gerenciamento de estado compartilhado com Pinia
- [ ] Definir tema global (cores, fontes, espaçamentos no estilo Instagram)
- [ ] Configurar serviço HTTP (Axios) com interceptors pra JWT

### 2 - Autenticação
- [ ] Tela de Login
- [ ] Tela de Cadastro
- [ ] Centralizar sessão autenticada em store global
- [ ] Lógica de salvar/remover token no localStorage
- [ ] Redirecionamento automático (logado → feed, deslogado → login)
- [ ] Guard de rotas protegidas
- [ ] Configurar interceptor JWT no Axios

### 3 - Layout Principal
- [ ] Navbar inferior (mobile) ou lateral (desktop) — Home, Criar e Perfil
- [ ] Layout responsivo base (mobile-first)
- [ ] Usar slots no layout base para áreas de conteúdo dinâmico (header, main, footer)
- [ ] Usar componentes dinâmicos (`<component :is>`) para navegação ou troca de views

### 4 - Feed
- [ ] Componente de Post (imagem, legenda, likes, comentários, data)
- [ ] Listagem do feed (posts de quem você segue)
- [ ] Scroll infinito ou paginação
- [ ] Centralizar feed, curtidas e comentários em store global
- [ ] Ação de curtir/descurtir
- [ ] Ação de comentar inline
- [ ] Link pro perfil do autor

### 5 - Criar Post
- [ ] Tela de upload de imagem
- [ ] Preview da imagem
- [ ] Campo de legenda
- [ ] Botão de publicar
- [ ] Feedback de sucesso/erro

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
