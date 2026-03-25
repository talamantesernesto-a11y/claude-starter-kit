# Claude Starter Kit

Skills, rules y metodologia curada para desarrollo productivo con Claude Code. Probado en produccion en multiples proyectos SaaS y agentes de IA.

## Instalacion

```bash
claude install github:talamantesernesto-a11y/claude-starter-kit
```

Eso es todo. Los skills, rules y commands se instalan automaticamente.

## Que incluye

### Skills (se activan automaticamente segun contexto)

| Skill | Que hace | Cuando se activa |
|-------|----------|------------------|
| **inicio-de-proyecto** | Scaffold completo para nuevos proyectos o adaptar existentes | "nuevo proyecto", "iniciar proyecto" |
| **brainstorming** | Explora ideas antes de implementar, propone 2-3 enfoques | "tengo una idea", "quiero construir" |
| **task-plan** | Gestion de tareas en `tasks/todo.md` que persiste entre sesiones | Tareas de 3+ pasos |
| **self-correct** | Captura correcciones en `tasks/lessons.md` para no repetir errores | Automatico al corregir al agente |
| **systematic-debugging** | Debugging metodico: root cause antes de fixes | "no funciona", "hay un error" |
| **orchestrator** | El skill de "no se por donde empezar" | "que hago primero", "estoy atorado" |
| **blueprint** | Convierte una idea en plan de construccion paso a paso | Proyectos nuevos o features grandes |
| **local-review** | Code review local antes de commit | "revisa mi codigo", antes de push |
| **create-prd** | Crea PRDs completos que los ingenieros si leen | "escribeme un PRD", "spec this out" |
| **explain-code** | Explica codigo con diagramas y analogias | "como funciona esto", "explicame" |

### Rules (metodologia aplicada automaticamente)

| Rule | Que hace |
|------|----------|
| **coding-style** | Inmutabilidad, archivos pequenos, error handling |
| **testing** | TDD obligatorio, 80% coverage minimo |
| **git-workflow** | Conventional commits, PR workflow |
| **development-workflow** | Pipeline completo: research, plan, TDD, review, commit |
| **security** | Checklist de seguridad antes de cada commit |
| **performance** | Seleccion de modelo, context window management |
| **patterns** | Repository pattern, API response format |
| **hooks** | PreToolUse, PostToolUse, TodoWrite best practices |
| **agents** | Orquestacion de agentes especializados |

### Commands (slash commands)

| Command | Que hace |
|---------|----------|
| `/plan` | Crea plan de implementacion estructurado |
| `/tdd` | Workflow de test-driven development |
| `/code-review` | Review de codigo con 4 passes (bugs, seguridad, calidad, arquitectura) |
| `/build-fix` | Resolver errores de build |
| `/verify` | Verificacion post-implementacion |

## Filosofia

**Context engineering > prompt engineering.** El secreto no esta en el prompt, esta en el contexto. Este kit carga contexto rico (quien eres, tu proyecto, preferencias, herramientas) para que prompts simples den resultados excelentes.

### Principios clave

1. **Plan antes de codear** — No escribas codigo sin un plan aprobado
2. **Tests primero (TDD)** — RED, GREEN, IMPROVE. Siempre.
3. **Root cause antes de fix** — No adivines, investiga
4. **Inmutabilidad** — Nunca mutes, siempre crea copias nuevas
5. **Archivos pequenos** — 200-400 lineas tipico, 800 max
6. **Self-correct** — Cada correccion se guarda como leccion para no repetir errores

## Primeros pasos despues de instalar

1. Abre un proyecto y escribe: **"inicio de proyecto"** o **"new project"**
2. Claude te hara una entrevista para generar tu `claude.md`, `memory.md` y `context/`
3. Empieza a trabajar normalmente — los skills se activan solos segun el contexto
4. Cuando Claude se equivoque, corrigelo — `self-correct` guardara la leccion

## Estructura del repo

```
claude-starter-kit/
├── .claude-plugin/
│   └── plugin.json          # Manifiesto del plugin
├── skills/
│   ├── inicio-de-proyecto/   # Scaffold de proyectos
│   │   ├── SKILL.md
│   │   └── references/       # Templates (claude.md, memory.md, todo.md)
│   ├── brainstorming/        # Ideacion antes de implementar
│   ├── task-plan/            # Gestion de tareas persistente
│   ├── self-correct/         # Captura de correcciones
│   ├── systematic-debugging/ # Debugging metodico + referencias
│   ├── orchestrator/         # "No se por donde empezar"
│   ├── blueprint/            # Idea → plan de construccion
│   ├── local-review/         # Code review local
│   ├── create-prd/           # Product Requirements Documents
│   └── explain-code/         # Explicaciones con diagramas
├── rules/
│   └── common/               # Metodologia (coding style, TDD, security, etc.)
├── commands/                  # Slash commands (/plan, /tdd, /code-review, etc.)
├── package.json
└── README.md
```

## Compatibilidad

- Claude Code CLI
- Requiere Node.js >= 18

## Licencia

MIT
