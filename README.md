# ODD_BC

Flujo de trabajo con agentes de IA para programar de forma **semi-orgánica**: buena planificación,
implementación flexible y revisión de código real, con la velocidad que hoy exigen las empresas.

ODD Modificado no es waterfall ni "vibe coding". Es un punto medio: tú decides, el agente propone e
implementa, y cada avance queda documentado y revisable en el repo.

## Qué es ODD Modificado

Una adaptación de ODD (Organic Driven Development) pensada para trabajar con agentes de IA en el día
a día:

- **Planificación que se puede revisar.** La idea se convierte en un backlog de historias verticales
  y el plan se guarda como Markdown dentro del repo. Nada vive solo en el chat.
- **Implementación flexible.** Cada historia se refina justo antes de construirla, con un mini plan
  que se contrasta contra el código actual. El agente implementa de golpe hasta verde, con un único
  checkpoint de tests, y solo se detiene ante bloqueos reales.
- **Revisión de código como cierre.** Antes de dar una historia por terminada se valida que los
  tests sigan intactos, que no haya regresiones ni bugs sueltos y que el alcance se haya respetado.
  El agente nunca commitea: deja el diff listo para que lo revises.

El resultado: avances rápidos sin perder trazabilidad, control ni calidad del código.

## Cuándo usarlo

- Quieres moverte rápido con un agente de IA sin renunciar a la revisión de código.
- Necesitas que la planificación quede escrita y versionada, no dispersa en conversaciones.
- Trabajas en historias pequeñas y verticales que entregan valor por sí solas.
- Prefieres decidir tú y que el agente proponga, implemente y se detenga cuando hay que conversar.

## A tu manera

Siéntete libre de usar estas skills como mejor te funcione. Están pensadas para **OpenCode**, pero
no están atadas a él: puedes usar el flujo completo, solo algunas skills, en otro orden, o adaptar
los textos a tu equipo y a tu agente. La intención es darte una base sólida, no un dogma.

## Contenido

| Comando | Skill | Fase | Para qué sirve |
| --- | --- | --- | --- |
| `/backlog` | `backlog` | Planificación | Convierte una idea en un backlog de historias verticales. |
| `/apply_bckl` | `apply_bckl` | Planificación | Guarda el plan acordado en `Backlog/<nombre>/Plan.md`. |
| `/story` | `story` | Refinamiento | Refina una historia con criterios de aceptación y mini plan. |
| `/apply_st` | `apply_st` | Refinamiento | Guarda la historia aprobada en `Backlog/<carpeta>/HU_NN.md`. |
| `/build_st` | `build_st` | Implementación | Implementa la historia con un único checkpoint de tests. |
| `/end_st` | `end_st` | Revisión | Valida, marca la historia y actualiza el estado del Plan. |

## Flujo recomendado

```
/backlog → /apply_bckl → /story → /apply_st → /build_st → /end_st
```

1. **Planificar.** `/backlog` ordena y corta la idea en historias verticales. `/apply_bckl` deja el
   plan en el repo.
2. **Refinar.** `/story` toma una sola historia, propone 2–3 criterios de aceptación y un mini plan
   de 5 viñetas. `/apply_st` guarda la historia aprobada.
3. **Implementar.** `/build_st` escribe un único archivo de test por historia (máximo 7 casos,
   agrupados por tema), lo ve fallar una vez e implementa toda la historia hasta verde.
4. **Revisar.** `/end_st` recorre el diff, valida tests intactos, regresiones, bugs y alcance, marca
   los checkboxes verificados y actualiza el estado del Plan. Nunca commitea.

## Artefactos en el repo

```
Backlog/
└── <nombre-del-plan>/
    ├── Plan.md      # Contexto, decisiones, estado de implementación y backlog
    └── HU_01.md     # Una historia por archivo: story, criterios, plan y out of scope
```

El estado del plan y de cada historia se mantiene actualizado a medida que avanzas, así que el repo
siempre refleja qué está planificado, en curso e implementado.

## Instalación

### OpenCode (recomendado)

Copia el contenido a la configuración del usuario:

- `commands/*.md` → `~/.config/opencode/commands/`
- `skills/<id>/SKILL.md` → `~/.config/opencode/skills/<id>/SKILL.md`

En Windows: `%USERPROFILE%\.config\opencode\`.

OpenCode recarga comandos y skills automáticamente; no hace falta reiniciar.

También puedes instalarlo por proyecto, dentro del repo, para que el flujo viaje con el código:

- `commands/*.md` → `.opencode/commands/`
- `skills/<id>/SKILL.md` → `.opencode/skills/<id>/SKILL.md`

### Claude Code

El formato es compatible en lo esencial: Markdown con frontmatter YAML y comandos con
`$ARGUMENTS`.

- `skills/<id>/SKILL.md` → `~/.claude/skills/<id>/SKILL.md` (global) o
  `.claude/skills/<id>/SKILL.md` (proyecto).
- `commands/*.md` → `~/.claude/commands/` (global) o `.claude/commands/` (proyecto).

### Otros agentes y editores

Cursor, Windsurf, Copilot, Zed y similares no comparten exactamente el mismo formato, pero la
lógica se traslada sin problema: el cuerpo de cada `SKILL.md` es Markdown, así que puedes pegarlo
como regla o prompt reutilizable, y los comandos como prompts o snippets. El flujo —planificar,
refinar, implementar, revisar— es el mismo.

La recomendación es simple: instálalo donde trabajes a diario y ajústalo a tu manera.

