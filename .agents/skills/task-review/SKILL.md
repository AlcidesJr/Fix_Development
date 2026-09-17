---
name: task-review
description: Revisar de forma crítica e independente uma implementação do Fix Development usando TASK, PLAN, diff e evidências, classificando findings P0-P3. Use quando a tarefa estiver em IN_REVIEW, após correções de review ou quando um PR precisar de auditoria técnica focada.
---

# Task Review

1. Confirmar o HEAD exato sob revisão.
2. Ler `TASK.md`, `PLAN.md`, diff e evidências de testes.
3. Começar pelo diff; abrir arquivos completos somente quando necessário.
4. Verificar critérios de aceite, contratos, edge cases, regressões, escopo, testes e documentação.
5. Não criar finding por mera preferência estética já coberta por formatter/linter.
6. Registrar findings em `REVIEW.md` usando P0/P1/P2/P3 conforme `docs/REVISAO-E-QUALIDADE.md`.
7. Cada finding deve indicar local, impacto, evidência e correção esperada.
8. Finding efetivo retorna a tarefa para correção e nova verificação.
9. Quando não houver finding efetivo, registrar `REVIEW: PASS` e avançar para `SECURITY_REVIEW`.
10. Não transportar aprovação para um HEAD posterior sem verificar o novo diff.

Feedback ao usuário deve resumir somente findings efetivos, estado e próximo passo.
