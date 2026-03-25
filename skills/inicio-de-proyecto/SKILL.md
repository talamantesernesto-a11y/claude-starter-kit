---
name: inicio-de-proyecto
description: "Scaffold a new project workspace OR adapt an existing project to the Claude structure. Creates/audits claude.md, memory.md, and context/ folder. Use when: starting a new project, opening an existing project that lacks claude.md, or reformatting an existing claude.md. Trigger words: 'nuevo proyecto', 'inicio de proyecto', 'crear proyecto', 'new project', 'initialize project', 'scaffold workspace', 'arrancar proyecto', 'empezar proyecto', 'configurar proyecto', 'setup project', 'adaptar proyecto', 'fix my claude.md', 'organizar proyecto'."
---

# Inicio de Proyecto

Scaffold completo para iniciar un nuevo workspace de proyecto. Genera la estructura de archivos (claude.md, memory.md, context/) y ejecuta una entrevista para poblar el contexto inicial.

## Principio Central

Context engineering > prompt engineering. Cargar contexto rico (quien eres, tu negocio, preferencias, herramientas) para que prompts simples den resultados excelentes. El secreto no esta en el prompt, esta en el contexto.

## Workflow: Inicio de Proyecto

### Fase 0: Deteccion — Proyecto Nuevo o Existente

Antes de cualquier otra cosa, inspeccionar el directorio actual (o el que indique el usuario):

1. **Buscar archivos clave**: `claude.md`, `CLAUDE.md`, `memory.md`, carpeta `context/`
2. **Buscar codigo existente**: `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, `src/`, `app/`, etc.
3. **Buscar otros archivos de contexto sueltos**: READMEs, docs, .env.example, etc.

**Resultado A — Proyecto vacio o nuevo** (no hay codigo ni claude.md):
→ Continuar con Fase 1 normalmente.

**Resultado B — Proyecto existente SIN estructura Claude** (hay codigo pero no hay claude.md):
→ Ir a Fase 0b: Adaptacion de Proyecto Existente.

**Resultado C — Proyecto existente CON claude.md** (ya tiene claude.md pero puede estar mal formateado):
→ Ir a Fase 0c: Auditoria y Reformateo.

---

#### Fase 0b: Adaptacion de Proyecto Existente (sin claude.md)

El proyecto ya tiene codigo pero no tiene la estructura de Claude. Hacer lo siguiente:

1. **Escanear el proyecto** para entender que es:
   - Leer `package.json`, `pyproject.toml`, `README.md`, o equivalentes
   - Identificar tech stack, dependencias, estructura de carpetas
   - Detectar tipo de proyecto (Software/SaaS vs Rol/Agente)

2. **Mostrar al usuario lo que se detecto**:
   - "Encontre un proyecto [tipo] con [stack]. Voy a crear la estructura de Claude para el."
   - Pedir confirmacion antes de continuar

3. **Crear los archivos faltantes**:
   - `context/` — crear carpeta si no existe
   - `memory.md` — crear con template vacio
   - `tasks/todo.md` — crear con template, poblar con tareas pendientes detectadas (TODOs en codigo, issues, etc.)
   - `claude.md` — generar con la info detectada + entrevista reducida (solo preguntar lo que NO se pudo inferir del codigo)

4. **Registrar puertos** (solo para Software/SaaS):
   - Escanear archivos de config (`package.json`, `.env`, `docker-compose.yml`, etc.) para detectar puertos en uso
   - Consultar `~/.claude/ports.md` para verificar que no hay conflictos
   - Registrar los puertos del proyecto en `~/.claude/ports.md`
   - Si hay conflicto, avisar al usuario y sugerir puerto alternativo

5. **Mover contenido existente a context/** si aplica:
   - Si hay un README extenso con info de arquitectura → extraer a `context/tech-stack.md`
   - Si hay docs sueltos en la raiz → moverlos a `context/`
   - Si hay info de competidores, roadmap, etc. en cualquier archivo → sugerir extraer a archivos de contexto

5. Continuar con Fase 5 (Sugerir Archivos de Contexto) y luego Fase 6 (Permisos y Skills).

---

#### Fase 0c: Auditoria y Reformateo (ya tiene claude.md)

El proyecto ya tiene claude.md pero puede no seguir el formato del template. Hacer lo siguiente:

1. **Leer claude.md existente** y analizar:
   - Tiene las secciones del template? (Rol, Sobre el Proyecto, Tech Stack, Preferencias, Herramientas, Memoria, Contexto, Reglas)
   - Cuantas lineas tiene? (maximo recomendado: ~200)
   - Hay informacion que deberia estar en `context/` en lugar de claude.md?

2. **Mostrar diagnostico al usuario**:
   - "Tu claude.md tiene [X] lineas (recomendado: ~200)"
   - "Le faltan estas secciones: [lista]"
   - "Tiene [X] lineas de contenido que deberian ir en context/"
   - Pedir confirmacion antes de hacer cambios

3. **Reformatear claude.md**:
   - Reorganizar el contenido existente para que siga la estructura del template
   - NO borrar informacion — solo reestructurar y mover
   - Mantener el tono y estilo que ya tenia el usuario
   - Si pasa de ~200 lineas, extraer el exceso a archivos en `context/`:
     - Info detallada de tech stack → `context/tech-stack.md`
     - Descripciones largas de features → `context/features.md`
     - Reglas extensas → `context/rules-detail.md`
     - APIs e integraciones → `context/api-reference.md`
     - Cualquier otro bloque grande → `context/[nombre-descriptivo].md`
   - En claude.md, reemplazar el contenido movido con una referencia: "Ver detalle en context/[archivo].md"

4. **Crear archivos faltantes**:
   - Si no existe `memory.md` → crear con template vacio
   - Si no existe `tasks/todo.md` → crear con template, poblar con tareas pendientes si se detectan
   - Si no existe `context/` → crear carpeta

5. **Entrevista de huecos**: Solo preguntar por la informacion que falta en claude.md:
   - Si no tiene seccion de Rol → preguntar
   - Si no tiene Tech Stack → preguntar (o inferir del codigo)
   - Si no tiene Preferencias → preguntar
   - NO preguntar por cosas que ya estan cubiertas

6. Continuar con Fase 5 (Sugerir Archivos de Contexto) y luego Fase 6 (Permisos y Skills).

---

### Fase 1: Clasificacion del Proyecto

Solo se ejecuta para proyectos nuevos (Resultado A de Fase 0). Preguntar al usuario:

1. **Tipo de proyecto** — Determinar si es:
   - **Software/SaaS**: Aplicacion, plataforma, bot, API, herramienta tecnica
   - **Rol/Agente**: Departamento virtual (Executive Assistant, Head of Marketing, Content Team, CFO, etc.)

2. **Nombre del proyecto** — Nombre corto y descriptivo (ej: "ObraKit", "Executive Assistant", "Content Team")

3. **Ubicacion** — Siempre preguntar donde crear la carpeta. Sugerir el directorio actual si aplica.

### Fase 2: Crear Estructura de Carpetas

Crear la siguiente estructura en la ubicacion indicada:

```
NombreProyecto/
├── claude.md          (instrucciones del proyecto/rol)
├── memory.md          (template vacio — se llena automaticamente)
├── tasks/
│   └── todo.md        (tareas del proyecto — persiste entre sesiones)
└── context/           (documentos de referencia del proyecto)
```

Usar el template de `references/memory-template.md` para generar memory.md.
Usar el template de `references/todo-template.md` para generar tasks/todo.md.

### Fase 3: Entrevista para claude.md

Ejecutar una entrevista estilo conversacional para recopilar la informacion necesaria. Hacer las preguntas en bloques de 2-3 para no abrumar al usuario.

#### Para proyectos SOFTWARE/SaaS:

**Bloque 1 — Identidad:**
- Que hace este proyecto en una oracion?
- Quien es el usuario objetivo?
- Cual es el modelo de negocio (SaaS, marketplace, freemium, etc.)?

**Bloque 2 — Tecnologia:**
- Cual es el tech stack? (frontend, backend, base de datos, hosting)
- Que herramientas de desarrollo usas? (IDE, CI/CD, monitoreo)
- Hay integraciones clave? (APIs externas, servicios terceros)
- Que puertos necesita este proyecto? (frontend, backend, DB, etc.) — Consultar `~/.claude/ports.md` para evitar conflictos y registrar los nuevos

**Bloque 3 — Preferencias de trabajo:**
- Que tono prefieres en las respuestas? (tecnico, casual, directo)
- Hay convenciones de codigo o patrones que sigues?
- Que nivel de autonomia quieres que tenga el agente?

**Bloque 4 — Contexto adicional:**
- Hay competidores o referencias que deba conocer?
- Cual es la prioridad actual del proyecto? (MVP, escalar, refactorizar, etc.)
- Algo mas que deba saber para ser efectivo?

#### Para proyectos ROL/AGENTE:

**Bloque 1 — El rol:**
- Cual es el rol de este agente? (ej: "Eres mi asistente ejecutivo...")
- Cuales son sus responsabilidades principales?
- A quien sirve este agente? (a ti directamente, a un equipo, a clientes)

**Bloque 2 — Comunicacion:**
- Que tono debe usar? (formal, casual, profesional pero amigable)
- En que idioma(s) debe comunicarse?
- Hay frases, firmas o formatos que debe usar siempre?

**Bloque 3 — Herramientas y procesos:**
- Que herramientas usa este rol? (Gmail, Calendar, Notion, Slack, etc.)
- Hay procesos recurrentes que debe conocer?
- Que informacion necesita acceder regularmente?

**Bloque 4 — Limites y preferencias:**
- Que NO debe hacer este agente?
- Hay decisiones que siempre debe consultar antes de tomar?
- Algo mas que el agente necesite saber?

### Fase 4: Generar claude.md

Con las respuestas de la entrevista, generar el archivo claude.md usando la estructura del template en `references/claude-template-software.md` o `references/claude-template-role.md` segun el tipo de proyecto.

**Regla critica**: Mantener claude.md en ~200 lineas maximo. Si hay mas contexto, va en la carpeta context/.

### Fase 5: Sugerir Archivos de Contexto

Basado en el tipo de proyecto, sugerir archivos para la carpeta context/:

#### Para SOFTWARE/SaaS:
- `tech-stack.md` — Detalle del stack tecnologico, versiones, decisiones de arquitectura
- `competitors.md` — Analisis de competencia y diferenciadores
- `user-personas.md` — Perfiles de usuarios objetivo
- `api-reference.md` — Endpoints, schemas, integraciones
- `roadmap.md` — Prioridades y features planeados

#### Para ROL/AGENTE:
- `about-me.md` — Informacion personal y profesional del usuario
- `brand-voice.md` — Tono de voz, estilo de comunicacion de la marca
- `ideal-customer-profile.md` — Perfil del cliente ideal
- `products-services.md` — Descripcion de productos/servicios
- `processes.md` — SOPs y procesos recurrentes del rol

Preguntar al usuario cuales quiere crear y ejecutar mini-entrevistas para poblar cada uno.

### Fase 6: Permisos y Skills Complementarios

Antes de cerrar, ofrecer al usuario configurar permisos y activar skills que complementan el proyecto.

#### 6a. Permisos Sugeridos

Preguntar: "Quieres que configure permisos comunes para no estar aprobando cada operacion manualmente?"

Si acepta, sugerir estos permisos segun el tipo de proyecto:

**Permisos base (todos los proyectos):**
- `Read`, `Edit`, `Write`, `Glob`, `Grep` — operaciones de archivos
- `Bash(git *)` — commits, branches, status
- `Bash(ls *)`, `Bash(mkdir *)` — navegacion basica

**Permisos adicionales para SOFTWARE/SaaS:**
- `Bash(npm *)`, `Bash(npx *)`, `Bash(pnpm *)`, `Bash(yarn *)`, `Bash(bun *)` — gestores de paquetes
- `Bash(node *)`, `Bash(python *)`, `Bash(python3 *)` — ejecucion de scripts
- `Bash(docker *)`, `Bash(docker-compose *)` — si usan contenedores

**Permisos adicionales para ROL/AGENTE:**
- Permisos de MCPs relevantes segun las herramientas del rol (Gmail, Calendar, etc.)

**Nunca auto-aprobar sin preguntar:**
- `Bash(rm *)`, `Bash(git push *)`, `Bash(git reset *)` — operaciones destructivas
- Cualquier comando que afecte sistemas externos o datos compartidos

#### 6b. Skills Complementarios

Presentar al usuario los skills que potencian el proyecto recien creado:

**Para TODOS los proyectos:**

| Skill | Que hace | Activacion |
|-------|----------|------------|
| `/self-correct` | Captura correcciones en `tasks/lessons.md` para no repetir errores | Automatico al corregir al agente |
| `/session-memory` | Guarda snapshots de sesion con decisiones, archivos, tareas pendientes. Restaura contexto en nueva sesion | Automatico inicio/fin de sesion |
| `/task-plan` | Gestiona tareas en `tasks/todo.md` para trabajo multi-paso | Cuando hay trabajo complejo |

**Solo para SOFTWARE/SaaS:**

| Skill | Que hace | Activacion |
|-------|----------|------------|
| `/tdd-workflow` | Test-driven development: RED, GREEN, IMPROVE. Minimo 80% coverage | Antes de implementar features |
| `/local-review` | Code review local antes de commit: bugs, seguridad, calidad | Antes de hacer commit |

**Como las piezas trabajan juntas:**
- `memory.md` = preferencias y estilo del usuario (curado, estable)
- `tasks/lessons.md` (self-correct) = errores especificos a evitar (operacional, crece con correcciones)
- `.session-memory/` (session-memory) = continuidad entre sesiones (temporal, snapshots de trabajo)

Preguntar al usuario cuales quiere activar. Si acepta session-memory, inicializarlo:
```bash
python3 scripts/session_manager.py init /path/to/project
```

### Fase 7: Confirmacion y Siguientes Pasos

Al terminar, mostrar un resumen de todo lo creado y sugerir:
1. Empezar a trabajar en el proyecto para que memory.md se llene naturalmente
2. Corregir al agente cuando se equivoque — self-correct capturara las lecciones en `tasks/lessons.md`
3. Las sesiones se guardaran automaticamente si session-memory esta activo
4. Crear skills para procesos repetitivos conforme aparezcan

## Resources

### references/
Templates para los archivos generados:
- `claude-template-software.md` — Template de claude.md para proyectos de software
- `claude-template-role.md` — Template de claude.md para roles/agentes
- `memory-template.md` — Template de memory.md (universal)
- `todo-template.md` — Template de tasks/todo.md (tracking de tareas entre sesiones)
