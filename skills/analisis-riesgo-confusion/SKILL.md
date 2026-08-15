---
name: analisis-riesgo-confusion
description: >
  Esta skill debe usarse cuando el usuario pida "analizar el riesgo de
  confusión entre dos marcas", "comparar estas marcas", "hay confundibilidad
  entre X y Y", "dictaminar si una marca puede registrarse frente a otra",
  "opinión sobre semejanza en grado de confusión", o proporcione dos marcas
  (marca registrada/previa vs. marca propuesta/posterior) con sus productos
  o servicios y pregunte si el registro es viable conforme al derecho
  marcario mexicano (LFPPI / LPI abrogada). Cubre oposiciones, acciones de
  nulidad, opiniones de libertad de registro y respuestas a oficios del
  IMPI sobre semejanza en grado de confusión.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Análisis de riesgo de confusión entre marcas (derecho mexicano)

Produce un análisis legal estructurado y citable sobre si dos marcas son
"idénticas o semejantes en grado de confusión" conforme al derecho
mexicano, aplicando la doctrina sistematizada en el corpus empaquetado de
50 criterios de la SCJN y del TFJA.

## Formato de citación

Sigue el formato de citación (artículos de la LFPPI y jurisprudencia)
definido en `${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`.

## Fuente de datos

Lee el corpus completo antes de analizar: `${CLAUDE_PLUGIN_ROOT}/skills/analisis-riesgo-confusion/references/corpus_marcas_confusion.json`.

El archivo tiene dos claves de primer nivel: `metadata` (categorías A-N,
marco normativo, conclusiones y lineamientos) y `criterios` (arreglo de 50
registros, cada uno con `id`, `rubro`, `categoria_codigo`,
`autoridad_emisora`, `tipo_y_epoca`, `fecha`, `registro_digital`, `enlace`,
`articulos`, `palabras_clave`, `resumen`, y ya sea `texto_integro` o
`hechos`/`criterio_juridico`/`justificacion`. Filtra y cita a partir de
este archivo; no inventes criterios ni números de registro digital. Si
algún ángulo necesario no está cubierto por el corpus, dilo explícitamente
en lugar de fabricar una cita.

## Información a recabar antes de analizar

Si el usuario no la ha proporcionado ya, pide:

1. La marca previa/registrada (o la que se opone) y la marca propuesta/
   posterior: denominación exacta, y si alguna es mixta (denominativa +
   diseño) o puramente nominativa.
2. Los productos o servicios que ampara cada marca (idealmente con la
   clase de Niza), y si están dirigidos a un consumidor general o a uno
   especializado/técnico.
3. Si la misma persona o entidad es titular de ambas marcas (activa la
   doctrina de la "excepción del mismo titular", categoría L), lo que
   cambia sustancialmente el análisis.
4. Si el caso se rige por la LPI abrogada (art. 90, fracción XVI) o por la
   LFPPI vigente (art. 173, fracción XVIII); infiérelo de la fecha de
   presentación si el usuario no lo especifica: la LFPPI está en vigor
   desde el 5 de noviembre de 2020.

No te detengas por detalles faltantes que no cambien el resultado; procede
con supuestos razonables y señálalos.

## Marco analítico

Aplica la doctrina en este orden, citando el `id`/`registro_digital`
específico que respalde cada paso (toma los criterios de las categorías B,
C, D, E, F, G, H, I, J, K, L, M, N según corresponda):

1. **Encuadre normativo.** Indica el artículo aplicable (90 fr. XVI LPI o
   173 fr. XVIII LFPPI) y, si está en juego la nulidad, el art. 258 fr. IV
   LFPPI.
2. **Comparación de los signos en su conjunto** (doctrina de las categorías
   E/H): apreciación de conjunto, no fraccionada; imagen imperfecta que
   conserva el consumidor promedio; identificación del elemento dominante,
   especialmente en marcas mixtas (categoría G). Si una marca es puramente
   nominativa y la otra es mixta sin elemento gráfico dominante en la
   marca previa, debe privilegiarse la comparación fonética.
3. **Aspectos fonético, gráfico e ideológico/conceptual** (categoría I):
   analiza cada uno de forma independiente y después de forma integral.
4. **Fuerza distintiva del signo previo** (categoría D): ¿es arbitraria/de
   fantasía, evocativa, descriptiva-débil, o construida con términos de
   uso común? Las marcas débiles tienen un ámbito de protección más
   estrecho y su titular debe tolerar una coexistencia más cercana.
5. **Los ocho factores objetivos de similitud entre productos/servicios**
   (categoría B/C): naturaleza, destino, utilización, carácter de
   competidor o intercambiable, carácter complementario, público de
   referencia, canales de distribución, origen habitual. Señala el
   principio de interdependencia: una menor similitud entre productos
   puede compensarse con una mayor similitud entre signos, y viceversa
   (regla de proporcionalidad inversa, categoría C). Indica expresamente si
   los productos pertenecen a clases distintas y, en su caso, que esto por
   sí solo no excluye la confusión.
6. **Tipo de consumidor** (categoría F): general/promedio vs. técnicamente
   especializado. Un consumidor especializado eleva el umbral para
   encontrar confusión; cita la línea de criterios SYLK/SILK cuando sea
   relevante.
7. **Notoriedad**, si alguna marca pudiera calificar como notoriamente
   conocida (categoría J); la notoriedad amplía la protección más allá de
   la clase registrada.
8. **Excepción del mismo titular**, si aplica (categoría L): interpretación
   estricta, no se extiende a grupos corporativos ni a licenciatarios sin
   que el mismo titular registral presente la solicitud.
9. **Otros impedimentos distintos de la confusión** (categoría M): señala
   si el problema real es el riesgo de engaño sobre el origen empresarial
   (art. 173 fr. XV) o sobre la naturaleza/cualidades del producto, ya que
   estos requieren un análisis distinto y no deben confundirse con el
   análisis de confusión.

## Formato de salida

Entrega, en español, usando prosa con subtítulos claros (no listas densas
de viñetas), salvo que el usuario pida una tabla:

- **Conclusión** (1-2 oraciones: existe / no existe / es dudoso el riesgo
  de confusión, y por qué).
- **Fundamento legal** (artículo(s) aplicable(s), citados con su texto).
- **Análisis** organizado conforme al marco anterior, citando cada
  criterio de apoyo siguiendo el formato de `citas-legales-marcario`.
- **Riesgos y contraargumentos**: la posición contraria más sólida que
  podría plantear la contraparte, y qué criterio la respaldaría.
- **Advertencia de vigencia**: señala que este es un análisis doctrinal
  basado en un corpus curado, vigente al 9 de agosto de 2026, que los
  criterios pueden haber sido superados, y que el usuario debe verificar la
  vigencia actual en la fuente oficial SJF2 (https://sjf2.scjn.gob.mx) o
  del TFJA antes de presentar el escrito.

Este resultado es un borrador de análisis legal profesional, no una
opinión legal definitiva; preséntalo como un documento de trabajo para
revisión del abogado, no como asesoría definitiva a un cliente.
