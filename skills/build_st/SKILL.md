---
name: build_st
description: Builds one refined story end to end from its HU_NN.md, with a single test checkpoint (one file, max 7 cases grouped by topic) and stops only for real blockers. Never commits.
disable-model-invocation: true
---

# Build story

Una HU completa por sesión. Se hereda la fórmula de `pair` —el test es la especificación, el
código mínimo que lo cumple y nunca se commitea— pero con pasos grandes: **una HU = un archivo de
test = una entrega**. No se para en cada caso del test.

## 1. Revisión

- Leer la historia (ruta `Backlog/<carpeta>/HU_NN.md` o el bloque de `/story`). Ese archivo es el
  insumo esperado: si no llega, pedirlo.
- Contrastar el plan con el código actual. Si algo ya no encaja, decirlo antes de empezar.
- Si no hay plan, proponer uno de 5 viñetas y esperar aprobación.

## 2. Test único

- Proponer **un solo archivo de test por HU**: nombre del archivo, dónde vive, cómo se corre y la
  lista de casos —**máximo 7 `it`**, agrupados por tema tocado, no uno por criterio.
- Los casos cubren lo principal de la HU distribuido por tema y son de **lógica pura**: reglas,
  cálculos, estados, decisiones y persistencia. La **UI se valida a mano**, salvo que la HU sea
  explícitamente de UI; aun así se prueba su lógica (qué pantalla toca, qué se guarda, qué estado
  cambia), nunca el render ni lo visual.
- Presentar la lista ya numerada y descrita: `#01` qué escenario contempla y qué garantiza, `#02`
  igual, hasta el último. Esa misma descripción va al código.
- Si la HU no entra en 7 casos, **avisar antes de escribir nada** y proponer una salida: un test
  e2e que recorra el flujo completo, o dividir la HU.
- Esperar aprobación. Es la única parada antes de tocar código; esa lista es la especificación.

## 3. Implementación de golpe

1. Escribir el archivo de test y correrlo: mostrar que falla (rojo) una sola vez.
2. Implementar toda la HU hasta verde, sin paradas intermedias y sin sumar casos al test.
3. Correr los tests y mostrar verde.

## 4. Entrega

Un único mensaje de cierre, con esta forma:

```
✅ <HU_NN> verde: 1 archivo, <n> casos, <n> temas.
Funciones creadas:
1. `<nombre>` — <para qué sirve>. (`archivo:línea`)
2. `<nombre>` — <para qué sirve>. (`archivo:línea`)
Manual: <qué hay que probar a mano, si queda algo>
Decidí: <juicio propio, si hubo>
¿Reviso contigo, ajusto algo o cierro?
```

- El listado de funciones va **ordenado** y solo con lo nuevo: nombre, para qué sirve y dónde vive.
- Cerrar con una sugerencia de mensaje de commit si es un punto bueno (funcionalidad y refactor en
  commits distintos). **Nunca commitear.**

## Parar solo si

- Aparece una decisión de diseño que no está en el plan.
- Se cuela algo que no se pidió, aunque parezca razonable.
- **Hay que tocar un test**, nuevo o existente: es obligación parar **antes** de tocarlo, avisar
  cuál, por qué y qué va a cambiar. Todo el trabajo se ve en lazygit: quedará registrado que se
  tocó un test, así que se avisa primero, nunca se ajusta en silencio.
- **Hay que tocar una funcionalidad preexistente**: evidenciarlo (qué hace hoy, quién depende de
  eso, qué se rompería), planear el cambio y mostrarlo para conversarlo antes de tocarlo.
- Dos intentos sin verde.

## Reglas de test

- El valor esperado sale del criterio de aceptación, **nunca** de la misma lógica que el código.
- Se prueba comportamiento por la interfaz pública, no detalles internos.
- **Lógica pura, no UI**: se testean reglas, cálculos, estados y persistencia. Lo que se ve, se
  toca o se lee en pantalla se valida a mano; solo una HU explícitamente de UI lleva tests de su
  lógica interna, y nunca de render.
- No se agrega ninguna librería de testing de UI si el proyecto no la tiene: si hace falta, se
  para y se conversa.
- Un archivo por HU y como máximo 7 `it`: si hace falta el octavo, sobra alcance; avisar.
- **Cada test va documentado** con una descripción encima, numerada desde `#01`, en lenguaje
  llano: qué escenario contempla y qué garantiza. El `it` queda corto; la explicación va en el
  comentario y sirve de documentación del archivo:

```js
// #01 Test — contempla que una tesorera abre la app por primera vez y no hay moneda
// elegida: la intro se muestra antes que cualquier otra pantalla.
it('muestra la intro en la primera apertura sin configurar', () => { ... })

// #02 Test — contempla que ya vio la intro: no aparece aunque reinicie la app.
it('no repite la intro cuando ya fue vista', () => { ... })
```

- La numeración es consecutiva dentro del archivo y coincide con la lista aprobada en el paso 2.
- Nunca modificar tests existentes para que pase el código nuevo: si hace falta, se para y se
  conversa (ver arriba).
