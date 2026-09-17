# EVIDENCE — <ID>

## Intake

- Base HEAD: <sha>
- Task HEAD inicial: <sha|N/A>
- Dependências: <PASS/BLOCKED + referência>
- BLOCKED_BY: none
- DEFERRED_GATE: none

## Planejamento

- PLAN: <commit/path>
- Decisões relevantes: <referência|none>

## Implementação

- Commits: <sha(s)>
- Resumo: <curto>

## Verificação

| Gate | Comando/Run | Resultado |
| --- | --- | --- |
| Focado | `<comando>` | PASS/FAIL |
| Integração | `<comando ou N/A>` | PASS/FAIL/N/A |
| Global/CI | `<run ou N/A>` | PASS/FAIL/DEFERRED/N/A |

## Review

- Resultado: <PASS/FINDINGS>
- Findings abertos: <0 ou referências>
- REVIEW.md: <path>

## Segurança

- Resultado: <PASS/FINDINGS/N/A>
- Evidência/justificativa: <...>

## Integração

- PR: <número|N/A>
- HEAD aprovado: <sha>
- Merge SHA: <sha|pending>

## Fechamento

- STATUS.md: <atualizado/pending>
- BOARD.md: <atualizado/pending>
- Pendências formalizadas: <referências|none>
