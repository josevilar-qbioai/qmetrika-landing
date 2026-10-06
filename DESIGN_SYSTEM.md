# QMetrika Labs — Design System

Documento de referencia de la identidad visual de **qmetrika.xyz**. Propuesta minimalista con tema oscuro como principal.

Última actualización: octubre de 2026

> **Estado de la migración.** La hoja de estilos de este sistema es `qmetrika.css`. Por ahora solo la usa `index.html`. El resto de páginas (`en.html`, `blog/`, `tools/`) siguen cargando `styles.css` y se migrarán una a una. No editar `styles.css` para aplicar este sistema: afectaría a todo el sitio a la vez.

---

## 0. Principios

1. **Una tinta y un acento.** El color sirve para leer, no para decorar. El terracota aparece una o dos veces por pantalla.
2. **Líneas, no sombras.** La estructura se dibuja con líneas de 1px (`--rule`) y con un único escalón de fondo (`--panel`).
3. **Esquinas rectas.** Sin `border-radius` en ningún elemento.
4. **Dos familias, siete estilos.** Space Grotesk para leer; IBM Plex Mono para rotular.
5. **Un patrón por página.** Filas de índice separadas por líneas finas; nada de tarjetas ni recuadros.

---

## 1. Marca

### Ficheros (`assets/`)

| Fichero | Descripción | Uso |
|---------|-------------|-----|
| `simbolo-q-negativo.svg` | Símbolo Q, fondo oscuro | **Por defecto** (tema oscuro) |
| `logo-qmetrika-negativo.svg` | Símbolo + «qmetrika», fondo oscuro | **Por defecto** (tema oscuro) |
| `simbolo-q.svg` | Símbolo Q, fondo claro | Bloques claros, documentos impresos |
| `logo-qmetrika.svg` | Símbolo + «qmetrika», fondo claro | Bloques claros, documentos impresos |
| `favicon.svg` | Favicon | `<link rel="icon">` en todas las páginas |

### Símbolo Q en navegación (negativo, 26×26px)

```html
<svg viewBox="6 6 46 46" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
  <circle cx="28" cy="28" r="18" stroke="#E9E7E0" stroke-width="4.5"/>
  <circle cx="41" cy="41" r="9.6" fill="#1B1B18"/>
  <circle cx="41" cy="41" r="7.4" fill="#E9E7E0"/>
  <circle cx="41" cy="41" r="5.4" fill="#A6542E"/>
</svg>
```

Sobre fondo claro se intercambian `#E9E7E0` y `#1B1B18`; el núcleo `#A6542E` no cambia. No recolorear, no girar, no añadir efectos.

---

## 2. Color

Siete tokens. El tema oscuro es el principal (`:root`); el claro se activa con `data-theme="light"` en cualquier contenedor.

| Token | Oscuro | Claro | Uso |
|-------|--------|-------|-----|
| `--bg` | `#1B1B18` | `#E9E7E0` | Fondo de página |
| `--panel` | `#2A2925` | `#DEDBD1` | Callouts, código, cabeceras de tabla |
| `--ink` | `#E9E7E0` | `#1B1B18` | Texto principal, botón sólido |
| `--muted` | `#B4B0A5` | `#57544B` | Texto secundario, entradillas, pie |
| `--rule` | `#3A3934` | `#CFCCC2` | Líneas de 1px y huecos de rejilla |
| `--accent` | `#A6542E` | `#A6542E` | Núcleo del símbolo, rellenos, texto ≥24px |
| `--accent-text` | `#D98A5E` | `#904625` | Kickers, enlaces, etiquetas, cifra destacada |

Contraste (WCAG AA, 4,5:1 en texto normal), tema oscuro: `ink` 14:1, `muted` 8:1 y `accent-text` 6,4:1 sobre `bg`. `--accent` sobre fondo oscuro da 3,2:1: **nunca como texto**.

Cambios respecto a la versión de julio: se retiran `--faint` (3,6:1, no cumplía AA), `--dark`, `--dark-fg`, `--dark-muted` (sustituidos por el tema) y los colores de fase `--c-build`, `--c-test`, `--c-learn`. En diagramas se usan `ink`, `accent`, `muted` y `rule`, que se distinguen por luminosidad.

---

## 3. Tipografía

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap">
```

| Clase | Tamaño / interlineado · peso | Familia | Uso |
|-------|------------------------------|---------|-----|
| `.display` | 48 / 1,08 · 500, −0,03em | Space Grotesk | H1 (36px en móvil) |
| `.heading` | 24 / 1,2 · 500, −0,02em | Space Grotesk | H2 cuando haga falta |
| `.title` | 17 / 1,45 · 500 | Space Grotesk | Título de fila (línea, publicación, herramienta) |
| `.lede` | 14 / 1,75 · 400 | IBM Plex Mono | Entradilla de la cabecera |
| `.desc` | 13 / 1,7 · 400 | IBM Plex Mono | Descripción bajo cada título |
| `.q-kick`, `.meta` | 11 / 1,4 · 500, +0,1em | IBM Plex Mono | Rótulos de sección y metadatos |

Los titulares nunca pasan de peso 500.

---

## 4. Espacio y retícula

| Token | Valor | Uso |
|-------|-------|-----|
| `--space-1` | 8px | Etiqueta–título, huecos entre etiquetas |
| `--space-2` | 16px | Entre párrafos y elementos de tarjeta |
| `--space-3` | 24px | Relleno de tarjetas, callouts, celdas |
| `--space-4` | 48px | Margen lateral, separación entre bloques |
| `--space-5` | 88px | Relleno vertical de sección |

Contenedor `.shell`: 960px (portada y tesis), 740px (artículo). Margen lateral 48px, 22px por debajo de 760px.

---

## 5. Componentes (`qmetrika.css`)

La portada es un índice de investigación: texto sobre fondo plano, separado solo por líneas de 1px. Sin tarjetas, recuadros ni botones.

| Clase | Qué es |
|-------|--------|
| `.q-nav` | Barra superior: marca y enlaces entre corchetes en mono. Línea inferior `rule` |
| `.intro` | Cabecera: kicker, `.display` y una entradilla `.lede` |
| `.q-section-head` | Cabecera de sección: `§ 01` + nombre a la izquierda, metadato a la derecha, línea inferior en `ink` |
| `.q-index` + `.q-row` | Fila de índice en tres columnas: código y tipo · título y descripción · enlaces o DOI. Línea inferior `rule` |
| `.q-footer` | Pie: autor, ORCID, GitHub, email; debajo, año y enlaces secundarios |

Ancho de contenido: 960px (`.shell`). Un solo nivel de énfasis de color: los enlaces en `accent-text`.

---

## 6. Lenguaje de investigación

El sitio se lee como el de un laboratorio: estructura de artículo científico, no de página comercial.

- **Secciones numeradas:** `§ 01 líneas de investigación`, `§ 02 publicaciones`, `§ 03 herramientas abiertas`.
- **Publicaciones como bibliografía:** código (`P-L2`, `TECH-2`), tipo (`preprint`, `informe técnico`), título original y DOI completo.
- **Cada cifra con su fuente:** toda cifra (AUC, número de genes, % de varianza) aparece junto a la publicación que la respalda.
- **Sin reclamos comerciales:** nada de filas de cifras, botones de llamada a la acción ni bloques de «disciplinas».
- **Contacto en el pie,** no como sección.

---

## 7. Convenciones de contenido

- Navegación entre corchetes: `[ herramientas ]  [ bio-ia ]  [ blog ]`.
- Kicker: `// nombre_seccion` o `// 01 · nombre`, en minúsculas.
- Selector de idioma: `es/en`, con la barra en `accent-text`.
- Español como original; inglés con sufijo `-en.html` (blog) o `en.html` (portada).
- Traducciones fijadas: «espiral de acumulación» por *flywheel*; *fine-tuning* en inglés y cursiva; «el ratio».
- Construcciones impersonales mejor que primera persona del plural. Sin emojis.
- Email ofuscado: mostrar `info[at]qmetrika.xyz`; construir el `mailto:` con JavaScript si hace falta.

---

## 8. Qué no hacer

- `border-radius`, sombras, degradados o texturas de fondo.
- Colores fuera de los siete tokens.
- `--accent` en texto de menos de 24px.
- Bordes izquierdos de color para destacar bloques.
- Titulares en peso 700.
- Estilos en línea (`style=""`) para tamaños o colores: usar las clases.
