# Fluxo de trabalho

## Visão geral

O Fix Development transforma uma solicitação em uma sequência verificável de estados. O Orquestrador controla a progressão; papéis especializados entram somente quando agregam valor.

```text
INTAKE
  ↓
PLANNING
  ↓
IMPLEMENTATION
  ↓
VERIFY
  ↓
REVIEW
  ↓
SECURITY
  ↓
MERGE
  ↓
CLOSEOUT
```

## 1. PLANNED → INTAKE

Objetivo: descobrir o estado real antes de tomar decisões.

Ações:
- atualizar branch base e branch da tarefa;
- ler `AGENTS.md`;
- ler `BOARD.md`, `TASK.md` e `STATUS.md`;
- verificar dependências;
- verificar PR, CI e review threads existentes;
- localizar contratos/documentação relevantes.

Saída:
- contexto mínimo suficiente;
- `BLOCKED_BY` ou `DEFERRED_GATE` classificados, se houver;
- transição para `PLANNING` ou `BLOCKED`.

## 2. PLANNING → READY

Objetivo: escolher como implementar antes de editar.

`PLAN.md` deve responder:
- qual comportamento muda;
- quais superfícies serão alteradas;
- quais contratos precisam permanecer compatíveis;
- quais testes demonstram correção;
- quais riscos existem;
- como reverter quando rollback for relevante;
- quais partes podem ser paralelizadas.

Mudanças triviais podem usar um plano curto. Mudanças de alto risco exigem maior detalhamento.

Saída:
- plano executável e coerente com `TASK.md`;
- contratos definidos antes de paralelismo;
- estado `READY`.

## 3. READY → IMPLEMENTING

Objetivo: executar o plano sem expansão silenciosa de escopo.

Regras:
- editar somente superfícies justificadas;
- preservar compatibilidade declarada;
- escrever/ajustar testes junto da mudança quando apropriado;
- registrar decisões duráveis na documentação permanente;
- se aparecer trabalho adjacente, formalizá-lo em outra tarefa.

Subagentes podem ser usados conforme `MULTIAGENTE.md`.

## 4. IMPLEMENTING → VERIFYING

Objetivo: provar que a implementação cumpre o contrato.

Ordem preferida:
1. testes focados;
2. testes do módulo;
3. integração relevante;
4. regressões dirigidas;
5. build/lint/typecheck aplicáveis;
6. suíte global/CI exigida pelo projeto.

Falha causada pela mudança retorna a `IMPLEMENTING`.

Falha comprovadamente herdada pode ser registrada como `DEFERRED_GATE` conforme governança.

## 5. VERIFYING → IN_REVIEW

Objetivo: procurar problemas que o implementador não percebeu.

O Reviewer recebe preferencialmente:
- `TASK.md`;
- `PLAN.md`;
- diff;
- resultados de testes;
- `EVIDENCE.md` parcial.

Deve procurar:
- regressão;
- quebra de contrato;
- edge cases;
- expansão indevida de escopo;
- ausência de teste relevante;
- duplicação ou complexidade desnecessária;
- inconsistência entre código e documentação.

Findings efetivos devolvem o fluxo para correção e nova verificação.

## 6. IN_REVIEW → SECURITY_REVIEW

Objetivo: avaliar risco proporcional à superfície alterada.

Para mudança sem impacto de segurança, registrar `N/A` com justificativa curta.

Para mudança relevante, usar `docs/SEGURANCA.md`.

Finding crítico/alto não resolvido impede avanço.

## 7. SECURITY_REVIEW → READY_TO_MERGE

Pré-condições:
- critérios de aceite atendidos;
- testes/gates aplicáveis concluídos;
- findings efetivos resolvidos;
- estado do PR atualizado;
- branch base reconsultada se necessário.

Antes do merge, verificar novamente se o HEAD revisado é o mesmo HEAD que passou pelos gates.

## 8. READY_TO_MERGE → MERGED

Executar a política de merge do projeto.

Registrar:
- PR;
- HEAD final;
- merge SHA;
- resultado dos gates de integração.

## 9. MERGED → CLOSEOUT → DONE

Objetivo: deixar a tarefa auditável para quem chegar depois.

Atualizar:
- `EVIDENCE.md`;
- `STATUS.md`;
- `BOARD.md`;
- decisões permanentes;
- backlog para pendências formalizadas.

Somente depois marcar `DONE`.

## Loop de correção

Findings não encerram a tarefa. O fluxo retorna ao ponto adequado:

```text
REVIEW finding
  ↓
IMPLEMENTING
  ↓
VERIFYING
  ↓
IN_REVIEW
```

O mesmo vale para security findings.

## Quando pedir decisão humana

Escalar quando houver escolha material não coberta por contrato, especialmente:
- mudança de produto com alternativas válidas;
- quebra deliberada de compatibilidade;
- operação destrutiva sem rollback claro;
- risco de segurança aceito em vez de corrigido;
- conflito entre requisitos de mesma prioridade.

Não escalar perguntas que podem ser respondidas pela fonte de verdade ou por investigação técnica segura.
