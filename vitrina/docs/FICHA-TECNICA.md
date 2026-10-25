# Ficha técnica

## Stack

| Capa | Tecnología | Por qué |
|---|---|---|
| Framework | **Astro** | genera HTML estático y solo envía JS donde hace falta |
| Estilos | **Tailwind CSS** | utilidades con purga por contenido; tokens de marca centralizados |
| Lenguaje | **TypeScript** | contratos de datos explícitos (blog, proyectos) |
| PWA | manifest + service worker | instalable y con caché de assets |
| Build | Vite | recarga en caliente y builds incrementales |

## Métricas de la versión publicada

| Métrica | Valor |
|---|---|
| Páginas generadas | 24 |
| Rutas | 12 + detalle de proyectos y blog |
| Peso total del build | ~1,5 MB |
| CSS | ~42 KB (con la paleta completa) |
| Enlaces internos rotos | 0 |
| Páginas sin hoja de estilos | 0 |
| JavaScript obligatorio para ver contenido | ninguno |

## Estructura de contenido

| Tipo | Cuántos | Formato |
|---|---|---|
| Proyectos | 3 fichas completas | módulo tipado (cliente, plazo, superficie, galería…) |
| Artículos de blog | 6 | módulo tipado (autor, fecha, categoría, etiquetas) |
| Servicios | 5 | página propia cada uno |

## Sistema de diseño

- **Color primario:** `#1B3C59` (azul petróleo), con variantes oscura y clara.
- **Acento:** `#C9A227` (dorado) para llamadas de atención puntuales.
- **Tipografías:** Inter (texto) + Playfair Display (títulos), servidas localmente.
- **Componentes base:** botones, tarjetas, secciones y encabezados definidos una sola vez.

## Verificación automática

El proyecto compila con un verificador que se ejecuta en cada build:

```
✓ 24 páginas · 50 assets · 1.483 KB
✓ sin enlaces internos rotos
✓ todas las páginas cargan CSS
```

Si cualquiera de las tres falla, el build termina con error.

## Decisiones que se tomaron a propósito

| Decisión | Alternativa descartada | Motivo |
|---|---|---|
| Estático | SPA con React | SEO y tiempo de carga para un sitio de captación |
| Datos en módulos tipados | contenido dentro de cada página | evitar duplicación y desincronización |
| Formularios en modo demo | formularios que fallan sin backend | no prometer lo que no está conectado |
| Animación opt-out | animación forzada | respeto por `prefers-reduced-motion` |
| Sin sourcemaps en producción | sourcemaps publicados | no exponer el código fuente |

## Compatibilidad

Navegadores modernos (Chrome/Edge 90+, Firefox 90+, Safari 15+). El sitio es usable sin
JavaScript para lectura de contenido; la galería, la calculadora y los formularios requieren JS.
