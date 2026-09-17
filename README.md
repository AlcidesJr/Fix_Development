# Fix Development

**Um padrão prático, aberto e em português para desenvolver software com Codex de forma previsível, auditável e econômica em tokens.**

O Fix Development organiza o trabalho em **tarefas atômicas**, estados explícitos, planejamento antes da implementação, validação por evidências, revisão independente e fechamento rastreável no GitHub. O modelo é genérico: pode ser aplicado a APIs, aplicações web, automações, bibliotecas, integrações, infraestrutura e outros tipos de projeto.

> O humano define intenção e prioridade. O Codex executa dentro de contratos, estados e gates verificáveis.

## Em 30 segundos

Cada mudança segue este ciclo:

```mermaid
flowchart LR
    A[PLANNED] --> B[INTAKE]
    B --> C[PLANNING]
    C --> D[READY]
    D --> E[IMPLEMENTING]
    E --> F[VERIFYING]
    F --> G[IN_REVIEW]
    G --> H[SECURITY_REVIEW]
    H --> I[READY_TO_MERGE]
    I --> J[MERGED]
    J --> K[CLOSEOUT]
    K --> L[DONE]
```

Estados excepcionais: `BLOCKED` e `CANCELLED`.

Cada tarefa mantém, no mínimo:

```text
work/<TASK>/
├── TASK.md
├── PLAN.md
├── STATUS.md
├── EVIDENCE.md
└── REVIEW.md
```

## Regras centrais

1. **GitHub é a fonte de verdade.** Sempre consultar o estado atual antes de agir.
2. **Uma tarefa, um escopo.** Não corrigir assuntos adjacentes apenas para deixar o CI global verde.
3. **Planejar antes de codificar.** Mudanças não triviais passam por `PLAN.md` antes da implementação.
4. **Evidência antes de afirmação.** `PASS`, `DONE` e equivalentes exigem comando, resultado, commit, run ou outra evidência verificável.
5. **Revisão independente.** Quem implementa pode fazer autorrevisão, mas isso não substitui a revisão crítica da entrega.
6. **Feedback em português do Brasil.** Relatórios, estados, findings e mensagens ao usuário devem ser claros, objetivos e em PT-BR, preservando nomes técnicos quando necessário.
7. **Economia de tokens sem sacrificar correção.** Ler primeiro índices, contratos, diffs e trechos relevantes; ampliar contexto somente quando houver motivo técnico.
8. **Falhas herdadas são classificadas, não absorvidas.** Use `DEFERRED_GATE` para gates externos/preexistentes e `BLOCKED_BY` quando algo realmente impede o escopo atual.

## Classificações operacionais

- `BLOCKED_BY=<referência>` — dependência ou problema que impede diretamente a tarefa atual.
- `DEFERRED_GATE=<referência>` — falha herdada, externa ou fora do escopo que deve ser registrada e tratada pela frente responsável.
- `none` — nenhuma ocorrência.

`DEFERRED_GATE` **não autoriza ignorar uma regressão causada pela própria tarefa**.

## Economia de tokens

O padrão adota **divulgação progressiva de contexto**:

```text
AGENTS.md curto
   ↓
índices e contrato da tarefa
   ↓
arquivos/diffs diretamente relacionados
   ↓
testes e logs focados
   ↓
contexto amplo do repositório somente quando justificado
```

Regras detalhadas: [`docs/ECONOMIA-DE-TOKENS.md`](docs/ECONOMIA-DE-TOKENS.md).

## Comece por aqui

Para adotar o Fix Development em outro repositório:

1. copie o `AGENTS.md` e adapte apenas as regras realmente específicas do projeto;
2. copie `docs/`, `templates/` e `.agents/skills/`;
3. crie `work/BOARD.md` a partir do template;
4. crie a primeira tarefa em `work/<TASK>/`;
5. dê ao Codex um pedido no formato de issue: objetivo, escopo, fora de escopo, critérios de aceite e referências;
6. deixe o fluxo de estados conduzir a execução até `DONE`.

Guia completo: [`docs/ADOCAO.md`](docs/ADOCAO.md).

## Mapa da documentação

| Documento | Para que serve |
| --- | --- |
| [`AGENTS.md`](AGENTS.md) | Mapa operacional que o Codex deve ler primeiro |
| [`docs/GOVERNANCA.md`](docs/GOVERNANCA.md) | Regras de tarefas atômicas, fonte de verdade e decisões |
| [`docs/ESTADOS.md`](docs/ESTADOS.md) | Máquina de estados e transições permitidas |
| [`docs/FLUXO-DE-TRABALHO.md`](docs/FLUXO-DE-TRABALHO.md) | Processo completo, do intake ao fechamento |
| [`docs/ECONOMIA-DE-TOKENS.md`](docs/ECONOMIA-DE-TOKENS.md) | Regras para reduzir contexto, leituras e repetições |
| [`docs/MULTIAGENTE.md`](docs/MULTIAGENTE.md) | Quando e como paralelizar agentes/subagentes |
| [`docs/REVISAO-E-QUALIDADE.md`](docs/REVISAO-E-QUALIDADE.md) | Testes, review, CI e severidade de findings |
| [`docs/SEGURANCA.md`](docs/SEGURANCA.md) | Gate de segurança proporcional ao risco |
| [`docs/ZIMAOS-CUSTOM-APP.md`](docs/ZIMAOS-CUSTOM-APP.md) | Padrão adicional para apps customizados no ZimaOS |
| [`docs/ADOCAO.md`](docs/ADOCAO.md) | Como aplicar o modelo a um repositório existente ou novo |

## Papéis do fluxo

Os papéis são responsabilidades, não pessoas obrigatoriamente distintas:

- **Orquestrador:** controla escopo, estado, dependências e sequência.
- **Produto/Requisitos:** transforma intenção em comportamento e critérios de aceite.
- **Arquitetura:** define contratos, impactos e estratégia antes da implementação.
- **Implementação:** altera o código estritamente dentro do plano aprovado.
- **QA:** valida comportamento, regressões e gates relevantes.
- **Revisão:** procura defeitos, expansão indevida de escopo e contratos quebrados.
- **Segurança:** avalia riscos proporcionais à superfície alterada.
- **Fechamento:** registra evidências, merge e estado final.

Uma tarefa pequena pode combinar papéis. Uma tarefa crítica pode distribuí-los entre agentes independentes.

## ZimaOS

Projetos destinados a **Customized Apps do ZimaOS** recebem regras adicionais de empacotamento, persistência, portas, healthcheck, backup, atualização, rollback e validação pós-reboot. O fluxo principal continua o mesmo; o ZimaOS adiciona gates específicos de implantação.

Veja [`docs/ZIMAOS-CUSTOM-APP.md`](docs/ZIMAOS-CUSTOM-APP.md).

## Princípio de projeto

O Fix Development não tenta colocar todo o conhecimento no prompt nem em um `AGENTS.md` gigante. O repositório deve funcionar como sistema de registro: regras curtas apontam para documentação versionada e o Codex carrega detalhes **somente quando necessários para a tarefa atual**.

---

**Status do modelo:** versão inicial em construção.
