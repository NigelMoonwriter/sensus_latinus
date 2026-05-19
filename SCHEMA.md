# SCHEMA

## Objetivo
Definir un esquema base común para todos los diccionarios de ENTORNO GREKA, preservando extensiones específicas por corpus.

## Super-schema base
```json
{
  "id": "string-obligatorio",
  "project": "latinus|graecus|nepantla|semannsis",
  "title": "string-obligatorio",
  "type": "string-obligatorio",
  "lang": "string-opcional",
  "summary": "string-obligatorio",
  "body": "string-obligatorio",
  "tags": ["string"],
  "themes": ["string"],
  "related": ["string"],
  "sources": [
    {
      "title": "string",
      "author": "string",
      "kind": "primary|secondary|editorial|internal",
      "url": "string-opcional"
    }
  ],
  "level": "base|expanded|manifesto",
  "flags": {
    "reviewed": true,
    "aria_ready": false,
    "utf8_checked": true
  }
}
```

## Extensiones por diccionario

### sensus_latinus
- `lemma`
- `ipa`
- `etym`
- `evo`
- `deriv`
- `cogn`
- `example`
- `cmp`

### sensus_graecus
- `lemma`
- `translit`
- `defs`
- `researchNotes`
- `relatedEntries`
- `famousPhrases`
- `negativeTheologyTags`

### sensus_nepantla
- `num`
- `month`
- `phrase`
- `caption`
- `hashtags`
- `color`
- `line`
- `thesis`
- `theorists`

### sensus_semannsis
- `num`
- `greek` o `term`
- `translit` cuando aplique
- `cardinal`
- `def`
- `ref`
- `source`

## Reglas de consistencia
- `id` debe ser único por entrada.
- `title` debe ser el nombre principal visible de la entrada.
- `summary` debe corresponder a la definición breve.
- `body` debe corresponder a la reflexión principal.
- `sources` debe normalizar fuentes, aunque el render final conserve un string simplificado.
- `related` debe permitir cruces entre diccionarios.

## Ejemplo mínimo para SEMANNSIS
```json
{
  "id": "semannsis-061-protoestesia",
  "project": "semannsis",
  "title": "Protoestesia",
  "type": "spanish",
  "lang": "es",
  "summary": "Sentir antes de saber.",
  "body": "A veces el cuerpo se adelanta a la mente.",
  "tags": ["conciencia", "percepción", "hibridación"],
  "themes": ["sur"],
  "related": ["graecus-aisthesis"],
  "sources": [
    {
      "title": "Reflejos Híbridos",
      "author": "Entorno Greka",
      "kind": "internal"
    }
  ],
  "level": "base",
  "flags": {
    "reviewed": true,
    "aria_ready": true,
    "utf8_checked": true
  },
  "num": 61,
  "term": "Protoestesia",
  "cardinal": "sur",
  "def": "Sentir antes de saber.",
  "ref": "El cuerpo se adelanta a la interpretación.",
  "source": "Concepto original — Reflejos Híbridos"
}
```
