---
name: redaccion-escritos-marcarios
description: >
  Esta skill debe usarse cuando el usuario pida "redactar una oposición al
  registro de marca", "redacta el escrito de nulidad", "prepara los
  argumentos para responder un oficio de IMPI sobre semejanza en grado de
  confusión", "arma el capítulo de fundamento jurídico sobre
  confundibilidad marcaria", o necesite un borrador de argumentación legal
  (oposición, contestación, recurso de revisión, demanda de nulidad, o
  respuesta a oficio del IMPI) con base en la doctrina de confusión
  marcaria empaquetada con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Redacción de escritos sobre semejanza en grado de confusión

Redacta la o las secciones de argumentación legal de un escrito marcario
(oposición, respuesta a oficio, demanda de nulidad o recurso), con base en
la doctrina sistematizada en el corpus empaquetado. Esto produce un
borrador de trabajo para revisión del abogado, no un documento final listo
para presentarse.

## Formato de citación

Sigue el formato de citación (artículos de la LFPPI y jurisprudencia)
definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/redaccion-escritos-marcarios/references/corpus_marcas_confusion.json` — misma
estructura descrita en las demás skills de este plugin. Toma cada cita
legal de este archivo; nunca inventes un registro digital, un rubro o un
texto citado.

## Antes de redactar, establece

1. **Postura procesal**: oposición (art. 90 LFPPI), respuesta a oficio de
   la autoridad, recurso de revisión, juicio de nulidad ante el TFJA, o
   amparo. La postura determina el tono, la carga que se está atendiendo, y
   ante qué autoridad se dirige el escrito (IMPI vs. TFJA vs. tribunal
   colegiado).
2. **A qué parte representa el usuario**: opositor/actor (argumentando que
   existe confusión) o solicitante/demandado (argumentando que no existe, o
   que aplica una excepción, p. ej. el mismo titular bajo la categoría L o
   una marca previa débil/evocativa bajo la categoría D).
3. **Los hechos del caso**: las dos marcas, productos/servicios y clases,
   fechas de presentación, si alguna parte invoca la excepción del mismo
   titular, si alguna marca se reclama como notoriamente conocida.

Pregunta únicamente por lo que falte y sea relevante; no te detengas en
detalles procesales que el usuario ya haya proporcionado.

## Enfoque de redacción

Estructura la sección de argumentación así:

1. **Encuadre normativo**: cita textualmente el artículo aplicable (art. 90
   fr. XVI LPI / art. 173 fr. XVIII LFPPI / art. 258 fr. IV LFPPI / art. 173
   fr. XV LFPPI, según corresponda) con su referencia de publicación en el
   DOF/LFPPI tomada de `metadata.marco_normativo`.
2. **Doctrina aplicable**: expón el marco rector (apreciación de conjunto,
   elemento dominante, ocho factores objetivos, tipo de consumidor, fuerza
   distintiva) citando los criterios correspondientes, dando prioridad a
   las fuentes de mayor jerarquía disponibles en el corpus (Pleno/Salas
   antes que Tribunales Colegiados, conforme a
   `metadata.conclusiones_y_lineamientos`).
3. **Aplicación al caso concreto**: aplica cada elemento doctrinal a las
   marcas y productos reales en cuestión, construyendo el argumento del
   lado solicitado (existencia o inexistencia de confusión, procedencia o
   improcedencia de la excepción, etc.).
4. **Cierre**: la petición concreta (se niegue el registro, se declare la
   nulidad, se confirme la resolución impugnada, etc.), redactada para que
   el usuario la adapte al resto del escrito.

Redacta en español jurídico mexicano formal, en el registro usado en
escritos ante el IMPI/TFJA (tercera persona, "la promovente", "la parte
opositora", etc.), y marca claramente con `[ ]` cualquier dato pendiente
que el usuario deba completar (nombres de las partes, números de
expediente, fechas, anexos).

## Salvaguardas

- Esta es asistencia de redacción para un abogado con cédula profesional,
  no un sustituto del criterio profesional sobre estrategia de litigio.
- Señala cuando los hechos descritos sugieran un impedimento distinto al
  solicitado (p. ej., el usuario pide argumentar "confusión" pero los
  hechos describen riesgo de engaño sobre el origen, art. 173 fr. XV —
  categoría M), para que el borrador apunte a la teoría legal correcta.
- Cierra con un recordatorio de verificar la vigencia actual de cada
  criterio citado contra la fuente oficial SJF2/TFJA antes de presentar el
  escrito.
