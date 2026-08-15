---
name: citas-legales-marcario
description: >
  Esta skill define el formato obligatorio para citar tesis,
  jurisprudencia (SCJN o TFJA) y artículos de la LFPPI en cualquier
  respuesta de este plugin. Las demás skills de este plugin
  (busqueda-criterios-marcarios, consulta-lfppi-marcas,
  consulta-infracciones-delitos-marcas, analisis-riesgo-confusion,
  redaccion-escritos-marcarios, material-docente-marcas) deben
  consultarla cada vez que citen un criterio judicial/administrativo o un
  artículo de la LFPPI, en vez de describir su propio formato. También
  úsala cuando el usuario pregunte directamente "cómo citas la
  jurisprudencia", "cuál es el formato de citas de este plugin" o
  equivalente.
metadata:
  version: "0.1.0"
  author: "Joel Alejandro Gómez Treviño"
---

# Formato de citación

Todas las demás skills de este plugin que citen jurisprudencia, tesis o
artículos de la LFPPI deben seguir exactamente las reglas de este
documento. Ninguna otra skill debe describir su propio formato de
citación en prosa ni inventar variantes: solo debe remitir aquí
(`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-marcario/SKILL.md`).

## 1. Citación de jurisprudencia y tesis (SCJN o TFJA)

### 1.1 Cuántos resultados dicta qué formato

- **1 a 4 criterios** → formato completo (sección 1.2). Es obligatorio
  siempre que la consulta arroje entre 1 y 4 resultados, sin excepción —
  nunca lo sustituyas por el formato abreviado solo porque el contenido
  del registro es extenso.
- **5 o más criterios** → formato abreviado (sección 1.3).

### 1.2 Formato completo (1 a 4 criterios)

Para cada criterio, en este orden, cada etiqueta en su propia línea, sin
fusionar dos etiquetas en un mismo renglón:

```
[TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA, el `rubro` tal cual del corpus]
Autoridad emisora: [autoridad_emisora] (Ejemplo: Pleno de la Suprema Corte de Justicia de la Nación, o Pleno del TFJA)
Tipo y época: [tipo_y_epoca] (Ejemplo: Jurisprudencia, Duodécima Época)
Fecha: [fecha, formato DD/MM/AAAA]
Registro digital: [registro_digital]
Enlace: [enlace] (SJF2, p. ej. https://sjf2.scjn.gob.mx/detalle/tesis/2032298, o el portal del TFJA, según corresponda)
Resumen: [redacta un texto breve que resuma los hechos, el criterio jurídico y la justificación; puedes apoyarte en el campo `resumen` del corpus]

- Contenido de la tesis -
Hechos: [copia los hechos en su totalidad]
Criterio jurídico: [copia el criterio jurídico en su totalidad]
Justificación: [copia la justificación en su totalidad]
```

Si el registro del corpus no tiene la estructura Hechos/Criterio
jurídico/Justificación sino un campo `texto_integro` (tesis de
estructura tradicional en bloque único), sustituye el bloque
"- Contenido de la tesis -" por el `texto_integro` completo, sin
parafrasear ni resumir la regla legal operativa. Si un registro no trae
alguno de los tres campos, omite esa línea específica y conserva las
demás.

No omitas ninguna etiqueta (Autoridad emisora, Tipo y época, Fecha,
Registro digital, Enlace, Resumen) aunque el dato parezca obvio por el
contexto. Nunca uses etiquetas distintas a las de esta plantilla.

### 1.3 Formato abreviado (5 o más criterios)

Numera cada criterio por orden de aparición y usa las mismas etiquetas
de la sección 1.2, sin el bloque de "Contenido de la tesis":

```
[N]. [TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA]
Autoridad emisora: [autoridad_emisora]
Tipo y época: [tipo_y_epoca]
Fecha: [fecha]
Registro digital: [registro_digital]
Enlace: [enlace]
Resumen: [el campo `resumen` del corpus, sin parafrasear]
```

No incluyas `hechos`/`criterio_juridico`/`justificacion`/`texto_integro`
en esta lista abreviada. Al final de la lista, pregunta al usuario si
quiere conocer el contenido completo de alguna tesis, pidiéndole que la
identifique **por orden de aparición** ("¿quieres que te muestre el
contenido de la primera, la segunda, la tercera...?"), no por número de
registro digital. Cuando el usuario responda, entrega ese criterio en el
formato completo de la sección 1.2.

### 1.4 Excepción expresa

Si el usuario pide explícitamente solo el título y el enlace (p. ej.
"solo dame los títulos y el link"), respeta esa instrucción y omite el
resto de las etiquetas, sin perder el título ni el enlace oficial.

## 2. Citación de artículos de la LFPPI

Cada vez que cites un artículo de la Ley Federal de Protección a la
Propiedad Industrial, usa este formato:

```
Artículo [número] (LFPPI): [texto completo del artículo, incluyendo
todos sus párrafos, fracciones e incisos]
```

Ejemplo: `Artículo 173 (LFPPI): [texto_completo del art. 173]`.

Nunca cites solo el número de artículo sin su texto completo, ni
parafrasees el texto legal — reprodúcelo tal cual aparece en el campo
`texto_completo` del corpus normativo correspondiente
(`corpus_lfppi_marcas.json` o
`corpus_lfppi_infracciones_delitos.json`, según el artículo). Si el
artículo citado pertenece a la LPI abrogada (p. ej. art. 90, aplicable a
hechos anteriores a la LFPPI), identifícalo expresamente como "(LPI
abrogada)" en vez de "(LFPPI)".

## 3. Fuente de la cita: el corpus empaquetado

Cada criterio que cites proviene del corpus integrado con este plugin
(`corpus_marcas_confusion.json`), curado a partir de fuentes oficiales
(SJF2 y TFJA). Al citar un criterio, la fuente que reportas al usuario es
siempre ese corpus y el `enlace` oficial de verificación que trae cada
registro — esa es la referencia correcta y suficiente; no hace falta
añadir explicaciones sobre cómo se integró el corpus ni de dónde salió
originalmente cada dato.

Todas las skills de este plugin que citan jurisprudencia trabajan contra
este corpus ya integrado. La única excepción es `actualizar-corpus-marcario`,
que sí puede consultar un conector de investigación jurídica en vivo, pero
solo cuando el usuario se lo pida expresamente y ese conector esté
disponible en el entorno — y únicamente para proponer altas nuevas al
corpus, no para responder una consulta normal.

## 4. Regla general

Ninguna otra skill de este plugin debe reimplementar ni parafrasear
estas reglas: deben remitir a este documento para el formato exacto de
citación, tanto de jurisprudencia como de artículos de la LFPPI.
