---
name: material-docente-marcas
description: >
  Esta skill debe usarse cuando el usuario pida "crear material de clase
  sobre confusión marcaria", "hazme un resumen temático para estudiantes",
  "genera reactivos de examen sobre semejanza en grado de confusión",
  "arma un caso práctico para la clase de marcas", "prepara flashcards
  sobre los factores de similitud", o de cualquier otra forma necesite
  material didáctico para un curso de derecho, taller o diplomado, con
  base en la doctrina de confusión marcaria empaquetada con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Material docente sobre semejanza en grado de confusión marcaria

Genera material de estudio para estudiantes de derecho o audiencias de
educación continua a partir del corpus empaquetado: resúmenes temáticos,
casos prácticos, reactivos de examen o flashcards.

## Formato de citación

Sigue el formato de citación (artículos de la LFPPI y jurisprudencia)
definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/material-docente-marcas/references/corpus_marcas_confusion.json` — lee
`metadata.categorias` para el mapa de las 14 categorías, `metadata.marco_normativo`
para el contexto normativo (LPI abrogada vs. LFPPI vigente), y
`criterios[]` para el material jurisprudencial de fondo. Fundamenta cada
ejemplo y cada regla citada en un registro real del corpus; cita el
`registro_digital` para que los estudiantes puedan consultar la fuente.

## Tipos de material que esta skill puede producir

**Resumen temático**: organizado por las 14 categorías (A-N), explicando la
regla doctrinal de cada una con uno o dos criterios ilustrativos por
categoría, partiendo del fundamento normativo (art. 90 LPI / 173 LFPPI)
hasta llegar a los refinamientos (marcas débiles, consumidor especializado,
marcas mixtas, notoriedad, excepción del mismo titular).

**Caso práctico**: toma los `hechos` de un criterio real (o combina
elementos de dos) y preséntalo como un supuesto hipotético para que los
estudiantes lo analicen, con la resolución real disponible como clave de
respuesta; no reveles la respuesta en el enunciado mismo.

**Reactivos de examen**: preguntas de opción múltiple, verdadero/falso o
abiertas que evalúen si el estudiante puede (a) identificar el artículo
aplicable, (b) aplicar los ocho factores objetivos, (c) distinguir la
confusión de los impedimentos adyacentes de la categoría M, o (d) enunciar
correctamente la regla de interpretación estricta de la excepción del
mismo titular. Si el plugin `profesoria-joel-gomez` o una skill/herramienta
equivalente de elaboración de exámenes está disponible en el entorno,
prefiere delegarle el formato del examen y usa esta skill solo para
proporcionar contenido doctrinalmente exacto y citas correctas.

**Flashcards / glosario**: pares breves de pregunta-respuesta por cada
concepto clave (elemento dominante, imagen de conjunto, consumidor
especializado, marca notoriamente conocida, excepción del mismo titular,
etc.) con el registro digital de respaldo.

## Estilo y nivel

Pregunta al usuario (si no lo ha especificado ya) el nivel académico y el
contexto: licenciatura, posgrado, diplomado, taller corporativo, y ajusta
la profundidad y el vocabulario en consecuencia, pero nunca suavices ni
omitas la cita legal: toda doctrina presentada a los estudiantes debe poder
rastrearse hasta un criterio específico del corpus.

## Entregable

Entrega contenido listo para incorporarse a una guía de estudio, una
presentación de diapositivas o un examen. Si el usuario está produciendo un
archivo (Word, PowerPoint, PDF), usa la skill de creación de documentos
correspondiente disponible en el entorno (docx, pptx, pdf) en lugar de
devolver solo texto plano en el chat.
