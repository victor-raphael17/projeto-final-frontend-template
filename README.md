# 📸 InstaClone — Frontend (Vue.js 3)

## Visão Geral

O InstaClone é uma rede social inspirada no Instagram, construída como projeto final da disciplina. O objetivo é aplicar todos os conceitos vistos ao longo do curso.

Este repositório contém o frontend do projeto: uma SPA (Single Page Application) construída com Vue.js 3 que consome a API RESTful do backend. A interface replica a experiência do Instagram com foco em mobile-first, comunicando-se com o servidor exclusivamente via JSON.

## Autenticação

As telas de login e cadastro permitem que o usuário acesse a plataforma. O token JWT recebido da API é salvo no localStorage e enviado em todas as requisições protegidas via interceptors do Axios. Usuários autenticados são redirecionados automaticamente para o feed; acessos sem token são bloqueados por guards de rota.

## Layout Principal

A navegação é feita por uma barra inferior (mobile) ou lateral (desktop) com links para Home, Explorar, Criar Post e Perfil. O layout base utiliza slots para áreas de conteúdo dinâmico (header, main, footer) e componentes dinâmicos (`<component :is>`) para troca de views.

## Feed

O feed exibe os posts das pessoas que o usuário segue, com scroll infinito ou paginação. Cada post mostra imagem, legenda, contagem de curtidas, comentários e data. É possível curtir/descurtir e comentar diretamente no feed, além de navegar para o perfil do autor.

## Criar Post

Tela de upload com preview da imagem, campo de legenda e botão de publicar. Exibe feedback visual de sucesso ou erro após a requisição.

## Perfil

A tela de perfil exibe foto, bio e contadores de posts, seguidores e seguindo, com um grid dos posts do usuário. Em perfis alheios aparece o botão seguir/deixar de seguir; no perfil próprio, o botão de editar perfil (foto, nome, bio). Há também listagens de seguidores e seguindo.

## Explorar

Grid de posts populares com barra de busca para encontrar usuários por nome ou username. Os resultados de busca linkam para o perfil encontrado.

## Detalhes do Post

Tela individual com listagem completa de comentários paginados, campo para adicionar comentário, contagem de curtidas e botão de deletar (visível apenas para o dono do post).
