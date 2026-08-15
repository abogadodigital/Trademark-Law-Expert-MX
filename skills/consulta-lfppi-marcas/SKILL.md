---
name: consulta-lfppi-marcas
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué dice el artículo
  [número] de la LFPPI", "qué dice la ley sobre marcas notoriamente
  conocidas / avisos comerciales / nombres comerciales / licencias /
  nulidad de registro", "cuáles son los signos no registrables como
  marca", "cuánto dura el registro de una marca", "cómo se regula la marca
  colectiva o de certificación", o cuando necesite el texto literal de
  cualquier disposición del Título Cuarto (De las Marcas, Avisos y Nombres
  Comerciales) de la Ley Federal de Protección a la Propiedad Industrial
  (LFPPI), arts. 170 a 263, a diferencia de la jurisprudencia que
  interpreta esas disposiciones.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Consulta del texto de la LFPPI sobre marcas, avisos y nombres comerciales

Responde dudas sobre el contenido literal del Título Cuarto de la LFPPI
("De las Marcas, Avisos y Nombres Comerciales", arts. 170 a 263, incluyendo
229 Bis y 257 Bis) citando siempre el texto legal exacto contenido en el
corpus empaquetado. No parafrasees el artículo como si fuera la única
fuente de verdad sin antes mostrar o citar su texto íntegro; no inventes
artículos, fracciones o incisos que no existan en el corpus.

## Formato de citación

Sigue el formato de citación (artículos de la LFPPI y jurisprudencia)
definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-lfppi-marcas/references/corpus_lfppi_marcas.json`

Estructura:

- `metadata`: título y nombre del Título Cuarto, fuente (DOF), fecha de
  publicación original, última reforma reflejada en el corpus, lista de
  `capitulos` (I a VIII, con su título y artículo inicial), rango de
  artículos cubiertos, y `relacion_con_corpus_jurisprudencial` (explica
  cómo se conecta este corpus normativo con el corpus de jurisprudencia
  del plugin, `data/corpus_marcas_confusion.json`).
- `articulos[]`: 96 registros, cada uno con:
  - `numero`: número de artículo (p. ej. `"173"`, `"229 Bis"`).
  - `capitulo_codigo` / `capitulo_titulo`: capítulo del Título Cuarto al
    que pertenece.
  - `texto_intro`: primera oración del artículo (antes de fracciones, si
    las tiene).
  - `fracciones[]`: cada una con `numero` (romano, p. ej. `"XVI"`, `"I Bis"`),
    `texto`, `incisos[]` (`letra` + `texto`) y `notas[]` (párrafos que
    cierran esa fracción específica, p. ej. excepciones que solo aplican a
    ella).
  - `parrafos_finales[]`: párrafos de cierre que aplican al artículo
    completo o hacen referencia cruzada a varias fracciones a la vez
    (detectados porque el texto original dice "fracciones" en plural).
  - `reformas[]`: anotaciones de reforma/adición/derogación tal como
    aparecen en el texto vigente (p. ej. "Fracción reformada y recorrida
    DOF 03-04-2026"), útiles para advertir al usuario que esa porción fue
    modificada recientemente.
  - `texto_completo`: el artículo íntegro, verbatim, en el orden original
    del documento fuente (intro + fracciones + incisos + notas + párrafos
    finales + anotaciones de reforma). **Usa siempre este campo cuando
    cites o reproduzcas el texto legal** — los campos estructurados
    (`fracciones`, `incisos`, `notas`, `parrafos_finales`) son un índice de
    apoyo para localizar y filtrar contenido, no un sustituto de la cita
    literal.

## Estrategia de búsqueda

Empareja la pregunta del usuario, en este orden de precedencia:

1. Número de artículo exacto (`numero`), incluyendo variantes "Bis"
   (p. ej. "229 Bis").
2. Capítulo temático (`capitulo_codigo`/`capitulo_titulo`) cuando el
   usuario pregunta por un tema general:
   - I: De las Marcas (arts. 170-178) — qué es una marca, signos
     registrables, impedimentos de registro (art. 173), vigencia de 10
     años.
   - II: De las Marcas Colectivas y de Certificación (arts. 179-189).
   - III: De las Marcas Notoriamente Conocidas y Famosas (arts. 190-199).
   - IV: De los Avisos Comerciales (arts. 200-205).
   - V: De los Nombres Comerciales (arts. 206-213).
   - VI: Del Registro de Marcas (arts. 214-238) — procedimiento ante el
     IMPI, oposición, declaratoria de uso real y efectivo.
   - VII: De las Licencias y Transmisión de Derechos (arts. 239-257 Bis).
   - VIII: De la Nulidad, Caducidad y Cancelación de Registros
     (arts. 258-263).
3. Búsqueda de texto libre sobre `texto_intro`, `fracciones[].texto`,
   `fracciones[].incisos[].texto` y `parrafos_finales` cuando el usuario
   describe un supuesto sin dar número de artículo (p. ej. "¿puedo
   registrar un olor como marca?", "¿puede una persona física registrar
   marcas de certificación?").

Si la pregunta también involucra semejanza en grado de confusión entre
marcas, jurisprudencia o tesis, complementa la respuesta remitiendo al
usuario a las skills `busqueda-criterios-marcarios` o
`analisis-riesgo-confusion` de este mismo plugin, que consultan
`data/corpus_marcas_confusion.json`.

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y, si es relevante,
   la fracción/inciso exacto, reproduciendo el texto de `texto_completo`
   entre comillas o en bloque de cita.
2. Si el artículo tiene entradas en `reformas[]`, adviértelo brevemente
   (p. ej. "esta fracción fue reformada por DOF 03-04-2026; verifica que
   no exista una reforma posterior antes de usarla en un escrito").
3. Da una explicación breve en lenguaje llano de lo que dice el artículo,
   después de la cita textual, no en lugar de ella.
4. Si el usuario pide fundamento para un escrito o dictamen, usa el
   formato de `citas-legales-marcario` (sección 2: `Artículo [número]
   (LFPPI): [texto completo]`).

## Límites

- Este corpus es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real. Si el usuario necesita certeza absoluta sobre
  reformas recientes (después de la última reforma reflejada en
  `metadata.ultima_reforma`), sugiere verificar el texto vigente en el
  portal del DOF (https://www.dof.gob.mx) o en la Cámara de Diputados
  (https://www.diputados.gob.mx/LeyesBiblio/).
- No mezcles el texto legal con jurisprudencia sin distinguir claramente
  cuál es cuál: el texto de este corpus es la norma; los criterios de
  `corpus_marcas_confusion.json` son interpretación judicial/administrativa
  de esa norma.
- No es una opinión legal definitiva; los borradores que produzcas
  requieren revisión de un abogado antes de usarse.
