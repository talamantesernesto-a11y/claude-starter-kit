# Template: tasks/todo.md

Este archivo se crea con la estructura base y se pobla durante la entrevista inicial o escaneando el proyecto existente. Se actualiza continuamente conforme se trabaja.

```markdown
# Tareas del Proyecto

> Este archivo se actualiza automaticamente conforme se trabaja. Marca tareas como completadas cuando terminen. Al iniciar una nueva sesion, revisa este archivo para saber donde te quedaste.

## En Progreso
- [ ] [Tarea que se esta trabajando actualmente]

## Pendientes
- [ ] [Siguiente tarea prioritaria]
- [ ] [Tarea futura]

## Completadas
- [x] [YYYY-MM-DD] Proyecto inicializado con estructura Claude (claude.md, memory.md, context/, tasks/)
```

## Reglas de uso

1. **Al iniciar sesion**: Leer este archivo para entender donde se quedo el trabajo
2. **Durante la sesion**: Marcar tareas como completadas conforme se terminan, agregar nuevas conforme surjan
3. **Al cerrar sesion**: Asegurarse de que refleja el estado actual — que esta en progreso, que sigue
4. **Formato de completadas**: Incluir fecha `[YYYY-MM-DD]` al marcar como completada para tener historial
5. **No acumular**: Mover tareas completadas viejas (>30 dias) a un archivo `tasks/archive.md` si el archivo crece mucho
