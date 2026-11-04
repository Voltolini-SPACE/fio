# Fio

Gateway de WhatsApp auto-hospedado: uma API HTTP para sessões, mensagens, contatos e
webhooks, com servidor **MCP** embutido para agentes. Roda em um processo Node.

- **164 rotas** documentadas em `openapi.json` (Swagger em `/api/docs`).
- **MCP** em `/mcp` (Streamable HTTP), autenticado por chave.
- **Licença MIT** — ver `LICENSE`; origem do núcleo em `NOTICE` e `CREDITS.md`.

## Começar

```bash
npm ci --ignore-scripts
npm run build
node dist/main          # sobe em http://localhost:2785
```

A primeira subida cria a chave de API em `data/.api-key` (0600). Use-a em
`x-api-key` ou `Authorization: Bearer`. O painel web não faz parte desta edição.

## Para agentes

`MCP_ENABLED=true node dist/main` expõe `/mcp`; veja `MANUAL.md` §MCP.

Nome do pacote: `voltolini-fio`. Cor primária da marca: `#0F5132`.
