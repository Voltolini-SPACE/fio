# Paridade de Fio

Este documento declara o que a edição entrega e o que fica fora. Não é promessa de 100%.

## Entregue

| Item | Evidência |
| --- | --- |
| Núcleo de gateway (sessões, mensagens, contatos, webhooks) | `src/`, 164 rotas em `openapi.json` |
| Servidor MCP sobre HTTP | `/mcp`, `initialize`/`tools/list`/`tools/call` comprovados por cliente externo |
| Autenticação por chave | `data/.api-key`, `x-api-key`/`Bearer` |
| Build e subida | `npm ci` + `npm run build` + `node dist/main` |
| Licença e créditos | `LICENSE`, `NOTICE`, `CREDITS.md` |

## Fora desta edição

| Item | Por quê |
| --- | --- |
| Painel web (`dashboard/`) | não copiado para o pacote; UI própria é trabalho separado |
| SDK (`sdk/`) | não copiado |
| Documentação do projeto de origem | substituída por `README.md`/`MANUAL.md` |
| Sessão real de WhatsApp | exige QR e número; não roda em teste automático |

## Superfície por módulo

| Módulo | Rotas |
| --- | --- |
| `sessions` | 117 |
| `plugins` | 13 |
| `infra` | 12 |
| `auth` | 4 |
| `integration` | 4 |
| `health` | 3 |
| `stats` | 3 |
| `webhooks` | 3 |
| `audit` | 1 |
| `ingress` | 1 |
| `metrics` | 1 |
| `search` | 1 |
| `settings` | 1 |
