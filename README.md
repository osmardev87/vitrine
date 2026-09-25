# Servidor Valheim

A vitrine original está preservada em [`loja-online.html`](./loja-online.html). A página inicial do projeto, [`index.html`](./index.html), é a landing page do servidor Valheim.

## Iniciar o servidor dedicado

### Pré-requisitos

- Docker Engine com Docker Compose v2;
- portas UDP **2456–2458** liberadas no firewall e encaminhadas no roteador, quando o servidor for público;
- pelo menos alguns GB livres em disco: a primeira inicialização baixa o servidor dedicado do Valheim.

### Configuração

1. Crie o arquivo local de configurações e escolha uma senha com pelo menos cinco caracteres:

   ```bash
   cp valheim.env.example valheim.env
   ```

2. Edite `valheim.env`. Não envie esse arquivo ao Git: ele contém a senha do servidor.
3. Inicie o servidor:

   ```bash
   docker compose up -d
   ```

4. Acompanhe a preparação inicial e o status:

   ```bash
   docker compose logs -f valheim
   ```

O mundo, configurações e backups persistem em `valheim-data/`. Para atualizar a imagem posteriormente, execute:

```bash
docker compose pull && docker compose up -d
```

## Parar o servidor

```bash
docker compose down
```

Isso não remove o mundo nem os backups, pois eles ficam no volume local `valheim-data/`.

## Status em tempo real no site

O serviço `site` publica a landing page em `http://IP_DO_SERVIDOR:8080` e encaminha `status.json` internamente para o servidor Valheim. Assim, a página mostra a quantidade de jogadores conectados e atualiza a consulta a cada 10 segundos, sem expor a porta de status diretamente na internet.

O Valheim não disponibiliza a quantidade de mortes de cada jogador na consulta pública do servidor. Para exibir mortes reais no site, é necessário instalar um mod no servidor que registre eventos de morte e publique uma API própria; não use o campo `score` da consulta Steam como se fosse morte, pois ele não representa essa estatística no Valheim.
