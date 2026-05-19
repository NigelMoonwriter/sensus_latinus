# ACCESSIBILITY

## Objetivo
Asegurar una accesibilidad mínima real en los HTML standalone del ecosistema.

## Requisitos mínimos
- Todo `input` debe tener `label` visible o `aria-label`.
- Todo botón de toggle debe declarar `aria-expanded` y `aria-controls`.
- Los contadores dinámicos deben usar `aria-live="polite"`.
- Debe existir un skip link al contenido principal.
- Los botones de filtro deben declarar su estado (`aria-pressed` cuando aplique).
- Los bloques colapsables deben usar `hidden` o un patrón equivalente sincronizado con el estado visual.

## Semántica recomendada
- `nav` para navegación de filtros.
- `main` para contenido principal.
- `article` para entradas individuales.
- `footer` para cierre editorial.

## Contraste y legibilidad
- Verificar contraste suficiente entre fondo y texto.
- No depender solo del color para expresar estado.
- Mantener tamaños legibles en móvil.

## Prácticas de validación
- Navegar por teclado.
- Verificar foco visible.
- Revisar lectura con lector de pantalla en controles principales.
- Comprobar que los mensajes de cero resultados sean legibles y comprensibles.
