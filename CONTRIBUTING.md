# Contribuindo com o Fix Development

Obrigado por ajudar a tornar o modelo mais simples, verificável e útil para a comunidade.

## Idioma

A documentação principal e o feedback de contribuição devem ser escritos em **português do Brasil**. Termos técnicos podem permanecer em inglês quando isso preservar precisão.

## Antes de propor uma mudança

Pergunte:

1. O problema é recorrente o suficiente para virar regra?
2. A regra pode ser verificada automaticamente por teste, lint ou script?
3. Ela já existe em outro documento?
4. A mudança reduz ambiguidade sem inflar contexto?
5. Ela é genérica o suficiente para diferentes tipos de projeto?

## Princípios de contribuição

- preservar tarefas atômicas;
- manter `AGENTS.md` curto;
- evitar duplicação entre documentos e Skills;
- preferir exemplos genéricos;
- não incorporar nomes, paths, portas ou decisões de projetos particulares;
- manter feedback e templates em PT-BR;
- tratar economia de tokens como seleção de contexto, nunca como redução de qualidade;
- adicionar regras de ZimaOS somente à trilha ZimaOS quando não forem universais.

## Mudanças em estados

Alterar a máquina de estados possui impacto amplo. Uma proposta deve explicar:
- problema que o estado atual não resolve;
- transição nova/alterada;
- impacto em templates e Skills;
- compatibilidade com tarefas já existentes.

## Mudanças em Skills

Mantenha `SKILL.md` conciso. Coloque somente procedimento necessário para execução. Informações detalhadas devem ser referenciadas em `docs/` ou em `references/` específicas da Skill quando realmente necessárias.

## Pull Request

O PR deve informar:
- problema;
- mudança proposta;
- arquivos afetados;
- como a mudança foi validada;
- impacto em compatibilidade/adoção;
- se exige migração de quem já utiliza o modelo.

## Regra de ouro

Se uma nova regra torna o agente mais previsível mas obriga todas as tarefas a carregar muito mais contexto, procure primeiro uma forma de aplicá-la **sob demanda**.
