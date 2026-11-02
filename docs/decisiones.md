# Documento de decisiones de diseño

> Proyecto académico ficticio: PádelComunidad · Caso 05, Urbanización Los Olivos. Cada decisión indica qué se eligió, por qué y qué alternativa se descartó.

## Ruta de trabajo

- [ ] Ruta A · Figma
- [x] Ruta B · VS Code: diseño directamente en `guia.html` y estilos en Sass.

## 1. Color (RA1 · CE b)

- **Elección:** escala de acento cálido para el caso 05, cuyo tono de referencia es **52° en OKLCH**. Se definen seis niveles (50, 300, 400, 700, 800 y 950) en `$primitivos` de `scss/abstracts/_tokens.scss`. La escala mantiene como referencia el tono OKLCH de 52°.
- **Uso:** `$tema` asigna `acento-700` al tema claro y `acento-400` al oscuro; para hover utiliza 800 y 300. `sobre-acento` define el texto del botón y `acento-tenue` su fondo suave. Los componentes solo consultan variables semánticas como `var(--color-acento)`.
- **Accesibilidad:** `$pares-contraste` exige al menos 4,5:1 en los pares de texto declarados y 3:1 para foco y bordes de control. `npm run check` verifica estos pares en ambos temas; `guia.html` recoge las muestras y sus contrastes. Hay que contrastar las cifras de la guía con los valores finales del código.
- **Alternativa descartada:** escribir colores hexadecimales directamente en los componentes o usar el mismo tono de acento para ambos temas, porque dificultaría mantener la coherencia y el contraste.

## 2. Tipografía (RA1 · CE b)

- **Familia:** `system-ui`, para buena legibilidad, compatibilidad con cada sistema y ausencia de descarga de fuentes externas. La fuente monoespaciada se reserva para datos como el concepto del pago.
- **Escala:** base de 16 px y razón 1,2 en móvil; base de 18 px y razón 1,25 en escritorio. Sass genera siete pasos (−1 a 5) mediante `clamp()` y `rem`, para adaptar la jerarquía sin tamaños fijos por dispositivo. Interlineado: 1,5 en texto y 1,15 en títulos.
- **Lectura:** los párrafos tienen `max-inline-size: 65ch` y `text-wrap: pretty`, para limitar la longitud de línea y mejorar los saltos.
- **Alternativa descartada:** tamaños fijos en `px` y fuentes web sin necesidad justificada, por peor adaptabilidad o mayor coste de carga.

## 3. Espaciado y forma

- **Escala:** 4, 8, 12, 16, 24, 32, 48 y 64 px (tokens `3xs` a `2xl`, publicados en `rem`). Mantener la escala de la plantilla evita separaciones arbitrarias y facilita la consistencia.
- **Radios:** 8 px en controles, 12 px en tarjetas y formato píldora para elementos redondeados. Se usan los tokens `--radio-control`, `--radio-tarjeta` y los que publica la plantilla.
- **Alternativa descartada:** asignar márgenes, rellenos y radios independientes a cada componente, porque dificultaría modificar el sistema de forma global.

## 4. Componentes (RA1 · CE f)

| Componente | Estados o variantes | Resolución en CSS |
| --- | --- | --- |
| Botón | Normal, hover, foco, desactivado y secundario | Clase `.boton`, pseudoclases y modificador `.boton--secundario`; tokens semánticos. |
| Tarjeta de turno | Disponible, seleccionado, ocupado y foco | Radio accesible; `.turno:has(:checked)`, `:has(:disabled)` y `:has(:focus-visible)`. Ocupado añade borde discontinuo y texto. |
| Contador de invitados | 0–3 invitados, marcado, foco y desactivado | `fieldset` y radios con el mismo `name`; `.invitados__opcion:has(...)`. No requiere JavaScript. |
| Aviso de pago | Ejemplo normal en Fase 1; aparición condicional en Fase 4 | `.aviso` y elementos BEM con importe, teléfono y concepto ficticios. En Fase 4 se mostrará con `:has()` según los radios. |

Todos los estados interactivos deben poder identificarse sin depender solo del color y los objetivos táctiles deben alcanzar 44 × 44 px.

## 5. Comparativa de tecnologías (RA1 · CE e)

| Criterio | Figma | Penpot | Diseño en código |
| --- | --- | --- | --- |
| Coste / licencia | Plan gratuito con límites; herramienta propietaria | Código abierto; opción de alojamiento propio | VS Code y herramientas del proyecto disponibles sin coste de licencia |
| Traslado a código | Requiere trasladar o sincronizar decisiones | Requiere trasladar o sincronizar decisiones | La guía y los componentes usan directamente los tokens de Sass |
| Mantenimiento | Variables y componentes visuales | Bibliotecas y componentes visuales | Una fuente de verdad en `_tokens.scss` |

| Criterio | Sass + CSS propio | CSS nativo | Bootstrap / Tailwind |
| --- | --- | --- | --- |
| Tokens y temas | Mapas Sass y Custom Properties | Custom Properties escritas manualmente | Sistema de configuración o utilidades del framework |
| CSS final | Solo las reglas que se diseñan y compilan | Sin compilación Sass | Depende de la configuración y de las clases utilizadas |
| Cascada | `@layer` y selectores propios | `@layer` y selectores propios | Convenciones y estilos del framework que hay que integrar |

**Decisión:** Ruta B con VS Code, Sass modular y CSS propio. Se ajusta a la plantilla y a la prohibición de frameworks CSS y JavaScript de esta fase. Sass organiza mapas, mixins y compilación; las Custom Properties permiten cambiar de tema en el navegador. Se descarta hacer primero el diseño en Figma o Penpot porque añadiría un paso de traspaso de valores sin aportar una ventaja necesaria en este encargo.
