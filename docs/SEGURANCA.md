# Segurança

## Objetivo

Aplicar revisão de segurança proporcional ao risco da mudança, sem transformar toda tarefa em auditoria completa.

## Regra de entrada

Toda tarefa em `SECURITY_REVIEW` deve receber uma das classificações:

```text
SECURITY: PASS
SECURITY: FINDINGS
SECURITY: N/A — <justificativa curta>
```

`N/A` é aceitável para mudanças sem superfície de segurança relevante, desde que a justificativa seja explícita.

## Superfícies a considerar

Conforme a tarefa, verificar:

- autenticação e identidade;
- autorização e isolamento entre usuários/tenants;
- validação e normalização de entrada;
- SQL/queries e injeção;
- comandos de shell/processos;
- filesystem e traversal;
- upload/download de arquivos;
- serialização/deserialização;
- SSRF e chamadas externas;
- CORS/CSRF quando aplicável;
- secrets, tokens e credenciais;
- logging de informação sensível;
- criptografia e armazenamento de dados sensíveis;
- dependências e cadeia de suprimentos;
- permissões de infraestrutura;
- operações destrutivas e rollback;
- exposição de portas/serviços;
- rate limiting e abuso, quando relevante.

Não carregue toda essa lista no contexto de um subagente se apenas uma superfície for aplicável; selecione o necessário.

## Processo

1. Ler `TASK.md`, `PLAN.md` e diff.
2. Identificar superfícies de risco realmente alteradas.
3. Inspecionar contratos/callers necessários.
4. Executar testes de segurança/regressão aplicáveis.
5. Registrar findings concretos.
6. Revalidar após correção.

## Findings

Use a mesma escala P0–P3 de `REVISAO-E-QUALIDADE.md`.

Finding de segurança deve conter:

```text
SEVERIDADE: P0|P1|P2|P3
SUPERFÍCIE: <...>
CENÁRIO: <condição de exploração/falha>
IMPACTO: <...>
EVIDÊNCIA: <código/teste/configuração>
MITIGAÇÃO ESPERADA: <propriedade que deve ser garantida>
```

Evite descrever exploração desnecessariamente além do que é preciso para corrigir e testar o problema.

## Gates

- P0/P1 aberto: bloqueia merge.
- P2: corrigir ou formalizar tratamento conforme política do projeto.
- P3: pode ser backlog quando não representar risco material imediato.

## Mudanças de alto risco

Exigem revisão mais ampla e evidência de rollback quando aplicável:

- autenticação/autorização;
- migrations ou transformação destrutiva de dados;
- secrets/credenciais;
- código que executa comandos;
- upload/processamento de arquivos não confiáveis;
- exposição pública de novos serviços;
- mudanças de privilégio;
- webhooks e integrações externas com efeitos mutáveis.

## Secrets

Nunca versionar:
- chaves privadas;
- tokens reais;
- senhas;
- arquivos `.env` com segredos;
- dumps com dados sensíveis.

Use placeholders e documentação de configuração.

Se um segredo for encontrado no histórico, remover do código não é suficiente: registrar necessidade de revogação/rotação conforme o provedor.

## Segurança como contrato

Quando uma regra de segurança for recorrente, prefira transformá-la em:
- teste;
- lint/regra automatizada;
- configuração de CI;
- script determinístico;
- documentação versionada curta e referenciada.

Feedback repetido deve melhorar o sistema, não depender para sempre da memória do agente.
