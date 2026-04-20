# 📸 InstaClone — Frontend (Vue.js 3)

## Visão Geral

O InstaClone é uma rede social inspirada no Instagram, construída como projeto final da disciplina. O objetivo é aplicar todos os conceitos vistos ao longo do curso.

Este repositório contém o frontend do projeto: uma SPA (Single Page Application) construída com Vue.js 3, Vue Router e Pinia. No estado atual, a aplicação funciona em modo local-first: autenticação, sessão e feed ficam persistidos no `localStorage` enquanto a integração completa com a API RESTful continua como próximo passo.

## Gerenciamento de Estado

O estado compartilhado foi centralizado com Pinia para os fluxos que já exigem consistência entre telas:

- `src/stores/auth.js`: sessão autenticada, usuário atual, hidratação inicial e contas locais de teste.
- `src/stores/feed.js`: posts do feed, curtidas, comentários, criação de posts e resumo de perfil.

Estados transitórios, como campos de formulário, preview de upload e mensagens momentâneas de feedback, continuam locais nas views porque ainda não precisam ser globais.

## Autenticação

As telas de login e cadastro usam contas locais persistidas no navegador. O store de autenticação hidrata perfis seed para teste, mantém a sessão ativa com token mock e atualiza os dados do usuário atual sempre que o perfil é editado. Usuários autenticados são redirecionados automaticamente para o feed; acessos sem sessão ativa continuam bloqueados por guards de rota.

## Layout Principal

A navegação é feita por uma barra inferior (mobile) ou lateral (desktop) com links para Home, Criar Post e Perfil. O layout base utiliza slots para áreas de conteúdo dinâmico (header, main, footer) e componentes dinâmicos (`<component :is>`) para troca de views.

## Feed

O feed exibe os posts das pessoas que o usuário segue, com paginação simples. Cada post mostra imagem, legenda, contagem de curtidas, comentários e data. Curtidas, comentários e novos posts atualizam o store do feed imediatamente e ficam persistidos localmente no navegador.

## Criar Post

Tela de upload com preview da imagem, campo de legenda e botão de publicar. A imagem é otimizada no cliente antes de ser salva, e a publicação entra no topo do feed assim que o store confirma a criação local.

## Perfil

A área de perfil agora reúne avatar, bio, contadores de posts/seguidores/seguindo, grade de posts do usuário, botão de seguir/deixar de seguir para perfis alheios, edição do próprio perfil e telas dedicadas para listar seguidores e perfis seguidos. Tudo isso permanece em modo local-first, sincronizado entre `auth` e `feed`.

## Detalhes do Post

A tela individual de post agora exibe imagem, legenda, autor, localização, data, contagem de curtidas e comentários em um layout dedicado. Os comentários aparecem paginados com botão de carregar mais, seguem aceitando novos envios na própria tela e, quando o post pertence ao usuário autenticado, a interface também libera a ação de deletar a publicação.
