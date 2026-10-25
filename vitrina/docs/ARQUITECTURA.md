# Arquitectura

> Documento de vitrina: explica **cómo está construido** el sitio sin publicar el código.
> Si necesitas el detalle de implementación, se comparte bajo acuerdo.

## Decisión principal: estático, no SPA

El sitio se genera como HTML estático. Es una decisión deliberada, no una limitación:

| Criterio | Estático (elegido) | SPA (descartado) |
|---|---|---|
| Tiempo hasta ver contenido | inmediato (HTML ya pintado) | espera al bundle de JS |
| SEO | cada página es indexable por sí sola | requiere render en servidor o prerender |
| Coste de hosting | $0 en CDN | servidor o funciones |
| Mantenimiento | sin dependencias en runtime | framework + router + estado |

Para un sitio de servicios donde el objetivo es **que te encuentren y te escriban**, el estático
gana en las tres dimensiones que importan.

## Capas

```
┌─────────────────────────────────────────────┐
│  Páginas (rutas)                            │  index, servicios, proyectos, blog, contacto…
├─────────────────────────────────────────────┤
│  Componentes                                │  galería, calculadora, formularios, tarjetas
├─────────────────────────────────────────────┤
│  Datos tipados                              │  blog.ts · projects.ts (fuente única)
├─────────────────────────────────────────────┤
│  Sistema de diseño                          │  tokens + utilidades (Tailwind)
├─────────────────────────────────────────────┤
│  Servicios transversales                    │  SEO, PWA, animaciones, envío de formularios
└─────────────────────────────────────────────┘
```

### Por qué los datos están separados de la vista

El listado de proyectos y la página de detalle necesitan **el mismo contenido**. Si cada uno lo
declara por su cuenta, se desincronizan al primer cambio. Por eso el contenido vive en módulos
tipados que ambas páginas importan, y el detalle se genera a partir de esa misma lista.

Esto además permite migrar el contenido a un CMS o a una base de datos sin tocar las páginas.

## Generación de rutas

Las páginas de detalle se generan en el build a partir de los datos: una ruta por proyecto y una
por artículo. El resultado es HTML puro, sin consultas en tiempo de ejecución.

## Comportamiento sin backend

El escaparate no incluye servidor. En lugar de dejar formularios que fallen con un error opaco,
hay una capa que decide qué hacer:

| Situación | Respuesta al usuario |
|---|---|
| Modo demostración | aviso explícito: "tus datos no se envían" |
| Backend ausente (404) | se trata como demostración, no como error |
| Error de red / timeout | mensaje real, distingue "tardó demasiado" |
| Éxito | confirmación normal |

Cambiar a producción implica activar el envío real y desplegar el endpoint: el resto del sitio no
se toca.

## Rendimiento

- HTML por página, sin hidratación global.
- Imágenes con dimensiones declaradas y carga diferida.
- CSS generado solo con las clases usadas (Tailwind purga por contenido).
- JS cargado por componente, no en un bundle único.

## Accesibilidad

- Foco visible en todos los elementos interactivos.
- `prefers-reduced-motion`: si el usuario pide menos movimiento, las animaciones se desactivan y el
  contenido aparece de inmediato.
- Contraste verificado sobre la paleta de marca.
- Etiquetas y textos alternativos en formularios e imágenes.

## Verificación

El build incluye un verificador propio que falla si:

- una página queda sin hoja de estilos,
- un enlace interno apunta a una ruta que no existe,
- un asset referenciado no está en la salida.

Se ejecuta en cada compilación, no como paso manual opcional.
