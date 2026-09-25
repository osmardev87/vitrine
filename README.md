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
