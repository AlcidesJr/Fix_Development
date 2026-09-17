---
name: task-closeout
description: Encerrar uma tarefa do Fix Development após merge, consolidando evidências, merge SHA, estado, board, decisões e pendências até DONE. Use quando a implementação já estiver MERGED ou quando for necessário auditar se uma tarefa pode ser marcada como concluída.
---

# Task Closeout

1. Confirmar que o PR/integração foi realmente mesclado.
2. Registrar merge SHA e referências finais em `EVIDENCE.md`.
3. Confirmar que findings efetivos estão resolvidos.
4. Confirmar gates finais e qualquer `DEFERRED_GATE` permitido/documentado.
5. Atualizar decisões permanentes e backlog de pendências que surgiram sem pertencer ao escopo.
6. Atualizar `STATUS.md` para `CLOSEOUT`.
7. Atualizar `work/BOARD.md`.
8. Verificar consistência entre TASK, STATUS, EVIDENCE, REVIEW, PR e merge SHA.
9. Somente então definir `STATE: DONE`.

Resumo final em português do Brasil:

```text
TAREFA: <id>
ESTADO: DONE
PR: <...>
MERGE_SHA: <...>
CI: <...>
BLOCKED_BY: none
DEFERRED_GATE: <...|none>
PENDÊNCIAS: <referências|none>
```
