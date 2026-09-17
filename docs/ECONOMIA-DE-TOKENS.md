# Economia de tokens e gestão de contexto

## Objetivo

Reduzir custo, latência e perda de foco sem sacrificar correção.

> Carregue o menor contexto suficiente para tomar a próxima decisão correta.

Se houver dúvida material sobre dados, compatibilidade, migração, segurança ou causa de uma falha, amplie o contexto.

## Escada de contexto

Não comece pelo repositório inteiro. Expanda nesta ordem:

1. **Contrato:** `AGENTS.md`, `TASK.md`, `STATUS.md` e dependências.
2. **Índices e contratos técnicos:** arquitetura, interfaces, schemas e decisões aplicáveis.
3. **Superfície afetada:** busca, símbolos, arquivos-alvo, testes e diffs.
4. **Diagnóstico:** logs focados, callers/callees e histórico relacionado.
5. **Visão ampla:** somente para mudança transversal, risco sistêmico ou causa ainda não isolada.

## AGENTS.md

Use `AGENTS.md` como mapa, não como enciclopédia:

- mantenha somente regras persistentes;
- aponte para documentos detalhados;
- não duplique conteúdo de `docs/`;
- remova regras obsoletas;
- prefira um arquivo curto, aproximadamente 80–150 linhas quando possível.

## Skills

Aplique divulgação progressiva:

- metadata curta identifica quando a Skill é aplicável;
- `SKILL.md` contém somente fluxo essencial e gates;
- detalhes extensos ficam em `references/`;
- rotinas repetitivas e determinísticas podem virar `scripts/`;
- não duplique a mesma explicação em vários arquivos.

## Prompts

Prefira pedidos no formato de issue:

```text
TASK: ABC-001
Objetivo: ...
Escopo: ...
Fora de escopo: ...
Critérios de aceite: ...
Referências: ...
```

Evite colar arquivos, logs ou regras que o Codex pode consultar no repositório.

## Leitura e reconsulta

Reconsulte estado **mutável** quando ele puder ter mudado: HEAD, CI, PR, review threads e branch base.

Não releia automaticamente conteúdo imutável e já validado.

Em revisão:

1. liste arquivos alterados;
2. leia o diff/patch;
3. abra arquivo completo apenas quando o contexto estrutural for necessário;
4. expanda para dependências somente com motivo técnico.

## Testes

Execute do menor para o maior:

```text
focado → módulo → integração → regressão dirigida → suíte global/CI
```

A suíte global continua obrigatória quando a política do projeto exigir; apenas não deve ser o primeiro instrumento de diagnóstico para toda pequena edição.

## Logs

Ao investigar CI:

- identifique primeiro o job e step que falharam;
- leia erro e contexto próximo;
- amplie o log somente se a causa continuar ambígua;
- em `EVIDENCE.md`, registre resultado e referência do run em vez de copiar o log inteiro.

## Subagentes

Forneça apenas:

```text
objetivo
limites
contrato relevante
superfície sob responsabilidade
saída esperada
critério de conclusão
```

Não replique toda a conversa do orquestrador.

Paralelize apenas quando o contrato estiver estável e os subescopos forem realmente independentes. Mais agentes também podem significar mais tokens.

## Compactação

Em ambientes com compactação de contexto, prefira usá-la após marcos relevantes de sessões longas, por exemplo:

- intake concluído;
- plano aprovado;
- implementação concluída antes da revisão;
- review resolvido antes do fechamento.

Antes disso, grave decisões duráveis no repositório. A conversa nunca deve ser a única fonte de verdade.

## Feedback ao usuário

Por padrão, reporte somente:

```text
estado
mudança relevante
resultado dos gates
bloqueios
próximo passo
```

Detalhes completos ficam em `EVIDENCE.md`, `REVIEW.md`, PR e CI.

## Risco supera economia

Quanto maior o risco, maior pode ser o contexto necessário. Autenticação, autorização, migrations, dados persistentes, concorrência, segurança e operações destrutivas justificam inspeção mais ampla.

Nunca economize tokens a ponto de adivinhar.

## Anti-padrões

- `AGENTS.md` gigante;
- ler todo o repositório sem hipótese;
- reler arquivos inalterados em loop;
- mandar histórico completo para todo subagente;
- rodar a suíte global após cada edição pequena;
- copiar logs enormes para evidências;
- paralelizar agentes sem contrato estável;
- repetir ao usuário informações que não mudaram.

## Checklist

Antes de buscar mais contexto, pergunte:

1. Qual decisão preciso tomar agora?
2. Qual é a menor fonte de verdade que responde isso?
3. Essa informação já foi lida e continua válida?
4. Posso usar busca, diff ou trecho em vez do arquivo inteiro?
5. Existe risco suficiente para justificar ampliar o contexto?
