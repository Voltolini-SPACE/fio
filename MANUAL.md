# Manual do Fio

## 1. O que é

Fio expõe por HTTP as operações de um gateway de WhatsApp e as publica também por MCP.
O processo é único: API, MCP e tarefas internas na mesma instância Node.

## 2. Requisitos

- Node >= 22.19
- 1 GB de RAM livre
- porta livre (padrão 2785)

## 3. Instalação

```bash
npm ci --ignore-scripts
npm run build
```

## 4. Configuração

| Variável | Para quê | Padrão |
| --- | --- | --- |
| `PORT` | porta HTTP | `2785` |
| `MCP_ENABLED` | liga `/mcp` | `false` |
| `SERVE_DASHBOARD` | serve painel se houver build | `false` |
| `API_MASTER_KEY` | chave ADMIN semeada no primeiro boot | gerada em `data/.api-key` |
| `ALLOW_DEV_API_KEY` | usa `dev-admin-key` fixa — **só em teste local** | `false` |

## 5. Subir e operar

```bash
node dist/main
curl -s localhost:2785/api/health
```

`/api/health` responde 200 sem chave. As demais rotas exigem a chave do arquivo `data/.api-key`.

## 6. Autenticação

Envie `x-api-key: <chave>` (ou `Authorization: Bearer <chave>`).
A chave completa só aparece no log da primeira subida; depois disso, apenas em `data/.api-key`.

## 7. MCP

```bash
MCP_ENABLED=true node dist/main
curl -X POST localhost:2785/mcp -H "content-type: application/json" \
  -H "accept: application/json, text/event-stream" -H "x-api-key: $CHAVE" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-06-18","capabilities":{},"clientInfo":{"name":"cliente","version":"0"}}}'
```

## 8. Superfície HTTP

164 rotas em `openapi.json`, agrupadas por módulo:

- `sessions`: 117
- `plugins`: 13
- `infra`: 12
- `auth`: 4
- `integration`: 4
- `health`: 3
- `stats`: 3
- `webhooks`: 3
- `audit`: 1
- `ingress`: 1
- `metrics`: 1
- `search`: 1
- `settings`: 1

## 9. Docker

```bash
docker compose up -d --build
```

## 10. Limites desta edição

- Painel web (`dashboard/`) e SDK não fazem parte do pacote.
- Sessão real de WhatsApp exige QR e não é validada pelo teste automático;
  o que o teste prova é o processo subir, `/api/health` responder e o MCP aceitar handshake.
- Paridade item a item em `PARIDADE.md`.
