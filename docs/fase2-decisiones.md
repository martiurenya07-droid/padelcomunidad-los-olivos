# Fase 2 · Decisiones de estructura · Caso 05, Los Olivos

## Arquitectura

- Siete páginas HTML vinculadas entre sí; dos plantillas en raíz.
- Cabecera común con menú accesible, enlace de salto y página actual visible también por subrayado; pie común con datos LSSI ficticios.
- Flujo principal: `index.html` → `reserva.html` → `justificante.html` → `mis-turnos.html`. Las tres lecturas se encuentran desde todas las páginas.
- `docs/mapa-navegacion.svg` representa el flujo y agrupa los enlaces comunes.
- No hay JavaScript ni backend en la Fase 2. Los enlaces y los formularios demuestran estructura y navegación; no crean, cancelan ni almacenan reservas.

## Reutilización del sistema de diseño

- Se mantienen los tokens OKLCH H≈52° del caso, la tipografía fluida, los componentes `.boton`, `.turno`, `.invitados` y `.aviso` originales.
- Los tres parciales de layout para `.cabecera`, `.pie` y `.hueco` se añaden con `@use`, `@layer layout`, BEM, `var(--…)` y el mixin de objetivo táctil.
- Las clases adicionales de las páginas se aíslan en `scss/components/_portal.scss`; sin cambiar las reglas de los componentes existentes.
- Se mantiene el diseño base con `flex-wrap` para legibilidad en móvil; la maquetación adaptable completa se deja para la Fase 3.

## Datos y limitaciones declaradas

- Comunidad: Comunidad de Propietarios Urbanización Los Olivos, CIF ficticio H-00000005, Paseo de Los Olivos, 10, 00000 Localidad Ficticia; correo `administracion@losolivos.example`.
- Pistas Central, Norte y Sur; turnos de 60 minutos; 08:30–22:30; 2,00 €/invitado no residente, máximo tres; Bizum 600 000 000; vivienda de ejemplo 3.º A.
- La ficha **no establece un plazo de cancelación ni una sanción automática**. En normas se propone un plazo indicativo de 12 horas y revisión administrativa, con advertencia explícita de que debe aprobarlo la comunidad.
- Los datos visibles del resumen y justificante son ejemplos estáticos. Un formulario HTML estático no puede mantener la elección de `index.html` en el justificante sin un servidor o JavaScript; no se inventa esa funcionalidad.
- En el aviso Bizum se incluyen todos los importes posibles, de 0 a 6 €, porque sin JavaScript no se calcula dinámicamente la cantidad elegida. El concepto `PADEL 3A 2011` es un ejemplo válido para el 20 de noviembre.
- El pie y los textos legales indican expresamente que todos los datos son ficticios. Se describe la base jurídica propuesta RGPD 6.1.b, conservación y derechos, pero la redacción necesitaría revisión legal antes de un uso real.

## Verificación

- `npm run check`: compilación de Sass, contraste de tokens y Stylelint.
- Comprobaciones estáticas: 7 páginas + 2 plantillas, etiquetas semánticas, títulos, enlaces, etiquetas de controles, marcas `aria-current`, identidades de encabezados y navegación.
- **Pendiente de verificación manual real:** validator.w3.org, nueve capturas, navegador móvil/escritorio, navegación por teclado y árbol de accesibilidad. No se declara W3C validado hasta tener evidencia real.
- Historial de commits: crear al aplicar los pasos ahora con fechas verdaderas; no atribuirlo a las clases del 5 y 11 de noviembre.
