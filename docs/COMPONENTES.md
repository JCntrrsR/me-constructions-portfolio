# Componentes del escaparate — inventario y criterio

> Estado al 2026-10-23, tras la reparación del build. Sirve para decidir qué se usa, qué se
> conserva sin usar y qué conviene eliminar en la siguiente pasada.

## Reglas de esta carpeta

1. **Un componente se usa o se documenta.** Si no lo importa ninguna página ni layout, va aquí
   con el motivo; no se deja suelto como si estuviera vivo.
2. **Los datos no viven dentro de las páginas.** Están en `src/data/` (tipados) para que el
   listado y el detalle compartan la misma fuente.
3. **Los formularios no hablan con `fetch` directo.** Pasan por `src/lib/formularios.ts`, que
   decide entre envío real y modo demostración.
4. **Las animaciones no se copian.** Se marca el elemento con `data-reveal` y la lógica vive en
   `src/lib/reveal.ts`.

## En uso

| Componente | Se usa en | Qué aporta |
|---|---|---|
| `Layout.astro` | todas | shell, SEO, fuentes, reveal, analytics |
| `OptimizedImage` | index, proyectos, proyectos/[id] | imagen con placeholder y lazy |
| `LoadingButton` | index, citas, proyectos/[id] | estado de carga en botones |
| `BudgetCalculator` | index, calculadora | estimación de presupuesto |
| `ImageGallery` | proyectos/[id] | galería con lightbox (PhotoSwipe) |
| `AdvancedImageGallery` | blog | galería del listado de artículos |
| `AdvancedTestimonials` | index | carrusel de testimonios |
| `EnterpriseContactForm` | index | formulario multi-paso |
| `ChatBot` | index | asistente con respuestas predefinidas (**mock**) |
| `PWAInstaller` | index | instalación de la app |
| `ScrollToTop` | Layout | volver arriba |
| `NotificationSystem` | Layout | avisos |
| `AdvancedSEO` | Layout | metadatos y JSON-LD |
| `Analytics` | Layout | analítica (**IDs placeholder**) |
| `ErrorBoundary` | Layout | captura de errores de render |

## Sin uso (se conservan, requieren decisión)

| Componente | Motivo por el que no se usa | Recomendación |
|---|---|---|
| `TestimonialSlider` | duplica `AdvancedTestimonials`, que sí se usa | eliminar o fusionar |
| `ContactForm` | `EnterpriseContactForm` lo reemplazó (ya adaptado al modo demo) | mantener como formulario simple |
| `Card` | las tarjetas se escribieron inline en cada página | adoptar en la próxima pasada |
| `Toast` | `NotificationSystem` cubre el caso | eliminar |
| `LazyImage` / `LazyComponent` / `ImageWithFallback` | `OptimizedImage` cubre el caso | eliminar |
| `LoadingSpinner` | `LoadingButton` lo incluye | eliminar |
| `PerformanceMonitor` | no hay backend que reciba métricas | dejar para producción |

## Librerías declaradas

| Librería | Estado |
|---|---|
| `photoswipe` | **en uso** (galería) |
| `sweetalert2` | **en uso** (avisos de formularios, confirmaciones) |
| `swiper` | **sin uso** — se quitó de `manualChunks` y `optimizeDeps`; se puede desinstalar |
| `aos` | **sin uso** — reemplazada por `src/lib/reveal.ts` |
| `lazysizes` | **sin uso** — el lazy loading lo hace `OptimizedImage` |

## Módulos propios añadidos

| Módulo | Responsabilidad |
|---|---|
| `src/lib/formularios.ts` | envío único, modo demo, validación mínima |
| `src/lib/reveal.ts` | animación de aparición compartida |
| `src/data/blog.ts` · `src/data/projects.ts` | fuente única de contenido |
| `scripts/build-optimization.js` | verificación post-build (páginas, enlaces, CSS) |
| `scripts/generate-icons.mjs` | iconos PWA desde `public/logo-ca.svg` |
