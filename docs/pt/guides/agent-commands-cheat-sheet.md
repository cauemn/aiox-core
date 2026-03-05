<!--
  Idioma: PT-BR
  Fonte de verdade dos comandos: .aiox-core/development/agents/*.md
  Ultima atualizacao: 2026-03-05
-->

# Guia de Bolso: Comandos dos Agentes AIOX

Este guia prioriza uso pratico: qual agente ativar e quais comandos rodar em cada cenario.

## Uso em 30 segundos

1. Ative um agente: `@dev`, `@qa`, `@po`, etc.
2. Rode `*help` para ver todos os comandos do agente ativo.
3. Execute o comando da tarefa.
4. Troque de agente quando mudar de etapa.
5. Finalize com `*exit`.

Exemplo rapido:

```text
@dev
*develop
```

Ou em uma linha:

```text
@dev *develop
```

## Regras importantes

- `@devops` e o agente com autoridade para `*push`, `*create-pr` e `*release`.
- Workflow padrao: story primeiro (`@sm` / `@po`), implementacao depois (`@dev`), validacao (`@qa`), entrega (`@devops`).
- Se estiver em duvida, rode `*help` e siga os comandos listados no agente atual.

## Matriz rapida: objetivo -> agente -> comando

| Objetivo | Agente | Comando inicial | Comando de fechamento |
| --- | --- | --- | --- |
| Tirar ideia do papel | `@analyst` | `*create-project-brief` | handoff para `@pm` |
| Definir produto | `@pm` | `*create-prd` | `*create-epic` |
| Desenhar arquitetura | `@architect` | `*create-full-stack-architecture` | `*create-plan` |
| Criar story | `@sm` | `*draft` | handoff para `@po` |
| Validar story | `@po` | `*validate-story-draft` | handoff para `@dev` |
| Implementar | `@dev` | `*develop` | `*run-tests` |
| Revisar qualidade | `@qa` | `*review` | `*gate` |
| Entregar | `@devops` | `*pre-push` | `*push` + `*create-pr` |
| Fechar ciclo | `@po` | `*close-story` | backlog atualizado |

## Fluxo 1: Da ideia ao deploy (fim a fim)

### Quando usar

- Voce tem uma ideia nova e quer levar ate producao.

### Sequencia recomendada

```text
@analyst
*create-project-brief

@pm
*create-prd
*create-epic

@architect
*create-full-stack-architecture

@sm
*draft

@po
*validate-story-draft

@dev
*develop
*run-tests

@qa
*review
*gate

@devops
*pre-push
*push
*create-pr
```

Depois do merge:

```text
@devops
*release

@po
*close-story
```

## Fluxo 2: Implementacao simples (story ja pronta)

### Quando usar

- Story ja validada, mudanca pequena, baixo risco.

### Sequencia recomendada

```text
@dev
*develop
*run-tests

@qa
*review

@devops
*pre-push
*push
*create-pr
```

## Fluxo 3: Fix de bug

### Quando usar

- Bug reproduzido, precisa corrigir com rastreabilidade.

### Sequencia recomendada

```text
@qa
*review
*create-fix-request

@dev
*fix-qa-issues
*run-tests

@qa
*review
*gate

@devops
*pre-push
*push
*create-pr
```

Atalho comum para ajuste rapido de review:

```text
@dev
*apply-qa-fixes
```

## Fluxo 4: Feature nova com banco de dados

### Quando usar

- Feature envolve schema, migracao, RLS ou query critica.

### Sequencia recomendada

```text
@architect
*assess-complexity
*create-plan

@data-engineer
*snapshot pre-feature
*dry-run path/to/migration.sql
*apply-migration path/to/migration.sql
*security-audit schema

@dev
*develop
*run-tests

@qa
*validate-migrations
*security-check
*review

@devops
*pre-push
*push
*create-pr
```

## Fluxo 5: Feature de UI / design system

### Quando usar

- Tela nova, componente novo, padrao visual novo.

### Sequencia recomendada

```text
@ux-design-expert
*research
*wireframe high
*create-front-end-spec

@dev
*develop

@qa
*review

@devops
*pre-push
*create-pr
```

## Modo incidente: hotfix em producao

### Quando usar

- Erro critico em producao (quebra de fluxo, regressao grave, indisponibilidade).

### Sequencia recomendada

```text
@qa
*risk-profile
*review

@dev
*develop
*run-tests

@qa
*gate

@devops
*pre-push
*push
*create-pr
```

Se houver necessidade de release imediata:

```text
@devops
*release
```

## Comandos de bolso por agente (top comandos)

### @sm

- `*draft`
- `*story-checklist`

### @po

- `*validate-story-draft`
- `*stories-index`
- `*close-story`

### @pm

- `*create-prd`
- `*create-epic`
- `*create-story`

### @architect

- `*create-full-stack-architecture`
- `*assess-complexity`
- `*create-plan`

### @data-engineer

- `*create-schema`
- `*create-migration-plan`
- `*snapshot {label}`
- `*dry-run {path}`
- `*apply-migration {path}`

### @dev

- `*develop`
- `*run-tests`
- `*execute-subtask`
- `*verify-subtask`
- `*fix-qa-issues`

### @qa

- `*review`
- `*gate`
- `*create-fix-request`
- `*security-check`

### @devops

- `*pre-push`
- `*push`
- `*create-pr`
- `*release`

### @analyst

- `*create-project-brief`
- `*perform-market-research`
- `*create-competitor-analysis`

### @ux-design-expert

- `*research`
- `*wireframe {fidelity}`
- `*create-front-end-spec`
- `*build {component}`

### @squad-creator

- `*design-squad`
- `*create-squad`
- `*validate-squad`

### @aiox-master

- `*create`
- `*modify`
- `*workflow`
- `*validate-workflow`

## Atalhos de ativacao

- `@aiox-master`
- `@analyst`
- `@architect`
- `@data-engineer`
- `@dev`
- `@devops`
- `@pm`
- `@po`
- `@qa`
- `@sm`
- `@squad-creator`
- `@ux-design-expert`

## Referencia completa

Para lista completa de comandos e parametros, use `*help` no agente ativo e consulte `.aiox-core/development/agents/*.md`.