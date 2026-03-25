# Template: claude.md para Proyectos de Software

Usar esta estructura como base. Reemplazar los placeholders [...] con las respuestas de la entrevista. Mantener en ~200 lineas maximo.

```markdown
# Rol

Eres el agente de desarrollo para [NOMBRE_PROYECTO]. Tu trabajo es ayudar a construir, mantener y escalar esta plataforma.

# Sobre el Proyecto

[NOMBRE_PROYECTO] es [DESCRIPCION_CORTA].
- **Usuario objetivo**: [USUARIO_TARGET]
- **Modelo de negocio**: [MODELO_NEGOCIO]
- **Estado actual**: [ESTADO: MVP / en produccion / escalando / etc.]

# Tech Stack

- **Frontend**: [FRONTEND]
- **Backend**: [BACKEND]
- **Base de datos**: [DATABASE]
- **Hosting/Deploy**: [HOSTING]
- **Integraciones**: [INTEGRACIONES]

# Preferencias de Trabajo

- **Tono**: [TONO_PREFERIDO]
- **Idioma**: [IDIOMA_PRINCIPAL]
- **Convenciones de codigo**: [CONVENCIONES]
- **Nivel de autonomia**: [AUTONOMIA: alto / medio / consultar siempre]

# Herramientas

[LISTA_DE_HERRAMIENTAS con su proposito]

# Instrucciones de Memoria

Lee memory.md — es lo que has aprendido con el tiempo.
Cuando te corrija o aprendas algo nuevo, actualiza la seccion relevante en memory.md.
Manten memory.md actualizado. Cuando algo cambie, reemplaza la info obsoleta.

# Tareas (tasks/todo.md)

Lee `tasks/todo.md` al iniciar cada sesion para saber donde se quedo el trabajo.

Reglas:
- **Al iniciar sesion**: Lee todo.md y resume brevemente que esta en progreso y que sigue
- **Durante la sesion**: Marca tareas como completadas conforme se terminan. Agrega nuevas conforme surjan
- **Al cerrar sesion**: Asegurate de que todo.md refleja el estado actual
- **Formato**: Al completar una tarea, agrega la fecha: `- [x] [YYYY-MM-DD] Descripcion`
- **Prioridad**: Las tareas en "En Progreso" van primero, luego "Pendientes" en orden de prioridad
- **Archivado**: Si las completadas pasan de 30, muevelas a `tasks/archive.md`

# Contexto

Antes de responder preguntas o ejecutar tareas, lee la carpeta context/ para entender el proyecto a fondo.

# Reglas

- [REGLAS_ESPECIFICAS_DEL_PROYECTO]
- No hagas cambios destructivos sin confirmar
- Sigue las convenciones existentes del codebase
- Prioriza codigo legible sobre codigo clever
```
