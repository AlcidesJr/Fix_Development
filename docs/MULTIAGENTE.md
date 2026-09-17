# Execução multiagente

## Princípio

Use múltiplos agentes para reduzir tempo de ciclo **somente quando o trabalho puder ser dividido sem criar ambiguidade ou edição concorrente desnecessária**.

Mais agentes aumentam coordenação, contexto e custo. Paralelismo é ferramenta, não objetivo.

## Papéis

### Orquestrador

Responsável por:
- estado e escopo;
- dependências;
- contrato entre subescopos;
- distribuição de trabalho;
- integração das saídas;
- decisão de quando ampliar contexto;
- progressão dos estados.

### Produto/Requisitos

Transforma intenção em comportamento observável e critérios de aceite. Não decide arquitetura por conta própria.

### Arquitetura

Define contratos, fronteiras, dados, compatibilidade e estratégia técnica antes de trabalhos paralelos.

### Implementação

Executa um subescopo bem definido e verifica localmente sua entrega.

### QA

Desenha e executa validações independentes do raciocínio do implementador.

### Reviewer

Procura defeitos concretos e expansão de escopo. Não deve reescrever código apenas por preferência estética.

### Segurança

Analisa superfícies de risco e registra findings com evidência.

### Fechamento

Consolida evidências e atualiza o estado final.

## Quando paralelizar

Bom candidato:
- contratos já definidos;
- ownership de arquivos/superfícies claro;
- subescopos independentes;
- integração final previsível;
- ganho de tempo relevante.

Exemplo genérico:

```text
              contrato estável
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      API         migration    testes
        │           │           │
        └───────────┼───────────┘
                    ▼
                integração
```

## Quando NÃO paralelizar

Evite quando:
- a arquitetura ainda está sendo descoberta;
- agentes editariam os mesmos arquivos/linhas;
- um subescopo depende da saída ainda indefinida de outro;
- todos precisariam carregar o mesmo contexto grande;
- a tarefa é pequena e a coordenação custa mais que a execução.

## Contrato de subagente

Todo subagente deve receber uma instrução semelhante a:

```text
Papel: <...>
Objetivo: <...>
Escopo: <...>
Fora de escopo: <...>
Entradas/contratos: <...>
Ownership: <arquivos ou superfícies>
Validação obrigatória: <...>
Saída esperada: <diff, relatório, testes, findings...>
Critério de conclusão: <...>
Idioma do feedback: português do Brasil
```

Não envie toda a conversa do Orquestrador sem necessidade.

## Regras de ownership

- preferir um agente escritor por superfície mutável;
- leitores/reviewers podem compartilhar superfície;
- se dois implementadores precisarem do mesmo arquivo, serializar ou redefinir fronteiras;
- integração deve ser feita pelo Orquestrador ou por um agente explicitamente responsável por integração.

## Revisão independente

Um agente implementador pode fazer autorrevisão, mas review independente deve começar do contrato e diff, não da justificativa interna do implementador.

Isso reduz confirmação do próprio raciocínio.

## Saída dos subagentes

Prefira respostas compactas:

```text
RESULTADO: PASS | FINDINGS | BLOCKED
ALTERAÇÕES: <resumo>
TESTES: <resumo + evidência>
FINDINGS: <se houver>
BLOCKED_BY: <...|none>
PRÓXIMO PASSO: <...>
```

Detalhes técnicos duráveis devem ser escritos nos artefatos da tarefa, não repetidos em mensagens longas.

## Integração

O Orquestrador deve:
1. verificar se cada saída respeitou o contrato;
2. detectar conflitos semânticos, não apenas conflitos Git;
3. executar testes de integração;
4. atualizar evidências;
5. somente então avançar o estado.

## Worktrees

Quando o ambiente suportar worktrees ou sandboxes isolados:
- usar uma por implementação paralela quando houver benefício real;
- partir do mesmo contrato/base conhecida;
- não assumir que um agente vê alterações ainda não integradas de outro;
- integrar de forma controlada e testar novamente após combinação.
