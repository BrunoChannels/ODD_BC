---
name: apply_bckl
description: Saves the plan agreed in the conversation as Backlog/<nombre-descriptivo>/Plan.md inside the repo, creating the folder if missing. Use when the user wants to persist a backlog or plan as a Markdown document.
disable-model-invocation: true
---

# Apply backlog

Guarda el plan acordado en la conversación como `Backlog/<nombre-descriptivo>/Plan.md`.

## Pasos

1. Raíz del repo = directorio de trabajo. Buscar `Backlog/` sin distinguir mayúsculas; si no
   existe, crearla con esa grafía.
2. Elegir un nombre descriptivo en kebab-case español (2–4 palabras, sin acentos) a partir del
   título del plan. Si esa carpeta ya existe, preguntar si se actualiza su `Plan.md` o se usa
   otro nombre. Nunca sobrescribir sin preguntar.
3. Escribir `Plan.md` con exactamente estas secciones, en este orden:

```markdown
# <Título en una línea>

## Context

<2–4 líneas: qué es y para quién; stack; decisiones caras que aplican>

## Decisiones acordadas

- **<tema>**: <decisión tomada>
- **<tema>**: <decisión tomada>

## Estado de implementación

**🔲 Planificado.** Ninguna historia implementada.

## Backlog

- [ ] **HU1** — Como <actor>, quiero <acción>, para <beneficio>.
- [ ] **HU2** — Como <actor>, quiero <acción>, para <beneficio>. _(Requires: #1)_
```

4. Responder con la ruta creada y cuántas HU quedaron.

## Reglas

- Solo dividir lo que el usuario dijo; no inventar requisitos, criterios de aceptación ni
  estimaciones.
- Conservar la redacción acordada de cada historia; numerar HU1..n en el orden del plan.
- Checkbox siempre (`- [ ]` o `- [x]`); `_(Requires: #N)_` solo donde se acordó.
- Si en la conversación hay más de un plan, preguntar cuál guardar.
- Si todavía no hay un plan acordado, decirlo y ofrecer `/backlog` en vez de inventarlo.
- Al actualizar un plan existente: marcar `[x]` las HU terminadas y reescribir solo la sección
  "Estado de implementación" (puede llevar subsecciones con lo implementado, archivos
  principales y verificación).
- No tocar `AGENTS.md` ni ningún otro archivo.
