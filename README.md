# SENSUS LATINUS

> *El lenguaje no es un inventario: es una geología del pensamiento.*

Un diccionario etimológico filosófico de latín y griego clásico, 27 entradas con raíces protoindoeuropeas, evolución fonética documentada paso a paso, derivados en cinco lenguas romances, cognados transversales, y tres niveles de lectura: Aficionado, Estudiante, Profesor.

Un solo archivo HTML. Sin servidor. Sin dependencias. Doble clic y funciona.

**[Ver en vivo](https://nigelmoonwriter.github.io/sensus_latinus/)**

---

## La posición

SENSUS LATINUS no es solo un diccionario: es una máquina de lectura. Nace como un HTML standalone, un solo archivo que contiene la forma de una web y la paciencia de una biblioteca, donde cada entrada no se limita a traducir una palabra, sino a mostrar su viaje: del protoindoeuropeo al latín, del latín al romance, de la raíz al concepto.

Aquí el lenguaje aparece como historia de transformaciones. Cada lema es una escena donde la filología deja de ser archivo muerto y se vuelve drama de sonido, memoria y uso. Las palabras cambian por desgaste, por prestigio, por contacto, por analogía; y en ese cambio revelan algo más que su origen: revelan la manera en que una cultura piensa el mundo.

El proyecto trabaja con una intuición filosófica simple y radical: nombrar es interpretar. Un diccionario, cuando está bien hecho, no solo explica vocablos; ordena una ontología mínima del habla. Por eso SENSUS LATINUS se acerca al latín y al griego como lenguas de herencia, pero también como laboratorios de pensamiento: *logos* no es solo "palabra", *physis* no es solo "naturaleza", *ethos* no es solo "costumbre". Son umbrales donde el significado se vuelve forma de vida.

---

## Contenido

### Inventario de entradas

| Lengua | Cantidad | Ejemplos |
|---|---|---|
| Latín | 21 | *aqua, canis, corpus, terra, pax, pacis, vox, vocis, ars, artis, deus* |
| Griego clásico | 6 | *logos, physis, ethos, pathos, gnosis, philosophia* |
| **Total** | **27** | |

### Niveles de lectura

Cada entrada se despliega en tres niveles de profundidad, accesibles mediante los botones Aficionado / Estudiante / Profesor:

- **Aficionado** — Definición clara, etimología accesible. Para quien se acerca por curiosidad.
- **Estudiante** — Añade derivados romances, cognados, comparación跨lenguas. Para quien estudia filología o lenguas clásicas.
- **Profesor** — Despliega la tabla completa de evolución fonética, comparación romance culto/vulgar, y notas filológicas. Para quien investiga o enseña.

### Distribución por nivel

| Nivel | Entradas |
|---|---|
| Básico | 12 (44%) |
| Intermedio | 13 (48%) |
| Avanzado | 2 (8%) |

### Temas

El diccionario organiza sus 27 entradas en 11 categorías temáticas:

| ID | Tema | Entradas |
|---|---|---|
| I | Conceptos y etimología | 2 |
| II | Español y romance | 19 |
| III | Fonética: vocales | 6 |
| V | Cambios fonéticos | 12 |
| VI | Declinaciones | 2 |
| IX | Griego: fonética | 6 |
| XI | Derivación griega | 6 |

---

## Arquitectura técnica

SENSUS LATINUS es un archivo HTML autónomo de 914 líneas que contiene:

```
sensus-latinus.html
├── <style>         — CSS embebido (133 líneas)
│   ├── Variables CSS (6 colores, 3 tipografías)
│   ├── Responsive (breakpoint a 600px)
│   └── Modos de lectura (body.mode-basico / .mode-intermedio / .mode-avanzado)
├── <body>          — Estructura HTML
│   ├── Hero + búsqueda
│   ├── Barra de modos (Aficionado / Estudiante / Profesor)
│   ├── Navegación por temas (11 botones)
│   ├── Área de contenido (renderizado dinámico)
│   └── Footer
└── <script>        — JavaScript embebido (IIFE, ~740 líneas)
    ├── THEMES[]    — Definición de 11 categorías
    ├── ENTRIES[]   — 27 entradas con 14 campos cada una
    └── Lógica      — Búsqueda, filtrado, renderizado, seguridad XSS
```

**No hay dependencias.** No se carga nada de internet. Todo — datos, estilos, lógica — vive dentro del archivo.

### Funcionalidades

- **Búsqueda en tiempo real** con debounce de 150ms. Busca en: lema, definiciones, raíz PIE, derivados, cognados, ejemplos.
- **Filtrado por tema** — 11 categorías clicables que aislan entradas por campo de estudio.
- **Modos de lectura** — Tres niveles que ocultan/muestran contenido progresivamente mediante clases CSS (`lvl-basico`, `lvl-intermedio`, `lvl-avanzado`).
- **Prevención de XSS** — Función `esc()` que sanitiza todo contenido dinámico mediante nodos de texto del DOM.
- **Responsive** — Adaptable a móvil mediante media query a 600px con tipografía fluida (`clamp()`).

---

## Esquema de datos

Cada una de las 27 entradas sigue un schema JSON de 14 campos obligatorios:

```json
{
  "id": "lux_lucis",
  "lemma": "lux, lucis",
  "lang": "latin",
  "pos": "sustantivo (3a decl.)",
  "themes": ["II", "V"],
  "level": "intermedio",
  "ipa": "/luks/",
  "defs": ["Luz, claridad, día. [...]"],
  "etym": {
    "pie": "*lewk-",
    "path": ["PIE *lewk-s > lat. lux (s) > lucis (radical)"],
    "notes": "Raíz asociada a brillo y visibilidad"
  },
  "evo": [
    { "s": "lat.", "from": "kt", "to": "t", "rule": "asimilación", "exp": "lukt- > lux (kt > x / _u)" },
    { "s": "lat.", "from": "ks", "to": "s", "rule": "sonorización", "exp": "lux > lucis (x > s / _i)" }
  ],
  "deriv": [
    { "w": "luz", "l": "es", "u": "dar luz" },
    { "w": "luminoso", "l": "es", "u": "cubierto de luz" },
    { "w": "light", "l": "en", "u": "to shed light" },
    { "w": "lumière", "l": "fr", "u": "lumière du jour" }
  ],
  "cogn": [
    { "w": "luna", "l": "es", "m": "astro que brilla" },
    { "w": "lucid", "l": "en", "m": "clear, bright" }
  ],
  "example": "Lux in tenebris lucet et tenebrae eam non comprehenderunt. — Juan 1:5",
  "cmp": {
    "culto": "luminoso",
    "vulgar": "lumbre",
    "es": "luz",
    "it": "luce",
    "fr": "lumière"
  }
}
```

### Campos detallados

| Campo | Tipo | Descripción |
|---|---|---|
| `id` | string | Identificador único (slug) |
| `lemma` | string | Palabra en latín/griego (con nominativo y genitivo si aplica) |
| `lang` | string | `"latin"` o `"greek"` |
| `pos` | string | Parte de la oración + declinación |
| `themes` | string[] | IDs de temas (I–XI) |
| `level` | string | `"basico"`, `"intermedio"` o `"avanzado"` |
| `ipa` | string | Pronunciación IPA |
| `defs` | string[] | Definiciones (1–2 por entrada) |
| `etym` | object | Etimología: raíz PIE (`pie`), camino evolutivo (`path`), notas |
| `evo` | object[] | Pasos de evolución fonética con regla y explicación |
| `deriv` | object[] | Derivados modernos: palabra (`w`), lengua (`l`), uso (`u`) |
| `cogn` | object[] | Cognados: palabra (`w`), lengua (`l`), significado (`m`) |
| `example` | string | Cita de uso con atribución |
| `cmp` | object | Tabla comparativa romance: culto, vulgar, español, italiano, francés |

---

## Corpus teórico y fuentes

SENSUS LATINUS opera desde la tradición filológica comparada:

- **Lewis & Short** — *A Latin Dictionary* (1879). Referencia clásica para el latín.
- **Liddell, Scott & Jones** — *A Greek-English Lexicon* (1940). Referencia para el griego clásico.
- **Perseus Digital Library** — Corpus textual y herramientas de análisis morfológico.
- **Logeion** — Interfaz unificada para LSJ y Lewis & Short con datos de морфología.
- **Calvert Watkins** — *The American Heritage Dictionary of Indo-European Roots*. Etimología PIE.
- **Michiel de Vaan** — *Etymological Dictionary of Latin and the Other Italic Languages* (2008).

### Fuentes por entrada

Cada entrada referencia tácitamente las fuentes above. Las etimologías PIE siguen a Watkins y de Vaan; las definiciones latinas se basan en Lewis & Short; las griegas en LSJ. Los pasos de evolución fonética siguen modelos estándar de cambio lingüístico romance (asimilación, lenición, sonorización, diptongación, palatalización, simplificación de grupos consonánticos).

---

## Diseño como posición

La paleta visual es un argumento estético:

- **Negro `#0a0a0a`** — El espacio donde el pensamiento ocurre.
- **Crema `#f5f0e8`** — La página como soporte, no como pantalla.
- **Rojo `#c23b22`** — La urgencia del significado que no se deja ignorar.

La tipografía es la estrella: tres familias (serif para el cuerpo, sans para la interfaz, mono para los datos técnicos). No hay fotografías. No hay iconos decorativos. La página funciona como póster editorial y como herramienta de consulta. En esa tensión entre cartel y diccionario se manifiesta una idea de diseño que no decora el saber, sino que lo hace visible.

La estética sigue la tradición de **Paula Scher**: tipografía como imagen, composición diagonal, monocromático con acento. El resultado es un diccionario que parece un cartel de una exposición de filología y funciona como una herramienta de investigación seria.

---

## Cómo usarlo

### Opción A — Clonar el repositorio
```bash
git clone https://github.com/NigelMoonwriter/sensus_latinus.git
```
Abrir `sensus-latinus.html` en cualquier navegador.

### Opción B — Descargar directamente
Ir al repositorio → `sensus-latinus.html` → Download raw file → doble clic.

### Opción C — Usar en línea
**[sensus-latinus en GitHub Pages](https://nigelmoonwriter.github.io/sensus_latinus/)**

No se necesita npm, ni Node, ni Python, ni servidor, ni conexión a internet. El archivo funciona en cualquier navegador moderno de forma autónoma.

---

## Parte del Entorno Greka

SENSUS LATINUS es uno de cuatro diccionarios de la familia **Entorno Greka**:

| Diccionario | Campo | Entradas |
|---|---|---|
| [SENSUS LATINUS](https://github.com/NigelMoonwriter/sensus_latinus) | Latín · Griego | 27 |
| [SENSUS GRAECUS](https://github.com/NigelMoonwriter/sensus_graecus) | Griego clásico | 31 |
| [SENSUS SEMANNSIS](https://github.com/NigelMoonwriter/sensus_semannsis) | Griego · IA | 61 |
| [SENSUS NEPANTLA](https://github.com/NigelMoonwriter/sensus_nepantla) | Spanglish | 27 |

El índice central: [entorno_greka](https://github.com/NigelMoonwriter/entorno_greka)

Cada diccionario es un archivo HTML independiente. Juntos forman un ecosistema de herramientas filológicas sin plataforma, sin tracking, sin intermediarios.

---

## Licencia

`CC BY-NC-SA 4.0` — Libre para uso y adaptación no comercial con atribución. Los derivados deben mantener la misma licencia.

---

**Rei García / KhaosLiminal / Sarayu Aguilar**
Morelia, Michoacán, México — 2026

*Nombrar es interpretar. Un diccionario, cuando está bien hecho, no solo explica vocablos; ordena una ontología mínima del habla.*
