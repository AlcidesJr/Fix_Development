---
name: task-intake
description: Iniciar ou retomar uma tarefa do Fix Development recuperando estado fresco, escopo, dependências, PR, CI e evidências antes de qualquer implementação. Use quando uma tarefa nova começar, quando uma tarefa existente for retomada ou quando o estado remoto puder ter mudado.
---

# Task Intake

1. Ler `AGENTS.md`.
2. Identificar TASK ativa e branch base.
3. Ler `work/BOARD.md`, `TASK.md`, `STATUS.md` e referências explicitamente necessárias.
4. Consultar estado atual de branch, PR, CI e review threads quando existirem.
5. Validar dependências.
6. Classificar impedimentos como `BLOCKED_BY` ou gates herdados como `DEFERRED_GATE` conforme `docs/GOVERNANCA.md`.
7. Não editar código durante o intake, exceto documentação operacional necessária para registrar o estado.
8. Atualizar `STATUS.md` para `INTAKE`, depois `PLANNING` ou `BLOCKED` conforme resultado.

Aplicar `docs/ECONOMIA-DE-TOKENS.md`: ler somente contexto suficiente e expandir sob demanda.

Feedback em português do Brasil, curto:

```text
TAREFA: <id>
ESTADO: <estado>
HEAD/PR: <referência>
CI: <estado>
BLOCKED_BY: <...|none>
DEFERRED_GATE: <...|none>
PRÓXIMO PASSO: <...>
```
