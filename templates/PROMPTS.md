# Prompts de operação

Os prompts abaixo são deliberadamente curtos. Regras permanentes devem permanecer no repositório, não ser copiadas em toda conversa.

## Iniciar uma tarefa

```text
Inicie exclusivamente a <TASK>.

GitHub e os arquivos versionados são a fonte de verdade.
Siga AGENTS.md integralmente.
Reconsulte o estado fresco antes de agir.

Leia primeiro:
- AGENTS.md
- work/BOARD.md
- work/<TASK>/TASK.md
- work/<TASK>/STATUS.md

Conduza a tarefa pelos estados do Fix Development.
Não implemente tarefas adjacentes.
Mantenha o feedback em português do Brasil.
```

## Retomar uma tarefa

```text
Retome exclusivamente a <TASK>.

Não presuma o estado anterior: reconsulte branch, HEAD, PR, CI, review threads e arquivos da tarefa.
Siga AGENTS.md integralmente.
Continue do estado real encontrado.

Feedback em português do Brasil, objetivo.
```

## Revisar um PR

```text
Revise o PR #<N> exclusivamente contra a <TASK>.

Reconsulte HEAD, base, CI e todas as review threads.
Leia TASK.md, PLAN.md, EVIDENCE.md e o diff.
Procure regressões, quebra de contrato, edge cases, expansão de escopo e ausência de testes.
Classifique findings conforme docs/REVISAO-E-QUALIDADE.md.
Não gere findings por preferência estética.
```

## Verificar estado e próximo passo

```text
Verifique o estado fresco da <TASK>.

Responda somente com:
- TASK;
- STATE;
- HEAD/PR;
- CI;
- BLOCKED_BY;
- DEFERRED_GATE;
- próximo passo;
- prompt curto para executar esse próximo passo, se uma nova execução for necessária.
```

## Fechar uma tarefa

```text
Faça o closeout da <TASK>.

Confirme merge, merge SHA, CI, findings, EVIDENCE.md, STATUS.md e BOARD.md.
Só marque DONE se todos os requisitos de docs/ESTADOS.md e AGENTS.md estiverem satisfeitos.
```

## Criar a próxima tarefa

```text
Audite primeiro o estado do repositório e backlog.
Não invente uma nova tarefa se já existir uma pendência formalizada equivalente.

Quando houver próximo trabalho claro, crie a tarefa atômica com TASK.md, STATUS.md e linha no BOARD, registrando dependências e critérios de aceite.
Não implemente a nova tarefa nesta etapa.
```
