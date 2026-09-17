# Desenvolvimento para ZimaOS Customized App

## Objetivo

Adicionar gates específicos para projetos que serão instalados e mantidos pelo **App Management / Customized App do ZimaOS**.

Este documento complementa o fluxo principal. A tarefa continua usando os mesmos estados, evidências, review e classificação de gates.

## 1. Princípio de gerenciamento

Se o projeto foi definido como Customized App, trate o App Management do ZimaOS como a camada de gerenciamento da aplicação.

Evite criar uma instalação que só funciona quando iniciada manualmente por outra ferramenta e desaparece da governança esperada do ZimaOS.

O Compose entregue deve ser a representação reproduzível da aplicação.

## 2. Compose mínimo

O `docker-compose.yml` deve declarar explicitamente, conforme aplicável:

- `name` estável para o projeto;
- serviços;
- imagens com versão controlada;
- portas publicadas;
- volumes persistentes;
- redes necessárias;
- variáveis de ambiente não secretas;
- política de restart;
- healthcheck para serviços críticos;
- dependências/ordem de inicialização quando realmente necessárias.

Evite depender de defaults implícitos importantes.

## 3. Imagens e versões

Para releases reproduzíveis:

- prefira tags imutáveis/versionadas;
- evite `latest` em produção quando a atualização precisa ser controlada;
- exponha versão da aplicação por endpoint, comando, label ou arquivo verificável;
- quando houver build local, valide a versão **dentro da imagem** antes da implantação.

## 4. Persistência

Dados que precisam sobreviver a:

- recriação de container;
- atualização de imagem;
- reboot;
- rollback;

não podem existir somente na camada gravável do container.

Para cada volume/bind mount, documente:

```text
origem
container path
finalidade
backup necessário? sim/não
permissões relevantes
```

Nunca misture dados persistentes com diretórios temporários sem necessidade.

## 5. Secrets

Não versionar secrets no Compose.

A forma de injeção deve ser documentada e compatível com o ambiente alvo. Se o fluxo depender de `.env`, secrets externos ou outro mecanismo, valide que a versão alvo do ZimaOS e o método de instalação escolhido realmente o suportam.

## 6. Portas

Antes do deploy:

1. listar todas as portas publicadas pelo Compose;
2. verificar conflito no host;
3. falhar o preflight se uma porta obrigatória estiver ocupada;
4. permitir porta configurável quando o produto suportar isso;
5. registrar a porta final em `EVIDENCE.md`.

Não "resolver" conflito matando serviço não relacionado.

## 7. Healthcheck

Serviço crítico deve preferencialmente possuir healthcheck que valide comportamento útil, não apenas processo existente.

Exemplos:
- endpoint HTTP `/health`;
- conexão simples com serviço interno;
- comando de diagnóstico da própria aplicação.

Defina intervalos e retries compatíveis com o tempo real de inicialização.

## 8. Backup antes de atualização

Toda atualização com dados persistentes deve classificar se backup é necessário.

Quando necessário:

1. criar backup antes de substituir imagem/schema;
2. registrar path/artefato e tamanho quando útil;
3. validar que o backup foi criado;
4. para bancos, preferir mecanismo nativo consistente (`pg_dump`, dump lógico equivalente, snapshot validado etc.);
5. registrar procedimento de restauração/rollback.

## 9. Upgrade reproduzível

Fluxo recomendado para release/update:

```text
validar artefato
→ validar checksum quando fornecido
→ backup
→ preparar release em área separada
→ validar versão e Compose
→ build/pull da imagem
→ validar versão interna da imagem
→ publicar/taguear imagem quando aplicável
→ atualizar Compose gerenciado pelo app
→ recriar serviços
→ validar health/status
→ validar mounts e persistência
→ validar versão exposta
→ smoke test
→ validação pós-reboot quando exigida
```

Não sobrescreva a única cópia do release anterior antes de existir caminho de rollback.

## 10. Build

Quando a aplicação possui Dockerfile próprio:

- build deve partir de fonte versionada;
- `docker compose config` ou validação equivalente deve passar antes do deploy;
- argumentos de build devem ser explícitos;
- versão deve ser rastreável até commit/release;
- cache não deve mascarar arquivo esperado ausente;
- uma build aprovada deve ser identificável por tag/digest.

## 11. Registry

O padrão não exige registry local nem remoto específico.

Se houver registry:
- documentar endereço;
- usar tag versionada;
- validar push/pull;
- registrar imagem/digest efetivamente implantado.

## 12. Rollback

Antes do upgrade, responder:

- qual imagem anterior será restaurada?
- há mudança de schema?
- downgrade é suportado?
- backup precisa ser restaurado?
- qual Compose anterior deve ser usado?

Se rollback não for seguro, isso deve estar explícito no `PLAN.md` antes da mudança.

## 13. Validação pós-deploy

Registrar, conforme aplicável:

```text
compose válido
containers esperados running/healthy
imagem/tag/digest corretos
portas corretas
mounts corretos
redes corretas
endpoint de health PASS
versão interna PASS
smoke test PASS
dados persistentes presentes
```

## 14. Validação pós-reboot

Para apps que devem sobreviver a reboot, a tarefa/release só deve considerar o requisito comprovado quando houver evidência de:

- containers retornando automaticamente;
- healthcheck estabilizando;
- mounts persistentes presentes;
- dados íntegros;
- serviço acessível na porta esperada.

Projetos podem tornar esse gate obrigatório apenas em releases maiores, desde que a política esteja documentada.

## 15. Pacote de release

Quando o projeto distribui pacote fonte/binário, recomenda-se entregar:

```text
artefato versionado
checksum SHA-256
CHANGELOG/release notes quando aplicável
guia de instalação limpa
guia de atualização
guia de rollback
Compose/Dockerfile versionados
```

## 16. App Store não é Customized App

Publicar um app em uma loja compatível com ZimaOS adiciona requisitos de manifesto/metadados próprios, como estrutura da store e campos `x-casaos`.

Não imponha esses metadados a todo Customized App. Adote-os somente quando o objetivo da tarefa incluir empacotamento para App Store.

## 17. Problemas de gerenciamento externo

Ao combinar ZimaOS com ferramentas externas de Docker:

- valide quem é a fonte de verdade do Compose;
- evite dois gerenciadores recriando o mesmo projeto;
- não presuma que alterações feitas fora do App Management serão refletidas corretamente na interface;
- teste recuperação/importação e atualização antes de declarar o fluxo suportado.

## Gate ZimaOS no STATUS.md

Projetos ZimaOS podem acrescentar:

```text
ZIMAOS_COMPOSE: PASS|FAIL|N/A
ZIMAOS_BACKUP: PASS|FAIL|N/A
ZIMAOS_HEALTH: PASS|FAIL|N/A
ZIMAOS_PERSISTENCE: PASS|FAIL|N/A
ZIMAOS_ROLLBACK: PASS|FAIL|N/A
ZIMAOS_REBOOT: PASS|FAIL|N/A
```
