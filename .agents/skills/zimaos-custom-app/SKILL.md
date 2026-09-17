---
name: zimaos-custom-app
description: Aplicar gates adicionais para desenvolver, atualizar ou revisar aplicações destinadas ao App Management / Customized App do ZimaOS. Use quando a tarefa envolver Docker Compose para ZimaOS, persistência, portas, healthcheck, backup, atualização, rollback, registry, validação de versão ou comportamento pós-reboot.
---

# ZimaOS Customized App

1. Ler `docs/ZIMAOS-CUSTOM-APP.md` e o plano da tarefa.
2. Confirmar quem gerencia o Compose e evitar fontes de verdade concorrentes.
3. Validar Compose, `name` estável, imagens/versionamento, portas, mounts, redes, restart e healthchecks aplicáveis.
4. Fazer preflight de portas; não interromper serviços não relacionados para liberar conflito.
5. Classificar necessidade de backup antes de upgrade.
6. Confirmar rollback antes de mudança destrutiva ou migration.
7. Validar build/pull e versão interna da imagem quando aplicável.
8. Após deploy, verificar containers, health, imagem, portas, mounts, versão e smoke test.
9. Executar/registrar pós-reboot quando o gate for exigido.
10. Registrar em `EVIDENCE.md` somente resultados e referências úteis; não copiar logs extensos.

Campos recomendados:

```text
ZIMAOS_COMPOSE: PASS|FAIL|N/A
ZIMAOS_BACKUP: PASS|FAIL|N/A
ZIMAOS_HEALTH: PASS|FAIL|N/A
ZIMAOS_PERSISTENCE: PASS|FAIL|N/A
ZIMAOS_ROLLBACK: PASS|FAIL|N/A
ZIMAOS_REBOOT: PASS|FAIL|N/A
```

Metadados de App Store, como `x-casaos`, só são obrigatórios quando a tarefa inclui publicação/empacotamento para a loja.
