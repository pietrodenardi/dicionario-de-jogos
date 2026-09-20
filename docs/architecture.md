```markdown
# 🛠️ Especificação Técnica (Tech Spec) - Backlog Log

Este documento detalha o modelo de dados, os relacionamentos entre as entidades e a estrutura prevista para a API Fake e integrações do sistema **Backlog Log**.

## 1. Modelo de Dados (Diagrama ER)

Abaixo está o Diagrama Entidade-Relacionamento (DER) que representa a estrutura prevista para o `db.json` e como as informações do sistema se relacionam.

```mermaid
erDiagram
    JOGO ||--o{ AVALIACAO : possui
    PLATAFORMA ||--o{ JOGO : suporta

    JOGO {
        int id PK "Gerado automaticamente"
        string rawgId "Identificador da API Externa"
        string titulo
        string capaUrl
        string plataformaId FK "Vínculo com a Plataforma"
        string genero
        int anoLancamento
        int horasJogadas
        string status "Backlog, Jogando, Concluido ou Desejos"
        string dataConclusao "Formato YYYY-MM-DD"
    }

    AVALIACAO {
        int id PK "Gerado automaticamente"
        int jogoId FK "Vínculo com o Jogo"
        int nota "Valores de 1 a 5"
        string reviewTexto
        string dataCriacao "Formato YYYY-MM-DD"
    }

    PLATAFORMA {
        string id PK "Ex: pc, ps5, xbox-series, switch"
        string nome
        string fabricante
    }

```

## 2. Dicionário de Dados

Breve explicação das entidades principais:

* **Jogos:** Responsável por armazenar as informações do catálogo pessoal e progresso dos títulos.
* `id`: Identificador único gerado pelo JSON Server.
* `rawgId`: ID de referência do jogo na API pública RAWG (para sincronização de metadados).
* `titulo`: Nome do jogo de video game.
* `capaUrl`: URL da imagem da capa (otimizada em formato WebP).
* `plataformaId`: Chave estrangeira que conecta o jogo a uma plataforma específica.
* `genero`: Gênero principal do jogo (ex.: Ação, RPG, Estratégia).
* `anoLancamento`: Ano em que o jogo foi lançado.
* `horasJogadas`: Quantidade acumulada de horas dedicadas ao título.
* `status`: Situação atual do jogo na biblioteca. Aceita os valores **Backlog**, **Jogando**, **Concluido** ou **Desejos**.
* `dataConclusao`: Data em que o jogo foi zerado (obrigatório apenas se o status for *Concluido*).


* **Avaliações:** Armazena as notas e análises pessoais escritas pelo jogador.
* `id`: Identificador único gerado pelo JSON Server.
* `jogoId`: Chave estrangeira que vincula a avaliação a um jogo da biblioteca.
* `nota`: Nota atribuída pelo usuário variando de **1** a **5**.
* `reviewTexto`: Análise textual crítica do jogo enviada pelo formulário.
* `dataCriacao`: Data de registro da avaliação no sistema.


* **Plataformas:** Armazena as opções de consoles e ecossistemas disponíveis no sistema.
* `id`: Identificador único da plataforma.
* `nome`: Nome de exibição da plataforma (ex.: PlayStation 5, PC).
* `fabricante`: Empresa responsável pela plataforma (ex.: Sony, Microsoft, Nintendo).



Cada jogo cadastrado no sistema deverá possuir uma **Plataforma** associada e poderá conter uma **Avaliação** vinculada caso tenha sido finalizado.

## 3. Rotas da API (JSON Server)

A aplicação utilizará uma API local simulada pelo JSON Server para persistir e consultar os dados.

Principais endpoints previstos:

* `GET /jogos` - Retorna a lista completa de jogos do backlog.
* `POST /jogos` - Cadastra um novo jogo na biblioteca.
* `GET /jogos/:id` - Retorna os detalhes de um jogo específico.
* `PATCH /jogos/:id` - Atualiza dados pontuais do jogo (ex.: status ou horas jogadas).
* `DELETE /jogos/:id` - Remove um jogo da coleção.
* `GET /avaliacoes?jogoId=1` - Retorna a avaliação e review associada a um jogo.
* `POST /avaliacoes` - Cadastra uma nova avaliação/review para um jogo zerado.
* `GET /plataformas` - Retorna a lista de plataformas cadastradas para popular campos `<select>`.

## 4. Estrutura do Banco de Dados (db.json)

Esta é uma representação inicial da estrutura do banco de dados simulado que será utilizada pelo JSON Server.

```json
{
  "jogos": [
    {
      "id": "1",
      "rawgId": "3498",
      "titulo": "Grand Theft Auto V",
      "capaUrl": "[https://media.rawg.io/media/games/20a/20aa7858b9221d1163b7f42d77265c1b.jpg](https://media.rawg.io/media/games/20a/20aa7858b9221d1163b7f42d77265c1b.jpg)",
      "plataformaId": "ps5",
      "genero": "Ação / Mundo Aberto",
      "anoLancamento": 2013,
      "horasJogadas": 85,
      "status": "Concluido",
      "dataConclusao": "2026-08-20"
    },
    {
      "id": "2",
      "rawgId": "58175",
      "titulo": "God of War Ragnarök",
      "capaUrl": "[https://media.rawg.io/media/games/362/36203f39a039d919d3f1188185c6f376.jpg](https://media.rawg.io/media/games/362/36203f39a039d919d3f1188185c6f376.jpg)",
      "plataformaId": "ps5",
      "genero": "Ação / Aventura",
      "anoLancamento": 2022,
      "horasJogadas": 12,
      "status": "Jogando",
      "dataConclusao": ""
    }
  ],
  "avaliacoes": [
    {
      "id": "1",
      "jogoId": "1",
      "nota": 5,
      "reviewTexto": "Uma obra-prima do mundo aberto. A história intercala muito bem entre os 3 protagonistas.",
      "dataCriacao": "2026-08-20"
    }
  ],
  "plataformas": [
    {
      "id": "pc",
      "nome": "PC",
      "fabricante": "Microsoft / Valve"
    },
    {
      "id": "ps5",
      "nome": "PlayStation 5",
      "fabricante": "Sony"
    },
    {
      "id": "xbox-series",
      "nome": "Xbox Series X/S",
      "fabricante": "Microsoft"
    },
    {
      "id": "switch",
      "nome": "Nintendo Switch",
      "fabricante": "Nintendo"
    }
  ]
}

```

## 5. Tecnologias e Integrações

### Framework CSS

- **Tecnologia:** Bootstrap
- **Versão Exata:** 5.3.3
- **Licença:** MIT
- **Uso no Projeto:** Grid responsivo, Navbar, Cards de jogos, Buttons, Forms, Input Groups, Badges de status, Modais de cadastro e classes utilitárias.
- **Customização:** A estilização padrão do Bootstrap é sobrescrita através de módulos SCSS (`_variables.scss` e `_components.scss`) para implementar a paleta de cores *Dark Mode* e a identidade visual gamer definida nos protótipos do projeto.

### API Pública Externa

- **Serviço:** RAWG Video Games Database API
- **Versionamento:** v1
- **Formato utilizado:** JSON
- **Endpoint Principal:** `https://api.rawg.io/api/games?key={api_key}&search={nome_do_jogo}`
- **Método HTTP:** GET

Campos Consumidos na Aplicação:

- `id`: Mapeado como `rawgId` para identificação única do título na base externa.
- `name`: Título oficial do jogo.
- `background_image`: URL da capa de alta resolução utilizada na renderização dos cards.
- `released`: Ano de lançamento extraído para o cadastro.
- `genres`: Mapeamento do gênero principal.

#### Tratamento de Exceções e Erros da API:
- **Chave de API inválida/ausente (`401 Unauthorized`):** O sistema deve alternar automaticamente para o modo de preenchimento 100% manual.
- **Busca sem resultados (`results: []`):** Exibição de aviso informando que o jogo não foi encontrado na base externa, liberando os campos do formulário para digitação livre.
- **Erro de Conexão/Rede:** Exibição de notificação discreta (Toast) informando a indisponibilidade momentânea do serviço sem travar o fluxo da aplicação.
