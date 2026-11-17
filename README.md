# PádelComunidad 2.0 · Urbanización Los Olivos

Proyecto académico de **Diseño de Interfaces Web (0615) · 2.º DAW · Curso 2026–2027**. Caso 05: Comunidad de Propietarios Urbanización Los Olivos. **Todos los datos son ficticios.**

## Fase 1: sistema de diseño

`guia.html` presenta paleta, tokens semánticos, tipografía, espaciado y componentes reutilizables. La arquitectura SCSS emplea `@use`, `@forward`, BEM y capas CSS.

## Fase 2: estructura del portal

| Archivo | Página |
|---|---|
| `index.html` | Turnos: seleccionar fecha, pista y horario |
| `reserva.html` | Confirmar reserva: invitados, Bizum y aceptación de normas |
| `justificante.html` | Justificante: referencia, PIN, turno y estado de pago |
| `mis-turnos.html` | Mis turnos: tabla y acciones de cancelación |
| `normas.html` | Normas de uso |
| `aviso-legal.html` | Aviso legal LSSI |
| `privacidad.html` | Privacidad RGPD |

Las dos plantillas originales de trabajo están en `plantilla-tarea.html` y `plantilla-lectura.html`. El mapa editable en diagrams.net es `docs/mapa-navegacion.drawio`; su versión exportable SVG está en `docs/mapa-navegacion.svg`.

## Arranque y comprobación

Instala dependencias si es necesario con `npm ci` y ejecuta:

```bash
npm run dev    # Sass en vigilancia
npm run check  # compila Sass + pasa Stylelint
```

Abre `index.html` en navegador/Live Preview y recorre las siete páginas. Para ver el sistema de diseño original, abre `guia.html`.

**Importante:** la Fase 2 es una **maqueta HTML de navegación**. No contiene backend ni JavaScript. Los formularios pasan a la siguiente página pero no registran reservas, los ejemplos de justificante no se generan a partir de los datos elegidos y los botones de cancelación son ilustrativos. La funcionalidad real deberá implementarse en una fase posterior.

## Accesibilidad y validación

- Un `<h1>` y un `<main>` por página, landmarks HTML5 y dos navegaciones con nombre.
- Primer enlace de teclado «Saltar al contenido»; enlace activo marcado con `aria-current="page"`.
- Radios agrupados en `fieldset` con `legend`, controles etiquetados; turnos ocupados sin nombres de viviendas.
- Estilos SCSS comprobables con `npm run check`; contraste integrado en Sass.
- **Validación oficial W3C manual pendiente:** hay que subir las **siete páginas y las dos plantillas** a <https://validator.w3.org/#validate_by_upload>, corregir todos los errores/avisos y guardar nueve capturas *reales* en `docs/validacion/` (véase `docs/validacion/LEEME.md`).

Más información: `docs/ficha-caso.md`, `docs/decisiones.md` (Fase 1) y `docs/fase2-decisiones.md` (Fase 2).
