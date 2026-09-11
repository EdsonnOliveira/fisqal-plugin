---
name: fisqal
description: Use FISQAL MCP to consult, draft, validate and emit NFS-e safely.
---

# FISQAL

Use the `fisqal` MCP server for Brazilian fiscal workflows.

## Autenticação

O plugin usa OAuth 2.1 via `.mcp.json` (sem API Key fixa). Na primeira conexão, o Codex/ChatGPT abre login em `fisqal.com.br`, pede consentimento e retorna tokens via PKCE. Registre o client em `POST /oauth/register` se necessário e inclua o `redirect_uri` na allowlist do servidor.

## Emissão de NFS-e

1. Identify the company with `list_companies` and confirm the intended company.
2. Search for a similar note with `find_similar_nfse` or `search_nfse`.
3. Create a draft with `create_nfse_draft` or `create_nfse_draft_from_previous`.
4. Run `validate_nfse_draft` and explain every blocking error.
5. Before `emit_nfse`, show the final recipient, service, amount, taxes and description and request explicit human confirmation.
6. After emission, use `get_nfse_status`, `get_nfse_pdf` or `get_nfse_xml` as requested.

Never emit or cancel a document without explicit confirmation in the current conversation.
