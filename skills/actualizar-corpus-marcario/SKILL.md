---
name: actualizar-corpus-marcario
description: >
  Esta skill debe usarse cuando el usuario pida "buscar tesis nuevas de
  confusión de marcas", "actualiza el corpus con criterios recientes",
  "hay jurisprudencia nueva sobre semejanza en grado de confusión", o
  quiera verificar si la SCJN o el TFJA han emitido criterios aún no
  incluidos en el corpus empaquetado con este plugin. Skill de
  mantenimiento opcional: requiere un conector capaz de buscar en el
  Semanario Judicial de la Federación y/o el TFJA; degrada de forma
  controlada cuando no hay un conector así disponible.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Actualización del corpus de criterios sobre confusión marcaria

Propone adiciones al corpus empaquetado buscando criterios de la SCJN o del
TFJA emitidos después de la fecha de corte del corpus. Nunca modifiques
automáticamente el archivo empaquetado; propón siempre los cambios para que
el usuario los revise y apruebe.

## Formato de citación

Sigue el formato de citación definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md` al
presentar los hallazgos al usuario.

## Precondición

Esta skill necesita acceso en vivo a un conector de base de datos legal
capaz de buscar jurisprudencia mexicana (tesis, jurisprudencia, ejecutorias)
por palabra clave; por ejemplo, un conector que exponga herramientas como
`buscar_tesis`, `buscar_tesis_tfja`, `ver_tesis`, o equivalentes. Verifica
si dicha herramienta está disponible en el entorno actual antes de empezar.

Si no hay un conector disponible, dilo claramente, indica que esta skill no
puede ejecutarse sin él, y sugiere al usuario buscar manualmente en
https://sjf2.scjn.gob.mx o en el portal propio del TFJA, o conectar un
conector de investigación legal adecuado.

## Línea base actual del corpus

`${CLAUDE_PLUGIN_ROOT}/skills/actualizar-corpus-marcario/references/corpus_marcas_confusion.json` — revisa
`metadata.fecha_investigacion` (actualmente 2026-08-09) y
`metadata.total_criterios` (actualmente 50) antes de buscar, y busca
únicamente criterios emitidos en o después de esa fecha.

## Términos de búsqueda

Reutiliza los términos de búsqueda documentados en `metadata.marco_normativo`
y en la nota metodológica (`metadata.categorias`): similitud de marcas,
confusión de marcas, riesgo de confusión, signos distintivos, marcas
confundibles, elemento dominante, distintividad, imitación de marca,
consumidor promedio, artículo 90 fracciones XVI y XVII (LPI abrogada),
artículo 173 fracción XVIII (LFPPI vigente). Busca en el Pleno, la Primera
Sala, la Segunda Sala, los Tribunales Colegiados de Circuito y el TFJA.

## Manejo de resultados

Para cada criterio candidato encontrado:

1. Confirma que es posterior a la línea base del corpus y que no está ya
   presente (compara por `registro_digital`).
2. Extrae los mismos campos usados en los registros existentes del corpus:
   rubro, autoridad emisora, tipo y época, fecha, registro digital, enlace,
   resumen, y ya sea texto íntegro o hechos/criterio jurídico/
   justificación.
3. Propón a qué categoría existente (A-N) pertenece, o propón una nueva
   categoría si ninguna encaja.
4. Presenta el o los nuevos registros propuestos al usuario con la misma
   estructura JSON que el corpus existente, y pide confirmación explícita
   antes de escribirlos en todas las copias de `corpus_marcas_confusion.json`
   empaquetadas en este plugin (una por skill, dentro de cada carpeta
   `skills/*/references/`; mantenlas idénticas). No sobrescribas los
   registros existentes; solo agrega nuevos.

## Después de una actualización aprobada

Incrementa `metadata.total_criterios` y `metadata.fecha_investigacion` en
el archivo JSON, y advierte al usuario que la versión del version.json o
del manifiesto del plugin también debería incrementarse (patch o minor) si
tiene intención de redistribuir el plugin actualizado.
