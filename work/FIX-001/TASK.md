# TASK — FIX-001

## Título

Bootstrap do padrão público v1

## Objetivo

Criar a primeira versão pública e genérica do Fix Development para desenvolvimento assistido por Codex, com documentação em português do Brasil, tarefas atômicas, estados, economia de tokens, Skills, templates e extensão para ZimaOS Customized Apps.

## Escopo

- README objetivo para a página inicial do GitHub;
- `AGENTS.md` curto como mapa operacional;
- governança e máquina de estados;
- fluxo de trabalho e multiagente;
- política revisada de economia de tokens;
- revisão, qualidade e segurança;
- guia de adoção;
- trilha ZimaOS Customized App;
- templates reutilizáveis;
- Skills do Codex;
- guia de contribuição em PT-BR;
- uso do próprio modelo no repositório.

## Fora de escopo

- regras específicas de projetos privados/particulares;
- escolher stack de aplicação;
- exigir provedor cloud específico;
- publicar pacote em App Store do ZimaOS;
- automação completa de criação de tarefas;
- definição de licença do repositório.

## Critérios de aceite

- [ ] README apresenta o modelo objetivamente e permite navegação rápida.
- [ ] Feedback e templates estão em português do Brasil.
- [ ] Estados e transições estão documentados.
- [ ] `BLOCKED_BY` e `DEFERRED_GATE` estão definidos sem ambiguidade.
- [ ] Economia de tokens possui regras práticas e prioridade de risco/correção.
- [ ] O modelo é genérico e não menciona projetos particulares como exemplo operacional.
- [ ] Existe seção completa para ZimaOS Customized App.
- [ ] Templates essenciais existem.
- [ ] Skills essenciais do Codex existem.
- [ ] Links principais do README resolvem para arquivos existentes.

## Dependências

- DEPENDS_ON: none

## Riscos conhecidos

- excesso de documentação aumentar contexto em vez de reduzi-lo;
- regras específicas demais reduzirem aplicabilidade genérica;
- extensão ZimaOS ser confundida com requisitos de App Store.

## Referências

- documentação oficial atual do Codex/OpenAI sobre gestão de contexto e Skills;
- documentação/ecossistema oficial atual do ZimaOS/CasaOS App Store para distinção de App Store.
