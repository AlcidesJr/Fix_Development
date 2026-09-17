---
name: task-implement
description: Implementar uma tarefa do Fix Development que já esteja READY e possua plano suficiente, mantendo escopo atômico, contratos, testes e documentação. Use para executar a alteração planejada, corrigir findings efetivos ou retomar implementação após nova verificação.
---

# Task Implement

1. Confirmar `STATE: READY` ou retorno autorizado a `IMPLEMENTING`.
2. Ler `TASK.md`, `PLAN.md` e somente arquivos/contratos necessários.
3. Atualizar estado para `IMPLEMENTING`.
4. Implementar apenas o escopo aprovado.
5. Preservar contratos e compatibilidade declarados no plano.
6. Criar/ajustar testes junto da mudança quando adequado.
7. Registrar decisões permanentes na documentação correta, não apenas em conversa.
8. Se surgir trabalho adjacente, formalizá-lo; não absorvê-lo silenciosamente.
9. Fazer autorrevisão do diff.
10. Atualizar `EVIDENCE.md` com commits/alterações relevantes.
11. Mover para `VERIFYING` quando a implementação estiver pronta para testes.

Se uma dependência real aparecer, registrar `BLOCKED_BY` e usar `BLOCKED`.
