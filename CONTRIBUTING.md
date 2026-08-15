# Contribuir a trademark-law-expert-mx

Gracias por tu interés en mejorar este plugin. Aquí van las pautas para
proponer cambios.

## Qué puedes aportar

- **Nuevos criterios (tesis/jurisprudencia).** Si conoces una tesis del
  Semanario Judicial de la Federación o del TFJA sobre semejanza en grado
  de confusión que no esté en `data/corpus_marcas_confusion.json`, abre un
  issue o un pull request con: número de registro digital, rubro, texto,
  órgano emisor, época e instancia. El skill
  `actualizar-corpus-marcario` está pensado justamente para este flujo.
- **Correcciones al texto de la LFPPI.** El corpus
  `data/corpus_lfppi_marcas.json` (Título Cuarto, arts. 170-263) debe
  reflejar el texto vigente publicado en el Diario Oficial de la
  Federación. Si detectas una reforma no incorporada, indica la fecha de
  publicación en el DOF y el artículo afectado.
- **Mejoras a los skills.** Cambios a la redacción, ejemplos o lógica de
  cualquier `SKILL.md` son bienvenidos, siempre que mantengan el formato
  de cita jurídica exigido (ley/artículo/fracción/inciso o
  registro digital de tesis).
- **Reporte de errores.** Cualquier cita incorrecta, artículo mal
  transcrito o comportamiento inesperado de un skill.

## Cómo proponer un cambio

1. Haz un fork del repositorio.
2. Crea una rama descriptiva (`fix/corpus-art-90`, `feat/nuevo-criterio-x`).
3. Si agregas o modificas un criterio o disposición legal, incluye la
   fuente oficial (enlace al DOF, al Semanario Judicial de la Federación o
   al portal del TFJA).
4. Verifica que el archivo `.claude-plugin/plugin.json` siga siendo JSON
   válido y que las referencias dentro de cada `SKILL.md` apunten a
   archivos existentes en `references/` o `data/`.
5. Abre un pull request explicando el cambio y su fundamento.

## Estándares de cita

Este plugin exige fundamento verificable en todo momento. No se aceptarán
criterios, artículos o citas sin fuente oficial identificable (DOF,
Semanario Judicial de la Federación, TFJA o Corte IDH, según aplique).

## Licencia

Al contribuir, aceptas que tu aportación se distribuya bajo la misma
licencia Creative Commons Atribución-NoComercial-CompartirIgual 4.0
Internacional (CC BY-NC-SA 4.0) de este proyecto (ver
[LICENSE.md](LICENSE.md)).

## Contacto

Joel A. Gómez Treviño — [Lex Informática | Abogados e Ingenieros](https://lexinformatica.mx) · [Abogado Digital](https://lnk.bio/AbogadoDigital)
