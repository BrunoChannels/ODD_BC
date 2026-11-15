---
name: end_st
description: Cierra la historia recién implementada con build_st —valida tests intactos, regresiones, bugs y alcance—, marca los checkboxes de la HU y actualiza el estado de implementación del Plan. No commitea.
disable-model-invocation: true
---

# Cerrar historia

Vas a cerrar la historia que se acaba de implementar en esta sesión (con `build_st` o una skill
equivalente). Trabaja con calma y criterio: primero verificas, después decides, y solo si todo pasa
marcas el backlog. **Nunca commitees.** Nunca ajustes un test ni código para "hacer pasar" la
validación: si algo falla, lo reportas y te detienes.

## 0. Identifica la historia

- Revisa el contexto de esta sesión y localiza el archivo de la historia (habitualmente
  `Backlog/<carpeta>/HU_NN.md`) y su `Plan.md` hermano. Lee la historia completa (Story, criterios,
  Plan, Out of scope) y el Plan.
- Si el contexto no alcanza para saber cuál es, deduce la candidata desde el diff de git y
  **confírmala con el usuario antes de tocar nada**. No adivines ni marques otra historia.
- Respeta el formato real de cada archivo: puede usar `- [ ]`, `## Acceptance criteria` u otros
  títulos; adáptate sin reescribir su estructura.

## 1. Recorre lo implementado

- Mira `git status --short` y el diff completo, incluidos los archivos nuevos.
- Enumera qué se agregó y cambió, y mapéalo contra cada criterio de aceptación.
- Distingue: criterios cubiertos por código/tests, criterios visuales o manuales, y cualquier cosa
  fuera de alcance.

## 2. Valida las reglas

**a) Tests intactos.** Un archivo de test **nuevo** es lo esperado. Si un test preexistente aparece
modificado o eliminado y el usuario no lo aprobó explícitamente en esta sesión, detente: reporta
cuál, qué cambió y no marques nada. Comprueba también que el test nuevo no se haya retocado después
de ponerse en verde.

**b) Lógica adyacente intacta.** Identifica los módulos tocados y sus consumidores (imports, usos,
claves compartidas) y revisa que los flujos vecinos sigan coherentes. Detecta cómo corre el proyecto
sus verificaciones (revisa `package.json`, `AGENTS.md` o la documentación del repo) y ejecuta la
suite completa, el linter y, si se tocó el arranque, rutas o el bundle, también el build. Muestra la
evidencia.

**c) Sin bugs sueltos.** Lee el diff buscando condiciones de borde, estados de carga, claves de
traducción faltantes en todos los idiomas que use el proyecto, suscripciones sin limpiar, errores
silenciados, textos sin traducir y cambios de comportamiento no pedidos. Anota hallazgos; no
arregles nada por tu cuenta en este paso.

**d) Alcance respetado.** Confirma que no se coló nada del "Out of scope" de la historia.

## 3. Decide

- **Todo en verde** → sigue al paso 4.
- **Cualquier regla rota** → no marques checkboxes ni actualices estados. Entrega un informe breve
  con regla, evidencia (`archivo:línea`, comando), impacto y opciones, y pregunta cómo seguir.

## 4. Marca el backlog

**En la historia (`HU_NN.md`):**
- Marca con `- [x]` **solo** los criterios de aceptación que quedaron verificados. Los que dependan
  de una verificación manual (gestos, pantalla completa, aspecto visual) quedan sin marcar hasta
  probarlos.
- Actualiza la línea de estado (`**Estado:**`, si existe) a implementado, dejando claro si queda
  verificación manual.

**En el `Plan.md`:**
- Marca con `- [x]` únicamente la línea de esa historia en el Backlog. No toques las demás.
- **Actualiza siempre el estado de implementación** (sección tipo `## Estado de implementación`).
  Si no existe, créala justo antes del Backlog. Reconstruye su contenido desde el checklist del
  Backlog, sin inventar:
  - Ninguna historia marcada: `**🔲 Planificado.** Ninguna historia implementada.`
  - Algunas marcadas: `**🟡 En curso.** Implementadas: HU1, HU3. Pendientes: HU2, HU4–HU14.`
    (usa rangos con guion cuando sean consecutivas).
  - Todas marcadas: `**✅ Implementado.** Todas las historias del plan están implementadas.`
- No reescribas el texto de la historia ni el de otras secciones del Plan: solo checkboxes y
  estado.

## 5. Cierra

Un mensaje **muy breve**, cálido y útil:

- ✅ `HU_NN` validada y marcada.
- Dos o tres datos de importancia: qué quedó funcionando, verificaciones en verde, qué falta probar
  a mano y cualquier decisión que valga la pena recordar.
- Una sugerencia de mensaje de commit, sin commitear.

No cierres con una pregunta: termina con el resumen y la sugerencia de commit.
