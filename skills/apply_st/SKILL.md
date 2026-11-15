---
name: apply_st
description: Saves the story approved in the conversation (story, acceptance criteria, plan, out of scope, suggestions) as Backlog/<carpeta-del-plan>/HU_NN.md, numbered as in the plan's backlog. Use right after refining a story with /story.
disable-model-invocation: true
---

# Apply story

Guarda la historia aprobada como `Backlog/<carpeta-del-plan>/HU_NN.md`. Una historia por archivo.

## Pasos

1. Tomar del hilo el bloque que el usuario aprobó (Story, Acceptance criteria, Plan, Out of scope,
   Suggestions). Si no hay aprobación explícita, decirlo y ofrecer `/story` en vez de inventarlo.
2. Localizar la carpeta: la `Backlog/<carpeta>/` del plan al que pertenece la historia (por el
   `Plan.md` citado en el hilo). Si hay más de una candidata, preguntar cuál. Si `Backlog/` no
   existe, decirlo y ofrecer `/apply_bckl`.
3. Numerar con la HU del `## Backlog` del plan: `HU1` → `HU_01.md`, `HU10` → `HU_10.md`. Si no se
   puede saber a qué HU corresponde, usar el siguiente número libre de la carpeta.
4. Si el archivo ya existe, preguntar si se reemplaza. Nunca sobrescribir sin preguntar.
5. Escribir el archivo con el formato de abajo, respetando la redacción aprobada.
6. Responder con la ruta creada y cuántos criterios de aceptación tiene.

## Formato

```markdown
# HU_01 — <título corto en una línea>

**Plan:** `Backlog/<carpeta>/Plan.md` · HU1
**Estado:** 🔲 Planificado

## Story
As a <actor>, I want <action>, so that <benefit>.

## Acceptance criteria
- [ ] Given <context>, when <action>, then <result>.
- [ ] ...

## Plan
- ...

## Out of scope
- ...

## Suggestions (your call)
- ...
```

## Reglas

- Una sola historia por archivo; si el hilo trae varias aprobadas, preguntar cuál guardar.
- Copiar el bloque aprobado tal cual: mismo idioma, mismos criterios y viñetas.
- `Estado` arranca en `🔲 Planificado`; no marcarlo como hecho.
- No tocar `Plan.md`, `AGENTS.md` ni ningún otro archivo.
- No escribir código ni agregar requisitos que no estén en el bloque aprobado.
