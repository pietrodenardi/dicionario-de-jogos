Markdown

# 📄 Product Requirements Document (PRD) - Backlog Log

## 1. Visão Geral e Objetivo

Acompanhar o progresso em jogos de video game, organizar a coleção pessoal e decidir qual será a próxima jogatina pode ser um desafio, especialmente para quem possui títulos distribuídos em diferentes plataformas (PC, PlayStation, Xbox, Nintendo Switch).

Atualmente, o controle desses jogos costuma ser feito de maneira informal, por meio de planilhas complexas, anotações soltas ou mensagens com amigos, o que resulta na perda de dados sobre horas jogadas, avaliações pessoais e histórico de zeramentos.

Diante desse cenário, o projeto **Backlog Log** tem como objetivo criar uma plataforma centralizada para organizar a coleção de video games de um usuário e acompanhar seu progresso no backlog de forma interativa e visual.

Cada usuário poderá cadastrar os jogos que possui ou deseja jogar, registrando o status de cada obra (*Jogando*, *Concluído*, *Na Fila*, *Lista de Desejos*), o tempo investido, notas e avaliações pessoais. Além disso, a plataforma integrará APIs externas para buscar dados reais e capas de jogos, permitindo também o compartilhamento e consulta de estatísticas com outros gamers.

O projeto foi inicialmente pensado como um gerenciador pessoal, mas será desenvolvido de forma modular para que qualquer jogador possa catalogar e acompanhar sua jornada gamer de forma simples e eficiente.

---

## 2. Atores do Sistema

* **Visitante:** Usuário que ainda não possui uma conta e pode acessar as páginas públicas do sistema, visualizar a biblioteca pública de destaques e realizar seu cadastro.
* **Usuário / Collector:** Pessoa que possui uma conta registrada e pode cadastrar seus jogos, atualizar status de progresso, registrar avaliações, consultar dados em APIs externas e gerenciar sua coleção local/remota.
* **Administrador da Coleção:** O próprio usuário no papel de gestor de sua biblioteca, sendo responsável por editar, atualizar tempo de jogo ou remover itens do seu backlog.

> 💡 **Nota:** Um mesmo usuário exercerá as funções de **Collector** e **Administrador da Coleção** dentro da sua área privativa no sistema.

---

## 3. Histórias de Usuário e Escopo

Abaixo estão as funcionalidades descritas sob a perspectiva dos usuários finais do **Backlog Log**.

### 🔐 Épico 1: Autenticação e Perfil

* **US01 - Login de Jogador:** Como um usuário cadastrado, quero inserir minhas credenciais para acessar minha coleção pessoal no Backlog Log.
  * **Critérios de Aceitação:** O sistema deve validar as credenciais informadas antes de permitir o acesso ao painel e persistir o estado da sessão no `sessionStorage`.
* **US02 - Controle de Acesso:** Como um usuário, quero que o gerenciamento da minha biblioteca privada esteja disponível somente após o login, para manter meu histórico e notas protegidos.

---

### 🎮 Épico 2: Catalogações e Biblioteca de Jogos

* **US03 - Cadastro de Jogo via API Real:** Como um usuário, quero pesquisar um jogo através da RAWG API (ou IGDB API) e adicioná-lo à minha biblioteca.
  * **Critérios de Aceitação:** O sistema deve permitir pesquisar títulos em tempo real, auto-completar a capa, ano de lançamento e gênero, permitindo ao usuário selecionar o resultado para salvá-lo em seu catálogo.
* **US04 - Identificação do Jogo:** Como um usuário, quero que o jogo cadastrado seja associado ao seu identificador único na API externa e no `JSON Server`, garantindo que suas informações técnicas e capas adaptativas (`WebP`/`<picture>`) possam ser recuperadas.
* **US05 - Listagem da Coleção:** Como um usuário, quero visualizar todos os jogos cadastrados na minha biblioteca em formato de grid responsivo, para acompanhar o volume total da minha coleção.
* **US06 - Pesquisa e Filtros no Backlog:** Como um usuário, quero pesquisar por nome e filtrar meus jogos por plataforma (PC, PS5, Xbox, Switch) ou status (Jogando, Concluído, Backlog), para encontrar rapidamente uma obra específica.
* **US07 - Visualização dos Detalhes do Jogo:** Como um usuário, quero abrir um modal/card de detalhes de um jogo cadastrado para visualizar suas horas jogadas, nota atribuída, review pessoal e data de conclusão.

---

### ⏱️ Épico 3: Progresso e Avaliações

* **US08 - Registro de Progresso e Horas:** Como um usuário, quero registrar e atualizar a quantidade de horas jogadas em cada título, para monitorar o tempo investido em cada jogo.
  * **Critérios de Aceitação:** O campo de horas deve aceitar apenas valores numéricos positivos e aplicar máscaras de validação do lado do cliente.
* **US09 - Avaliação e Review:** Como um usuário, quero atribuir uma nota (de 1 a 5 estrelas) e escrever uma análise pessoal sobre o jogo ao concluí-lo.
  * **Critérios de Aceitação:** A análise deve respeitar limites de caracteres pré-definidos via validação nativa de formulário e REGEX.
* **US10 - Atualização de Status:** Como um usuário, quero alterar o estado de um jogo (ex.: mudar de *Jogando* para *Concluído*), registrando a data em que o título foi zerado.
  * **Critérios de Aceitação:** Após mudar para **Concluído**, o sistema deve disponibilizar o campo opcional para inserção da data de finalização (`YYYY-MM-DD`).
* **US11 - Remoção de Jogo:** Como um usuário, quero remover um jogo da minha coleção caso o tenha adicionado por engano ou desistido de jogá-lo.
  * **Critérios de Aceitação:** O sistema deve solicitar confirmação antes de disparar a requisição `DELETE` para a API Fake.

---

### 🔄 Épico 4: Status do Backlog e Estatísticas

* **US12 - Status: Na Fila (Backlog):** Como um usuário, quero identificar os jogos que já possuo mas ainda não iniciei, para priorizar minhas próximas jogatinas.
* **US13 - Status: Jogando:** Como um usuário, quero destacar os jogos que estou jogando atualmente, para acesso rápido e atualização frequente de horas no dashboard.
* **US14 - Status: Concluído (Zerado):** Como um usuário, quero visualizar meu histórico de jogos zerados, mantendo o registro de conquistas e avaliações salvas no `JSON Server`.
* **US15 - Status: Lista de Desejos (Wishlist):** Como um usuário, quero marcar jogos que pretendo comprar no futuro, mantendo-os separados dos títulos que já possuo na biblioteca.
