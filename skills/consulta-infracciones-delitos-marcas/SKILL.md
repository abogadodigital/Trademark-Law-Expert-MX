---
name: consulta-infracciones-delitos-marcas
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué sanción tiene
  [conducta] con una marca", "qué es una infracción administrativa en
  materia de marcas", "cuáles son las penas por falsificación de marca",
  "qué dice el artículo [número, entre 386 y 406] de la LFPPI", "cómo se
  calcula la indemnización por infracción a una marca", "en qué casos se
  persigue de oficio el delito de falsificación de marca", "qué multa
  impone el IMPI por usar una marca sin autorización", o cuando necesite el
  texto literal de cualquier disposición del Título Séptimo (De las
  Infracciones, Sanciones Administrativas y Delitos) de la Ley Federal de
  Protección a la Propiedad Industrial (LFPPI) aplicable a marcas, avisos
  comerciales, nombres comerciales, denominaciones de origen o indicaciones
  geográficas, a diferencia del derecho marcario sustantivo (registrabilidad,
  titularidad, licencias) o de la jurisprudencia sobre semejanza en grado de
  confusión.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Consulta de infracciones administrativas y delitos en materia de marcas (LFPPI)

Responde dudas sobre infracciones administrativas, sanciones, indemnización
y delitos previstos en el Título Séptimo de la LFPPI ("De las Infracciones,
Sanciones Administrativas y Delitos", arts. 386 a 406), citando siempre el
texto legal exacto contenido en el corpus empaquetado. No parafrasees el
artículo como si fuera la única fuente de verdad sin antes mostrar o citar
su texto íntegro; no inventes artículos, fracciones o sanciones que no
existan en el corpus.

## Formato de citación

Sigue el formato de citación (artículos de la LFPPI y jurisprudencia)
definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`.

## Alcance del corpus (importante)

Este corpus **no es el Título Séptimo completo**. Es un subconjunto
filtrado a lo relacionado con marcas, avisos comerciales, nombres
comerciales, denominaciones de origen e indicaciones geográficas, más las
disposiciones generales de sanciones y procedimiento que aplican a
cualquier infracción o delito de propiedad industrial. Quedaron fuera del
corpus, por no ser materia de marcas:

- Artículo 386, fracciones IV a XV (infracciones de patentes, modelos de
  utilidad, diseños industriales y esquemas de trazado) y fracción XXXIII
  (cláusula genérica de cierre, "las demás violaciones...").
- Artículo 402, fracciones III a VI (delitos de secretos industriales).

Si el usuario pregunta específicamente por infracciones o delitos de
patentes, modelos de utilidad, diseños industriales, esquemas de trazado o
secretos industriales, dile explícitamente que esos supuestos existen en
la LFPPI pero no están incluidos en este corpus (acotado a marcas), y
sugiere verificar el texto vigente en el DOF.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-infracciones-delitos-marcas/references/corpus_lfppi_infracciones_delitos.json`

Estructura:

- `metadata`: título y nombre del Título Séptimo, fuente (DOF), fecha de
  publicación original, última reforma reflejada en el corpus,
  `nota_alcance` (documenta exactamente qué fracciones se excluyeron y por
  qué — cítala si el usuario pregunta por qué falta algo), lista de
  `capitulos` (I: infracciones y sanciones administrativas; II: delitos) y
  `leyenda_materia` (explica los valores posibles del campo `materia`).
- `articulos[]`: 21 registros (arts. 386-406), cada uno con:
  - `numero`: número de artículo (p. ej. `"386"`, `"402"`).
  - `capitulo_codigo` / `capitulo_titulo`: capítulo del Título Séptimo al
    que pertenece (I o II).
  - `materia`: `"marca"`, `"denominacion_origen"` o `"general"` (o
    `"mixto"` cuando el artículo mezcla fracciones de distinta materia,
    como el 386 y el 402). Úsalo para advertir al usuario cuándo una
    disposición es exclusiva de marcas y cuándo es transversal a toda la
    propiedad industrial.
  - `texto_intro`: primera oración del artículo, antes de las fracciones.
  - `fracciones[]`: cada una con `numero` (romano, p. ej. `"XVII"`),
    `materia` (mismo criterio que arriba, a nivel de fracción) y `texto`
    completo de la fracción (incluye, cuando aplica, los incisos a)/b)/c)
    integrados en el mismo texto, p. ej. fracción II del art. 386).
  - `parrafos_finales[]`: párrafos de cierre que aplican al artículo
    completo (p. ej. reglas de querella vs. persecución de oficio en el
    art. 402, o las reglas de reincidencia del art. 390).
  - `texto_completo`: el artículo íntegro, verbatim (dentro del alcance
    filtrado), incluyendo una nota entre paréntesis cuando el artículo
    tuvo fracciones excluidas por no ser materia de marcas. **Usa siempre
    este campo cuando cites o reproduzcas el texto legal.**

## Estrategia de búsqueda

Empareja la pregunta del usuario, en este orden de precedencia:

1. Número de artículo exacto (`numero`).
2. Tipo de conducta o pregunta:
   - **Infracciones administrativas de marcas** (qué conductas están
     prohibidas): art. 386, fracciones XVI-XXVIII (marcas, avisos y
     nombres comerciales) y XXIX-XXXII (denominación de origen/indicación
     geográfica), más las fracciones generales I-III (competencia
     desleal, confusión/engaño, desprestigio).
   - **Sanciones administrativas y su cálculo**: arts. 388 (tipos de
     sanción: multa, multa adicional, clausura), 390 (reincidencia), 392
     (criterios para individualizar la sanción), 393-394 (ejecución de
     multas como créditos fiscales).
   - **Indemnización por daños y perjuicios**: arts. 395-399 (cuantía
     mínima del 40%, indicadores de valor legítimo, procedimiento
     incidental, prescripción de 2 años).
   - **Delitos**: art. 402 (falsificación de marca, fracciones I-II;
     denominación de origen/indicación geográfica, fracciones VII-VIII),
     art. 403 (penas: 3 a 10 años y multa), art. 404 (delito específico de
     venta ambulante de mercancía falsificada: 2 a 6 años), art. 405
     (dictamen técnico previo del IMPI para el ejercicio de la acción
     penal en los delitos de marcas), art. 406 (reparación del daño,
     remite al art. 396).
3. Búsqueda de texto libre sobre `texto_intro`, `fracciones[].texto` y
   `parrafos_finales` cuando el usuario describe un supuesto sin dar
   número de artículo (p. ej. "vendo en la calle playeras con marcas
   falsificadas, ¿qué riesgo penal tengo?" → arts. 402 fracc. II, 403 y,
   sobre todo, 404).

Si la pregunta involucra si una conducta constituye o no una infracción de
fondo (por ejemplo, si dos marcas son confundibles), complementa la
respuesta remitiendo a las skills `consulta-lfppi-marcas` (derechos
sustantivos, Título Cuarto) o `analisis-riesgo-confusion` /
`busqueda-criterios-marcarios` (jurisprudencia) de este mismo plugin — este
skill responde la consecuencia jurídica (sanción/pena), no si la conducta
de fondo se actualiza.

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y, si es relevante, la
   fracción exacta, reproduciendo el texto de `texto_completo` o de la
   fracción específica entre comillas o en bloque de cita.
2. Distingue expresamente si se trata de una **infracción administrativa**
   (competencia del IMPI, sanciones: multa/clausura, art. 388) o de un
   **delito** (competencia penal, vía Ministerio Público y, en su caso,
   dictamen técnico previo del IMPI conforme al art. 405).
3. Si la pregunta es sobre indemnización, aclara que puede reclamarse ante
   el IMPI (una vez declarada la infracción) o directamente ante los
   Tribunales (art. 396), y que la cuantía mínima es el 40% del indicador
   de valor legítimo.
4. Da una explicación breve en lenguaje llano después de la cita textual,
   no en lugar de ella.
5. Si el usuario pide fundamento para un escrito, denuncia o querella, usa
   el formato de `citas-legales-marcario` (sección 2: `Artículo [número]
   (LFPPI): [texto completo]`).

## Límites

- Este corpus es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real. Si el usuario necesita certeza absoluta sobre
  reformas recientes (después de la última reforma reflejada en
  `metadata.ultima_reforma`), sugiere verificar el texto vigente en el
  portal del DOF (https://www.dof.gob.mx) o en la Cámara de Diputados
  (https://www.diputados.gob.mx/LeyesBiblio/).
- Recuerda siempre el filtro de alcance descrito arriba: si la pregunta cae
  en una fracción excluida (patentes, modelos de utilidad, diseños
  industriales, esquemas de trazado o secretos industriales), dilo
  explícitamente en vez de guardar silencio sobre la limitación.
- No es una opinión legal definitiva ni sustituto de asesoría penal o
  administrativa especializada; los borradores que produzcas (denuncias,
  querellas, escritos de reclamación de daños) requieren revisión de un
  abogado antes de presentarse ante el IMPI, el Ministerio Público o los
  Tribunales.
