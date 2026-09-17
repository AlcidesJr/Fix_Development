# Revisão e qualidade

## Objetivo

Transformar qualidade em gates verificáveis, sem exigir a mesma cerimônia para toda mudança.

## Estratégia de verificação

Executar do mais focado ao mais amplo:

```text
1. teste diretamente relacionado
2. módulo/componente
3. integração relevante
4. regressões dirigidas
5. lint/typecheck/build aplicáveis
6. suíte global e CI exigidos pelo projeto
```

Não use a suíte global como primeiro instrumento de diagnóstico após cada pequena edição.

## Evidência mínima

Uma afirmação de sucesso deve apontar para evidência concreta, por exemplo:

```text
pytest tests/test_example.py -q → 12 passed
npm run build → exit 0
CI run 123456 → PASS
HEAD abc1234
```

Evite copiar logs completos quando a referência do run e o resumo bastarem.

## Autorrevisão do implementador

Antes de enviar para review:

- comparar diff com `TASK.md` e `PLAN.md`;
- procurar alterações acidentais;
- confirmar tratamento de erros;
- conferir compatibilidade declarada;
- verificar se testes cobrem a regressão/feature;
- remover código temporário, debug e TODOs indevidos;
- atualizar documentação afetada.

## Revisão independente

O Reviewer deve partir do contrato e da evidência, não apenas da explicação do implementador.

Perguntas obrigatórias:

1. O diff cumpre os critérios de aceite?
2. Existe comportamento quebrado fora do caminho feliz?
3. Algum contrato público/interno mudou sem documentação?
4. O teste realmente falharia antes da correção quando isso for relevante?
5. Existe expansão de escopo?
6. A implementação duplica mecanismo existente sem necessidade?
7. Existe risco de dados, concorrência, compatibilidade ou operação?
8. A evidência corresponde ao HEAD revisado?

## Severidade de findings

### P0 — crítico

Risco de perda grave de dados, comprometimento de segurança, indisponibilidade ampla ou comportamento destrutivo imediato.

Bloqueia merge.

### P1 — alto

Bug funcional relevante, quebra de contrato, regressão provável ou risco operacional sério.

Bloqueia merge.

### P2 — médio

Problema real de robustez, cobertura, manutenção ou edge case com impacto limitado.

Deve ser corrigido ou explicitamente transformado em tarefa separada conforme política do projeto.

### P3 — baixo

Melhoria pequena e objetiva sem impacto funcional relevante. Não usar P3 para preferências puramente estilísticas já cobertas por formatter/linter.

## Finding de qualidade

Todo finding deve conter:

```text
SEVERIDADE: P0|P1|P2|P3
LOCAL: arquivo/linha ou superfície
IMPACTO: o que pode dar errado
EVIDÊNCIA: por que o problema existe
CORREÇÃO ESPERADA: comportamento necessário, sem prescrever implementação quando não for preciso
```

## Review thread

Uma thread só deve ser resolvida quando:
- a correção foi integrada no HEAD atual; ou
- a observação foi demonstrada como não aplicável com evidência; ou
- foi formalmente convertida em trabalho separado permitido pela política.

Não resolver thread apenas porque houve resposta textual.

## CI e falhas herdadas

Se um gate falhar:

1. identificar job/step e causa;
2. verificar se a falha reproduz ou se relaciona ao diff atual;
3. se causada pela tarefa, corrigir;
4. se comprovadamente herdada/externa, registrar `DEFERRED_GATE`;
5. se impedir diretamente o aceite, registrar `BLOCKED_BY` e `BLOCKED`.

## Correspondência entre HEAD e evidência

Antes de `READY_TO_MERGE`, confirmar:
- qual commit foi revisado;
- qual commit passou no CI;
- se houve commit posterior, quais gates precisam ser repetidos.

Nunca transportar silenciosamente um `PASS` de um HEAD antigo para um novo.
