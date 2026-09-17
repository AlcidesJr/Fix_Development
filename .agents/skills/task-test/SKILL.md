---
name: task-test
description: Verificar uma implementação do Fix Development com testes focados, integração, regressões e gates de CI proporcionais ao risco, registrando evidências e classificando falhas herdadas. Use quando a tarefa estiver em VERIFYING ou após correções que exijam nova validação.
---

# Task Test

1. Confirmar HEAD e estado `VERIFYING`.
2. Ler estratégia de testes do `PLAN.md`.
3. Executar na ordem: focado → módulo → integração → regressão dirigida → build/lint/typecheck → global/CI exigido.
4. Registrar comando/run e resultado em `EVIDENCE.md`.
5. Em falha, diagnosticar primeiro job/step/erro relevante; não carregar logs inteiros sem necessidade.
6. Se a falha for causada pela tarefa, retornar a `IMPLEMENTING`.
7. Se comprovadamente herdada/externa, registrar `DEFERRED_GATE` conforme `docs/GOVERNANCA.md`.
8. Se impedir diretamente o aceite, registrar `BLOCKED_BY` e `BLOCKED`.
9. Confirmar que evidências pertencem ao HEAD atual.
10. Avançar para `IN_REVIEW` somente quando os gates exigidos estiverem satisfeitos ou corretamente classificados.

Nunca declarar `PASS` por inferência; exigir evidência verificável.
