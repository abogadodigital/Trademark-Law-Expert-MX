# Trademark Law Expert - MX

Plugin de propiedad industrial mexicana enfocado en marcas registradas (ley
y jurisprudencia). Empaqueta un corpus curado de 50 tesis, jurisprudencias
y precedentes de la Suprema Corte de Justicia de la Nación (SCJN) y del
Tribunal Federal de Justicia Administrativa (TFJA), más ocho skills que lo
convierten en una herramienta de trabajo para litigantes de marcas,
asesores de propiedad intelectual y en material de apoyo docente para
profesores y alumnos de propiedad intelectual.

Autor: Joel A. Gómez Treviño ([Lex Informática | Abogados e
Ingenieros](https://lexinformatica.mx) · [Abogado Digital](https://lnk.bio/AbogadoDigital)
· Escuela de Derecho Digital).

## Componentes

| Skill | Uso |
|---|---|
| `consulta-lfppi-marcas` | Responde qué dice el texto vigente de la LFPPI (Título Cuarto, arts. 170-263) sobre marcas, avisos y nombres comerciales, citando el artículo/fracción/inciso exacto. |
| `consulta-infracciones-delitos-marcas` | Responde qué dice la LFPPI sobre infracciones administrativas y delitos en materia de marcas (Título Séptimo, arts. 386-406), incluyendo sanciones, multas, indemnización y las penas del delito de falsificación de marca, citando el artículo/fracción exacto. |
| `analisis-riesgo-confusion` | Recibe dos marcas y sus productos/servicios y produce un análisis fundado de riesgo de confusión, citando los criterios aplicables. |
| `busqueda-criterios-marcarios` | Localiza y cita criterios (tesis o jurisprudencia) del corpus por tema, artículo, número de registro digital o palabra clave. |
| `redaccion-escritos-marcarios` | Redacta el capítulo de fundamento y argumentación de oposiciones, contestaciones, recursos o demandas de nulidad. |
| `material-docente-marcas` | Genera resúmenes temáticos, casos prácticos, reactivos de examen y flashcards para docencia. |
| `actualizar-corpus-marcario` | Skill de mantenimiento (opcional): busca criterios nuevos vía un conector de investigación jurídica, si está disponible, y propone altas al corpus para aprobación del usuario. |
| `citas-legales-marcario` | Define el formato único y obligatorio de citación de tesis, jurisprudencia y artículos de la LFPPI que usan las demás skills de este plugin. |

## Instalación

Este repositorio es, a la vez, el plugin y su propio marketplace (trae
`.claude-plugin/marketplace.json`). Para instalarlo:

1. Desde Claude Code, Claude Desktop o Cowork, agrega el marketplace:
   ```
   /plugin marketplace add abogadodigital/Trademark-Law-Expert-MX
   ```
2. Instala el plugin:
   ```
   /plugin install trademark-law-expert-mx@trademark-law-expert-mx
   ```
3. Si la instalación reporta "Run /reload-plugins to activate.", corre:
   ```
   /reload-plugins
   ```

En la app de escritorio (sin usar comandos de terminal), usa el botón
**+** junto al cuadro de mensaje → **Plugins** → **Add plugin**, y pega la
liga de este repositorio o `abogadodigital/Trademark-Law-Expert-MX`.

## Cómo usar

El plugin no requiere comandos especiales. Una vez instalado en Claude Code
o en Claude Desktop (Cowork), cada skill se activa sola cuando el prompt
del usuario coincide con su propósito; no hace falta invocarla por nombre.
Algunos ejemplos de prompts, agrupados por skill:

**`consulta-lfppi-marcas`** (texto vigente de la ley)
- "¿Qué dice el artículo 173 de la LFPPI sobre semejanza en grado de
  confusión?"
- "¿Cuáles son los signos no registrables como marca?"
- "¿Cómo se regula la marca colectiva en la LFPPI?"

**`consulta-infracciones-delitos-marcas`** (sanciones y delitos)
- "¿Qué sanción tiene usar una marca registrada sin autorización de su
  titular?"
- "¿Cuáles son las penas por falsificación de marca conforme a la
  LFPPI?"
- "¿Cómo se calcula la indemnización por infracción a una marca
  registrada?"
- "¿En qué casos se persigue de oficio el delito de falsificación de
  marca?"

**`analisis-riesgo-confusion`** (comparación de dos marcas)
- "Analiza el riesgo de confusión entre la marca 'SOLERA' para vinos
  (clase 33) y 'SOLERO' para restaurantes (clase 43)."
- "¿Es viable registrar 'NEXTIA' para software si ya existe 'NEXIA'
  registrada en la misma clase?"

**`busqueda-criterios-marcarios`** (jurisprudencia y tesis)
- "Busca tesis sobre marcas mixtas y semejanza en grado de confusión."
- "Cita el criterio del registro digital [número]."
- "¿Qué dice la jurisprudencia sobre la excepción del mismo titular?"

**`redaccion-escritos-marcarios`** (borradores procesales)
- "Redacta el capítulo de fundamento jurídico para una oposición contra
  el registro de la marca 'X', citando semejanza fonética con mi marca
  registrada 'Y'."
- "Prepara los argumentos para contestar un oficio de IMPI que cita
  semejanza en grado de confusión."

**`material-docente-marcas`** (docencia)
- "Hazme un resumen temático de los factores de similitud entre marcas
  para mi clase de propiedad intelectual."
- "Genera 10 reactivos de opción múltiple sobre semejanza en grado de
  confusión conforme a la LFPPI."

**`actualizar-corpus-marcario`** (mantenimiento, opcional)
- "¿Hay jurisprudencia nueva sobre confusión de marcas que no esté en el
  corpus?"
- Solo funciona si el usuario tiene conectado un conector de investigación
  jurídica con acceso al Semanario Judicial de la Federación o al TFJA;
  sin ese conector, el resto del plugin sigue funcionando de forma
  totalmente offline.

Todo lo que producen las skills son borradores de trabajo: deben revisarse
por un abogado antes de usarse en un procedimiento real (ver "Alcance y
limitaciones" abajo).

## Datos

El plugin empaqueta tres corpus, todos funcionan sin conexión a ningún
conector externo:

- `data/corpus_marcas_confusion.json`: corpus de jurisprudencia. Incluye
  `metadata` (título, fuente, épocas consultadas, mapa de 14 categorías
  temáticas A-N, marco normativo — LPI abrogada / LFPPI vigente — y
  conclusiones con referencias cruzadas entre criterios) y `criterios[]`
  (50 registros, cada uno con rubro, autoridad emisora, tipo y época,
  fecha, registro digital, enlace oficial al SJF2 o al TFJA, artículos
  aplicables, palabras clave, resumen, y texto íntegro o el esquema
  Hechos / Criterio jurídico / Justificación). Investigación con corte al
  9 de agosto de 2026.
- `data/corpus_lfppi_marcas.json`: corpus normativo con el texto íntegro
  vigente del Título Cuarto de la LFPPI ("De las Marcas, Avisos y Nombres
  Comerciales", arts. 170 a 263, incluyendo 229 Bis y 257 Bis), tomado de
  un documento de trabajo del usuario (última reforma reflejada: DOF
  03-04-2026). Incluye `metadata` (capítulos I-VIII con su artículo
  inicial, fuente, vigencia) y `articulos[]` (96 registros, cada uno con
  número, capítulo, fracciones/incisos estructurados y el `texto_completo`
  verbatim del artículo). Lo consume la skill `consulta-lfppi-marcas`.
- `data/corpus_lfppi_infracciones_delitos.json`: corpus normativo con el
  Título Séptimo de la LFPPI ("De las Infracciones, Sanciones
  Administrativas y Delitos", arts. 386 a 406), filtrado a lo relacionado
  con marcas, avisos comerciales, nombres comerciales, denominaciones de
  origen e indicaciones geográficas, más las disposiciones generales de
  sanciones, multas, indemnización y procedimiento aplicables a cualquier
  infracción o delito (última reforma reflejada: DOF 03-04-2026). Incluye
  `metadata` (con una `nota_alcance` que documenta qué fracciones se
  excluyeron por ser de patentes o secretos industriales) y `articulos[]`
  (21 registros), cada uno etiquetado con `materia`
  (`marca` / `denominacion_origen` / `general`) para distinguir qué es
  núcleo de marcas y qué es transversal. Lo consume la skill
  `consulta-infracciones-delitos-marcas`.

La skill `actualizar-corpus-marcario` permite mantener vigente el corpus de
jurisprudencia si el usuario cuenta con un conector de investigación
jurídica con herramientas de búsqueda de tesis y jurisprudencia. El corpus
normativo (`corpus_lfppi_marcas.json`) se actualiza manualmente
reemplazando el archivo cuando haya una reforma relevante.

## Configuración

No requiere variables de entorno ni servidores MCP propios. La skill de
actualización es opcional y solo se activa si el entorno del usuario ya
tiene conectado un conector de búsqueda de jurisprudencia mexicana; si no lo
tiene, el resto del plugin funciona igual de forma completamente offline.

## Alcance y limitaciones

- El corpus de jurisprudencia cubre exclusivamente la doctrina de
  semejanza/similitud en grado de confusión entre marcas (art. 90,
  fracción XVI, de la LPI abrogada y su equivalente, art. 173, fracción
  XVIII, de la LFPPI vigente), más los impedimentos y excepciones
  directamente relacionados (excepción del mismo titular, riesgo de
  engaño sobre origen empresarial, nulidad por error o diferencia de
  apreciación).
- El corpus normativo (`corpus_lfppi_marcas.json`) cubre únicamente el
  Título Cuarto de la LFPPI (marcas, avisos y nombres comerciales); no
  incluye otros títulos de la ley (patentes, modelos de utilidad, diseños
  industriales, secretos industriales, procedimientos administrativos
  generales, etc.). Es un documento de trabajo del usuario, no una fuente
  oficial en tiempo real: ante cualquier duda sobre reformas posteriores a
  la reflejada en `metadata.ultima_reforma`, debe verificarse el texto
  vigente en el DOF (https://www.dof.gob.mx).
- El corpus de infracciones y delitos (`corpus_lfppi_infracciones_delitos.json`)
  es un subconjunto filtrado del Título Séptimo: se excluyeron las
  fracciones del artículo 386 relativas a patentes, modelos de utilidad,
  diseños industriales, esquemas de trazado y secretos industriales, así
  como las fracciones del artículo 402 sobre secretos industriales, por no
  ser materia de marcas. Igual que el corpus del Título Cuarto, es un
  documento de trabajo del usuario y debe cotejarse contra el texto
  vigente en el DOF ante cualquier reforma posterior a la reflejada en
  `metadata.ultima_reforma`.
- Todo lo que producen las skills son borradores de trabajo para revisión de
  un abogado, no opiniones legales definitivas ni sustituto de la consulta
  directa a la fuente oficial (https://sjf2.scjn.gob.mx y el portal del
  TFJA).
- No se incluye información de clientes ni de casos reales del despacho del
  autor; el corpus se limita a criterios judiciales y administrativos de
  acceso público.

## Licencia

Creative Commons Atribución-NoComercial-CompartirIgual 4.0 Internacional
(CC BY-NC-SA 4.0). Uso no comercial con atribución; las obras derivadas
deben compartirse bajo la misma licencia. Para el texto completo, ver
[LICENSE.md](LICENSE.md). Para autorizaciones de uso comercial, contactar
a Joel A. Gómez Treviño (joelgomez@abogado.digital).
