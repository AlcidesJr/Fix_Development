---
name: task-plan
description: Planejar uma tarefa não trivial do Fix Development antes da implementação, definindo superfícies afetadas, contratos, testes, riscos, rollback e paralelismo. Use quando a tarefa estiver em PLANNING, quando o plano precisar ser revisado ou quando uma mudança de escopo exigir replanejamento.
---

# Task Plan

1. Confirmar `TASK.md` e estado `PLANNING`.
2. Ler somente contratos/arquitetura relacionados ao escopo.
3. Investigar a implementação atual até entender a superfície que realmente precisa mudar.
4. Preencher/atualizar `PLAN.md` usando `templates/PLAN.md`.
5. Definir critérios de verificação antes de codificar.
6. Identificar riscos, compatibilidade, migrations/dados e rollback quando aplicáveis.
7. Decidir se existe paralelismo real; se sim, definir contrato e ownership antes de criar subagentes.
8. Não implementar a solução durante esta Skill.
9. Mover para `READY` apenas quando o plano for executável e as dependências estiverem satisfeitas.

Para tarefas pequenas, manter o plano curto. Para alto risco, ampliar deliberadamente o contexto conforme `docs/ECONOMIA-DE-TOKENS.md`.
