# Funcionalidades

> Qué hace el sitio, módulo por módulo. Cada bloque indica para quién existe, no solo qué pinta.

## 1. Portada

**Para qué:** que en 5 segundos se entienda qué hace la empresa y qué hacer a continuación.

- Propuesta de valor en una línea y dos llamadas a la acción (ver servicios / cotizar).
- Servicios principales en tarjetas con icono, título y acceso al detalle.
- Banda de cifras (proyectos, años, m² construidos) como prueba de escala.
- Testimonios de clientes.
- Bloque de contacto al pie de cada sección, sin obligar a buscar el menú.

## 2. Servicios

**Para qué:** que el cliente se reconozca en un servicio concreto.

- Cinco líneas de servicio: obras civiles, tabiquería, pintura, terminaciones y remodelación.
- Cada una con página propia: alcance, proceso de trabajo, plazos y preguntas frecuentes.
- Bloques de aparición escalonada al hacer scroll (con opción de desactivarlas).

## 3. Portafolio de proyectos

**Para qué:** sustituir "confía en nosotros" por evidencia.

- Listado con imagen, categoría y resumen de cada obra.
- Ficha de detalle con: cliente, plazo, ubicación, superficie, presupuesto referencial, servicios
  ejecutados, desafíos, soluciones y resultados.
- **Galería con lightbox**: las imágenes se amplían sin salir de la página, con navegación por
  teclado.

## 4. Blog

**Para qué:** captar búsquedas técnicas y demostrar criterio.

- Listado con búsqueda por título o contenido y filtro por categoría.
- Artículo con tiempo de lectura, autor, fecha, etiquetas y artículos relacionados.
- Contenido en formato enriquecido (títulos, listas, jerarquía).

## 5. Calculadora de presupuesto

**Para qué:** convertir la curiosidad en una conversación con una cifra.

- Selección guiada: tipo de obra y superficie.
- Estimación inmediata en pantalla.
- **No promete un precio cerrado**: aclara que es una estimación y ofrece cerrar con una visita.

## 6. Agendamiento

**Para qué:** que el interesado reserve sin llamar.

- Formulario por pasos: servicio → fecha → datos → confirmación.
- Selección de fecha desde calendario.
- Validación por paso antes de avanzar.
- Confirmación en pantalla (modo demostración: no crea la cita en un sistema).

## 7. Contacto

- Formulario con nombre, correo, teléfono y mensaje.
- Validación de formato de correo y longitud mínima del mensaje.
- Estado de carga en el botón y confirmación explícita.
- Datos de contacto visibles: correo, teléfono y dirección.

## 8. Transversales

| Módulo | Qué aporta |
|---|---|
| **SEO** | título y descripción por página, Open Graph, JSON-LD de negocio, `sitemap.xml`, `robots.txt` |
| **PWA** | instalable desde el navegador, iconos en 8 tamaños, service worker |
| **Accesibilidad** | foco visible, contraste, `prefers-reduced-motion`, formularios etiquetados |
| **Animaciones** | aparición al entrar en viewport, escalonadas, desactivables |
| **Legales** | política de privacidad (Ley 19.628) y términos (Ley 19.496) |
| **404** | página propia en lugar del error del servidor |

## 9. Modo demostración

Todas las funciones que escribirían datos (contacto, cita) están en modo demo:

- validan como en producción,
- muestran el estado de carga,
- y avisan **explícitamente** que no envían nada.

Así el escaparate se puede enseñar sin prometer una funcionalidad que no está conectada.
