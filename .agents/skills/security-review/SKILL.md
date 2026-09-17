---
name: security-review
description: Avaliar segurança de uma tarefa do Fix Development de forma proporcional à superfície alterada, produzindo PASS, FINDINGS ou N/A justificado. Use quando a tarefa estiver em SECURITY_REVIEW ou quando mudanças envolverem identidade, permissões, dados sensíveis, migrations, comandos, arquivos não confiáveis, rede, secrets ou operações destrutivas.
---

# Security Review

1. Ler `TASK.md`, `PLAN.md`, diff e `docs/SEGURANCA.md`.
2. Identificar somente as superfícies de risco realmente alteradas.
3. Expandir contexto para callers, contratos e configuração quando necessário.
4. Executar validações/testes aplicáveis.
5. Classificar resultado como:
   - `SECURITY: PASS`;
   - `SECURITY: FINDINGS`;
   - `SECURITY: N/A — <justificativa>`.
6. Registrar findings P0–P3 com superfície, cenário, impacto, evidência e mitigação esperada.
7. P0/P1 aberto impede avanço.
8. Após correção, repetir validação no HEAD novo.
9. Se aprovado, avançar para `READY_TO_MERGE` conforme gates do projeto.

Não fazer auditoria genérica de todo o repositório quando a tarefa possui superfície pequena e bem delimitada.
