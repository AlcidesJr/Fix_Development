# Referências

O Fix Development é um modelo independente. As fontes abaixo ajudam a justificar decisões de desenho e devem ser revisitadas quando o Codex ou o ecossistema ZimaOS mudarem.

## Codex / OpenAI

### Harness engineering: leveraging Codex in an agent-first world

https://openai.com/index/harness-engineering/

Princípios adotados:
- repositório como sistema de registro;
- `AGENTS.md` curto como mapa;
- contexto como recurso escasso;
- objetivos de alto nível decompostos em blocos verificáveis;
- revisão e feedback entre agentes.

### Unrolling the Codex agent loop

https://openai.com/index/unrolling-the-codex-agent-loop/

Princípios adotados:
- gestão ativa de janela de contexto;
- compactação para sessões longas;
- contexto deve preservar informação relevante sem depender de histórico ilimitado.

### How OpenAI uses Codex

https://openai.com/business/guides-and-resources/how-openai-uses-codex/

Princípios adotados:
- prompts semelhantes a issues;
- `AGENTS.md` como contexto persistente;
- delegação de tarefas bem delimitadas.

### Skill Creator

https://github.com/openai/skills/blob/main/skills/.system/skill-creator/SKILL.md

Princípios adotados:
- Skills modulares;
- `SKILL.md` conciso;
- divulgação progressiva;
- referências carregadas sob demanda;
- scripts para rotinas determinísticas/repetitivas.

## ZimaOS

### ZimaOS App Store source / documentação

https://github.com/IceWhaleTech/CasaOS-AppStore

### Quick start de stores compatíveis

https://github.com/IceWhaleTech/CasaOS-AppStore/blob/main/docs/quick-start/overview.md

Uso no Fix Development:
- distinguir instalação como Customized App de empacotamento/publicação em App Store;
- tratar metadados de loja como requisito somente quando a tarefa realmente inclui distribuição via store.

## Política de atualização

Referências externas são informativas, não substituem a governança local do projeto.

Quando uma mudança relevante do Codex ou ZimaOS invalidar uma regra:
1. abrir tarefa atômica para atualizar o padrão;
2. citar a fonte nova;
3. atualizar documentos/Skills afetados;
4. registrar impacto para usuários que já adotaram o modelo.
