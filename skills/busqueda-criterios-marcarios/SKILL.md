---
name: busqueda-criterios-marcarios
description: >
  Esta skill debe usarse cuando el usuario pida "buscar tesis sobre
  confusión de marcas", "encuentra jurisprudencia sobre X" (marcas mixtas,
  consumidor especializado, marca notoriamente conocida, excepción del
  mismo titular, etc.), "cita el criterio del registro [número]", "qué
  dice la tesis sobre el artículo 90 fracción XVI / 173 fracción XVIII", o
  necesite localizar y citar correctamente uno o más de los 50 criterios
  de la SCJN/TFJA sobre semejanza en grado de confusión marcaria
  empaquetados con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Búsqueda y cita de criterios sobre confusión marcaria

Localiza el criterio o los criterios relevantes dentro del corpus
empaquetado y devuélvelos en formato de citación legal mexicana correcto.
No busques en internet ni inventes criterios: esta skill trabaja
exclusivamente contra el archivo empaquetado.

## Formato de citación (obligatorio — ver skill dedicada)

El formato exacto de citación (jurisprudencia completa/abreviada y
artículos de la LFPPI), así como la prohibición de atribuir el contenido
a cualquier conector o búsqueda en vivo, están definidos en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`. Esta
skill no repite esas reglas: consúltalas ahí y aplícalas al pie de la
letra cada vez que entregues un criterio de este corpus.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-marcarios/references/corpus_marcas_confusion.json`

Estructura: `metadata.categorias` (A-N con títulos), `metadata.marco_normativo`,
`metadata.conclusiones_y_lineamientos` (referencias cruzadas entre criterios
por registro digital), y `criterios[]`: 50 registros con `id`, `rubro`,
`categoria_codigo`/`categoria_titulo`, `autoridad_emisora`, `tipo_y_epoca`,
`fecha`, `registro_digital`, `enlace`, `articulos[]`, `palabras_clave[]`,
`resumen`, y `texto_integro` o `hechos`/`criterio_juridico`/`justificacion`.

## Estrategia de búsqueda

Empareja la solicitud del usuario, en este orden de precedencia:

1. `registro_digital` exacto, si se proporciona.
2. `categoria_codigo`/`categoria_titulo` si el usuario nombra un tema que
   corresponde a una de las 14 categorías (A: jerarquía superior; B:
   factores objetivos; C: productos de clases distintas; D: signos
   débiles/evocativos; E: funciones marcarias y criterios generales; F:
   consumidor promedio vs. especializado; G: marcas mixtas/isotipo; H:
   examen de novedad; I: similitud fonética; J: marcas notoriamente
   conocidas; K: competencia desleal/imagen comercial; L: excepción del
   mismo titular; M: otros impedimentos distintos de la confusión; N:
   criterios del TFJA).
3. `articulos[]` (p. ej., "artículo 90 fracción XVI", "173 fracción
   XVIII", "258 fracción IV").
4. `palabras_clave[]` y coincidencias de texto libre en `rubro` y
   `resumen`.

Lee `metadata.conclusiones_y_lineamientos` cuando el usuario haga una
pregunta sintética ("¿cuál es el criterio de mayor jerarquía sobre X?",
"¿cómo se relacionan estos criterios?"): esa sección ya mapea las
relaciones jerárquicas y temáticas entre registros.

Al presentar el formato abreviado de 5 o más criterios, agrupa la lista
por `categoria_codigo` y presenta primero la fuente de mayor jerarquía
(Pleno > Salas > Plenos de Circuito > Tribunales Colegiados > TFJA),
conforme a las notas de jerarquía en
`metadata.conclusiones_y_lineamientos`.

## Cuando no hay coincidencias

Si ningún registro del corpus responde la consulta, dilo claramente y
sugiere al usuario realizar una búsqueda en vivo en el Semanario Judicial
de la Federación oficial (https://sjf2.scjn.gob.mx) o en el TFJA, o, si
hay algún conector de búsqueda jurisprudencial disponible en este
entorno, ofrece usarlo directamente sin dar por hecho de cuál se trata.
Nunca fabriques un registro digital ni un rubro.

## Advertencia de vigencia

Señala siempre, al entregar una cita para uso en un escrito, que el corpus
está vigente al 9 de agosto de 2026 y que la vigencia debe confirmarse en
la fuente oficial antes de usarse.
