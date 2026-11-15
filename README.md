# ODD_BC

Paquete portátil de skills y comandos de OpenCode para llevar una idea desde el backlog hasta una
historia implementada y cerrada.

## Contenido

| Comando | Skill | Para qué sirve |
| --- | --- | --- |
| `/backlog` | `backlog` | Convierte una idea en un backlog de historias verticales. |
| `/apply_bckl` | `apply_bckl` | Guarda el plan acordado en `Backlog/<nombre>/Plan.md`. |
| `/story` | `story` | Refina una historia con criterios de aceptación y mini plan. |
| `/apply_st` | `apply_st` | Guarda la historia aprobada en `Backlog/<carpeta>/HU_NN.md`. |
| `/build_st` | `build_st` | Implementa la historia con un único checkpoint de tests. |
| `/end_st` | `end_st` | Valida, marca la historia y actualiza el estado del Plan. |

## Instalación global

Copia el contenido a la configuración de OpenCode del usuario:

- `commands/*.md` → `~/.config/opencode/commands/`
- `skills/<id>/SKILL.md` → `~/.config/opencode/skills/<id>/SKILL.md`

En Windows: `%USERPROFILE%\.config\opencode\`.

OpenCode recarga comandos y skills automáticamente; no hace falta reiniciar.

## Flujo recomendado

`/backlog` → `/apply_bckl` → `/story` → `/apply_st` → `/build_st` → `/end_st`
