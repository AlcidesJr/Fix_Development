# Governança

## Objetivo

Este documento define como organizar trabalho assistido por Codex sem perder controle de escopo, rastreabilidade ou capacidade de revisão.

## 1. GitHub como fonte de verdade

Toda decisão operacional relevante deve ser recuperável no repositório, issue, PR ou CI. Conversas ajudam na execução, mas não substituem o estado versionado.

Antes de iniciar ou retomar uma tarefa, reconsultar o estado fresco de:

- branch base;
- branch da tarefa;
- issue/tarefa;
- `work/BOARD.md`;
- `TASK.md`, `STATUS.md` e `EVIDENCE.md`;
- PR e review threads, quando existirem;
- CI associado ao HEAD atual;
- dependências declaradas.

## 2. Tarefa atômica

Uma tarefa deve resolver **um objetivo coerente e verificável**.

Uma tarefa não deve:

- absorver refatorações oportunistas sem relação com o aceite;
- implementar trabalho reservado a outra tarefa;
- alterar contratos vizinhos sem necessidade técnica demonstrada;
- corrigir gates herdados apenas para produzir um CI global verde.

Se durante a execução aparecer trabalho novo, registre-o no backlog/issue apropriado e continue apenas se for requisito direto do escopo atual.

## 3. Contrato mínimo da tarefa

`TASK.md` deve declarar:

- objetivo;
- contexto;
- escopo;
- fora de escopo;
- critérios de aceite;
- dependências;
- riscos conhecidos;
- referências relevantes.

Ambiguidade que altere significativamente comportamento, segurança, dados ou compatibilidade deve ser resolvida no planejamento antes de implementar.

## 4. Classificações operacionais

### `BLOCKED_BY`

Use quando uma dependência ou problema impede diretamente a conclusão correta da tarefa.

Exemplos:

- contrato obrigatório ainda não definido;
- migration anterior necessária não integrada;
- serviço externo obrigatório indisponível sem alternativa verificável.

Formato:

```text
BLOCKED_BY=<issue, task, PR ou descrição objetiva>
```

Ao usar `BLOCKED_BY`, o estado normalmente passa a `BLOCKED`.

### `DEFERRED_GATE`

Use quando um gate falha por causa herdada, externa ou fora do escopo, sem regressão causada pela tarefa atual.

Formato:

```text
DEFERRED_GATE=<run/gate + causa + frente responsável, quando conhecida>
```

Regras:

- documentar evidência suficiente para separar a falha do diff atual;
- não alterar código fora do escopo para resolver o gate;
- não usar `DEFERRED_GATE` para regressão introduzida pela própria tarefa;
- a política do projeto pode exigir aprovação humana antes do merge com gate adiado.

## 5. Branches e PRs

Convenção recomendada:

```text
task/<TASK>-<slug>
```

Regras:

- uma tarefa principal por branch;
- PR aponta para a branch de integração definida pelo projeto;
- commits devem ser compreensíveis e relacionados ao escopo;
- alterações documentais de fechamento podem usar PR separado quando a política do projeto exigir registrar o merge SHA da implementação antes de finalizar evidências.

## 6. Decisões

Decisões arquiteturais ou operacionais que sobreviverão à tarefa devem ser registradas na documentação permanente do projeto, não somente em `PLAN.md`.

Uma decisão deve registrar, no mínimo:

- contexto;
- decisão;
- alternativas relevantes consideradas;
- consequências;
- data/referência da tarefa que a introduziu.

## 7. Regras para mudança de escopo

Quando o escopo precisar mudar durante a implementação:

1. parar a expansão silenciosa;
2. registrar o motivo;
3. atualizar `TASK.md`/issue ou abrir nova tarefa;
4. reavaliar plano, testes, risco e dependências;
5. continuar somente dentro do contrato atualizado.

## 8. Definição de pronto

`DONE` significa estado comprovado, não intenção.

A tarefa deve ter, conforme aplicável:

- critérios de aceite atendidos;
- testes relevantes executados;
- regressões do próprio diff ausentes;
- findings efetivos resolvidos;
- segurança avaliada proporcionalmente ao risco;
- PR integrado;
- merge SHA registrado;
- documentação e evidências atualizadas;
- `BOARD.md` consistente com o estado final.

## 9. Feedback ao usuário

Por padrão, comunicar em português do Brasil e evitar relatórios excessivos.

Um bom feedback operacional contém:

```text
TAREFA: <id>
ESTADO: <estado>
HEAD/PR: <referência relevante>
CI: <PASS/FAIL/pending + referência>
BLOCKED_BY: <...|none>
DEFERRED_GATE: <...|none>
PRÓXIMO PASSO: <ação objetiva>
```

Detalhes extensos ficam em `EVIDENCE.md`, `REVIEW.md` ou na thread correspondente.
