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

As telas de login e cadastro usam contas locais de teste. O token mock e os dados do usuário autenticado são salvos no `localStorage` e hidratados pelo store de autenticação assim que a aplicação sobe. Usuários autenticados são redirecionados automaticamente para o feed; acessos sem sessão ativa continuam bloqueados por guards de rota.

## Layout Principal

A navegação é feita por uma barra inferior (mobile) ou lateral (desktop) com links para Home, Criar Post e Perfil. O layout base utiliza slots para áreas de conteúdo dinâmico (header, main, footer) e componentes dinâmicos (`<component :is>`) para troca de views.

## Feed

O feed exibe os posts das pessoas que o usuário segue, com paginação simples. Cada post mostra imagem, legenda, contagem de curtidas, comentários e data. Curtidas, comentários e novos posts atualizam o store do feed imediatamente e ficam persistidos localmente no navegador.

## Criar Post

Tela de upload com preview da imagem, campo de legenda e botão de publicar. A imagem é otimizada no cliente antes de ser salva, e a publicação entra no topo do feed assim que o store confirma a criação local.

## Perfil

A tela de perfil já mostra avatar, bio e métricas derivadas do feed local para o usuário atual ou para autores acessados a partir do feed. Edição de perfil, relacionamento entre contas e grid completo de posts continuam como próximos incrementos.

## Explorar

A área de explorar ainda está reservada para a próxima etapa. A estrutura de rota e layout já está pronta para receber grid de descoberta, busca por usuários e filtros.

## Detalhes do Post

A tela individual de post ainda não foi implementada. Hoje as interações principais acontecem direto no feed, e o detalhamento completo fica como evolução futura.
