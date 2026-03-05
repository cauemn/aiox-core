# Guia de Bolsillo: Comandos de Agentes AIOX

> [EN](../../guides/agent-commands-cheat-sheet.md) | [PT](../../pt/guides/agent-commands-cheat-sheet.md) | **ES**

Referencia practica: que agente activar y que comando ejecutar.

## Uso en 30 segundos

1. Activa un agente: `@dev`, `@qa`, `@po`, etc.
2. Ejecuta `*help` para listar comandos.
3. Ejecuta el comando de la tarea.
4. Cambia de agente cuando cambie la etapa.
5. Finaliza con `*exit`.

```text
@dev
*develop
```

## Reglas importantes

- `@devops` tiene autoridad para `*push`, `*create-pr` y `*release`.
- Flujo estandar: historia primero (`@sm` / `@po`), implementacion (`@dev`), validacion (`@qa`), entrega (`@devops`).
- Si tienes duda, usa `*help`.

## Matriz rapida: objetivo -> agente -> comando

| Objetivo | Agente | Comando inicial | Comando de cierre |
| --- | --- | --- | --- |
| Definir idea | `@analyst` | `*create-project-brief` | handoff a `@pm` |
| Definir producto | `@pm` | `*create-prd` | `*create-epic` |
| Definir arquitectura | `@architect` | `*create-full-stack-architecture` | `*create-plan` |
| Crear historia | `@sm` | `*draft` | handoff a `@po` |
| Validar historia | `@po` | `*validate-story-draft` | handoff a `@dev` |
| Implementar | `@dev` | `*develop` | `*run-tests` |
| Validar calidad | `@qa` | `*review` | `*gate` |
| Entregar | `@devops` | `*pre-push` | `*push` + `*create-pr` |
| Cerrar ciclo | `@po` | `*close-story` | backlog actualizado |

## Flujo 1: Idea a deploy (end-to-end)

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

Despues del merge:

```text
@devops
*release

@po
*close-story
```

## Flujo 2: Implementacion simple

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

## Flujo 3: Fix de bug

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

Atajo rapido:

```text
@dev
*apply-qa-fixes
```

## Flujo 4: Feature nueva con base de datos

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

## Flujo 5: Feature nueva de UI/design system

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

## Modo incidente: hotfix en produccion

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

Si hace falta release inmediato:

```text
@devops
*release
```

## Atajos de activacion

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

Usa `*help` en el agente activo y consulta `.aiox-core/development/agents/*.md`.