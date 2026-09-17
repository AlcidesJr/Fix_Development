# PLAN — FIX-001

## Resumo da solução

Estruturar o repositório em camadas de contexto: README objetivo, `AGENTS.md` curto, documentos detalhados sob `docs/`, templates reutilizáveis, Skills acionáveis sob `.agents/skills/` e uma tarefa real demonstrando o fluxo.

## Superfícies afetadas

- raiz do repositório;
- `docs/`;
- `templates/`;
- `.agents/skills/`;
- `work/`.

## Contratos e compatibilidade

- conteúdo principal em PT-BR;
- modelo genérico e independente de stack;
- estados canônicos centralizados em `docs/ESTADOS.md`;
- Skills apontam para documentação em vez de duplicá-la;
- ZimaOS é extensão opcional.

## Passos de implementação

1. Criar README e mapa operacional.
2. Documentar governança, estados e fluxo.
3. Documentar economia de tokens, multiagente, revisão e segurança.
4. Adicionar guia de adoção e ZimaOS.
5. Adicionar templates e Skills.
6. Registrar o próprio bootstrap em `work/`.
7. Revisar navegação, consistência e escopo.
8. Abrir PR.

## Estratégia de testes

1. Verificar existência de todos os paths referenciados no README/AGENTS.
2. Revisar consistência dos estados entre documentos e templates.
3. Buscar referências indevidas a projetos particulares.
4. Conferir frontmatter das Skills.
5. Revisar diff final antes do PR.

## Segurança

Sem superfície de aplicação executável nesta tarefa. Revisar apenas para evitar orientação que incentive versionamento de secrets ou operações destrutivas inseguras.

## Dados e migrations

N/A.

## Paralelismo

Não necessário para o bootstrap documental.

## Rollback

Reverter commits/PR; sem dados persistentes afetados.

## Riscos

- documentação excessiva → mitigado por `AGENTS.md` curto e navegação progressiva;
- duplicação → documentos centrais como fonte de verdade e Skills curtas;
- especificidade → exemplos e prefixos genéricos.
