# Plataforma Web Constructora Andina

Plataforma web corporativa bilingüe para una empresa de construcción, construida con Astro y Tailwind CSS, que incluye captación de leads, reserva de citas, páginas de servicios, portafolio de proyectos, blog y base técnica para pagos/autenticación con Supabase + Stripe.

## Overview
Este repositorio contiene el sitio web y la capa de servicios para **Constructora Andina**, una empresa de construcción y remodelación en Santiago de Chile. La implementación actual se enfoca en:

- Páginas públicas de marketing (inicio, servicios, proyectos, nosotros, contacto)
- Flujos de conversión (formularios de contacto, calculadora de presupuesto, agendamiento de citas)
- Optimización SEO y performance (datos estructurados, optimización de imágenes, ajustes de build)
- Capacidades PWA (manifest + service worker)
- Fundaciones de integración backend (esquema Supabase, servicio de auth, pagos y email)

### Propósito del Proyecto
El proyecto resuelve un problema habitual en pymes constructoras: adquisición de clientes fragmentada y baja presencia digital. Centraliza comunicación comercial y captura de oportunidades en una sola plataforma, dejando la base preparada para operación tipo CRM (usuarios, proyectos, cotizaciones, pagos, analítica).

### Tipo de Proyecto
**Tipo:** Aplicación web de negocio (marketing + generación de leads + base operativa de servicios).

### Estado del Proyecto
**Estado actual: MVP / desarrollo activo.**

Motivo:
- Existe una experiencia pública robusta y múltiples funcionalidades de conversión.
- Varias capacidades backend están avanzadas, pero no totalmente conectadas de punta a punta en producción.
- Existen recursos y valores por defecto placeholder que requieren configuración final por entorno.

## Features
### Sitio Público
- Home responsive con hero, destacados de servicios, proyectos, testimonios y CTAs.
- Páginas dedicadas para servicios, proyectos, contacto, nosotros, blog, calculadora y citas.
- Rutas dinámicas para servicios y detalle de proyectos.

### Captación y Conversión
- Formulario de contacto estándar y formulario empresarial con más campos.
- Calculadora interactiva para estimar rangos de presupuesto.
- Flujo multi-paso de agendamiento de citas con envío de confirmaciones por email.

### Contenido y Marketing
- Listado de blog y detalle de artículo (actualmente con contenido definido en estructuras locales).
- Componentes de testimonios y galerías de imágenes.

### SEO, Performance y UX
- Layout central con componente SEO avanzado y JSON-LD estructurado.
- Preload de fuentes, placeholders/lazy loading de imágenes y utilidades de performance.
- Middleware con headers de seguridad y caché.

### PWA
- Configuración de Web App Manifest.
- Service Worker para estrategias de caché y comportamiento offline básico.
- Soporte para prompt de instalación.

### Fundaciones de Plataforma (En progreso)
- Cliente Supabase y modelo tipado de base de datos.
- Migración SQL con entidades núcleo (usuarios, proyectos, leads, citas, cotizaciones, pagos, testimonios, analítica, etc.) y políticas RLS.
- Endpoint Stripe Payment Intent y abstracción de servicio de pagos.
- Servicio de autenticación con JWT y permisos por rol.
- Abstracción de email para SendGrid/Nodemailer.

## Tech Stack
- **Framework:** Astro 5 (salida estática)
- **Lenguaje:** TypeScript + sintaxis de componentes Astro
- **Estilos:** Tailwind CSS (+ plugins forms + typography)
- **Base de datos / backend services:** Supabase (PostgreSQL, RLS, storage, base de auth)
- **Pagos:** Stripe
- **Email:** SendGrid / Nodemailer
- **PWA:** Web Manifest + Service Worker personalizado
- **Build/tooling:** Vite, ESLint, Prettier, Vitest, Sharp, imagemin

## Architecture
Organización de alto nivel:

1. **Capa de Presentación (`src/pages`, `src/components`, `src/layouts`)**
   - Las páginas Astro definen rutas.
   - Componentes reutilizables encapsulan UI + interacción cliente.
   - `Layout.astro` centraliza navegación, SEO, analítica y shell global.

2. **Servicios de Aplicación (`src/lib/services`)**
   - `authService`, `emailService`, `paymentService` encapsulan operaciones de dominio.

3. **Acceso a Datos (`src/lib/database`)**
   - Clientes Supabase y contratos tipados de base de datos.
   - Esquema/migraciones SQL en `supabase/migrations`.

4. **Capa API (`src/pages/api`)**
   - Endpoints para contacto, citas y creación de Payment Intent.

5. **Utilidades Transversales (`src/utils`, `src/middleware.ts`, `scripts/`)**
   - Performance, SEO, validación, optimización de imágenes, optimización de build, headers de caché/seguridad.

## Installation
### Prerrequisitos
- Node.js 18+
- npm 9+

### Pasos
```bash
# 1) Clonar
git clone <tu-url-del-repositorio>
cd web-construccion-portfolio

# 2) Instalar dependencias
npm install

# 3) (Recomendado) Crear .env con credenciales del proyecto
# Ver variables de entorno más abajo

# 4) Ejecutar en desarrollo
npm run dev
```

URL por defecto: `http://localhost:4321`

### Variables de Entorno Sugeridas
Crea un archivo `.env` con estas claves según corresponda:

```bash
# Supabase
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Auth
JWT_SECRET=

# Stripe
PUBLIC_STRIPE_PUBLISHABLE_KEY=
STRIPE_SECRET_KEY=

# Email (SendGrid / SMTP)
EMAIL_PROVIDER=sendgrid
SENDGRID_API_KEY=
FROM_EMAIL=
FROM_NAME=
SMTP_HOST=
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=
SMTP_PASS=
```

## Usage
### Comandos de Desarrollo
```bash
npm run dev          # Levanta servidor local
npm run build        # Build estático + optimizaciones post-build
npm run preview      # Previsualiza build de producción
npm run type-check   # Type checks de Astro
npm run lint         # Lint de archivos fuente
npm run format       # Formateo de archivos fuente
npm run optimize-images
npm run analyze
npm run test
```

### Flujos típicos
- Visita `/` para landing y CTAs de conversión.
- Usa `/calculadora` para estimación de presupuesto.
- Usa `/contacto` para solicitudes de proyecto.
- Usa `/citas` para agendar reuniones.
- Navega `/blog` y `/proyectos` para contenido de confianza.

## Project Structure
```text
.
├── public/                  # Recursos estáticos (imágenes, fuentes, manifest, service worker)
├── scripts/                 # Scripts de build y optimización de imágenes
├── src/
│   ├── components/          # Componentes UI reutilizables e interactivos
│   ├── layouts/             # Layouts compartidos
│   ├── lib/
│   │   ├── database/        # Clientes Supabase + tipos de BD
│   │   └── services/        # Abstracciones de auth, email y pagos
│   ├── pages/
│   │   ├── api/             # Endpoints del servidor
│   │   ├── blog/            # Rutas del blog
│   │   ├── proyectos/       # Rutas de detalle de proyectos
│   │   └── ...              # Páginas principales del sitio
│   ├── utils/               # Utilidades (SEO, performance, validación, imágenes)
│   └── middleware.ts        # Middleware de headers/caché
├── supabase/
│   └── migrations/          # Esquema SQL y políticas RLS
├── astro.config.mjs
├── tailwind.config.mjs
└── package.json
```

## Development
### Flujo recomendado
1. Crea una rama por feature.
2. Agrega/modifica páginas/componentes Astro o rutas API.
3. Valida calidad:
   - `npm run type-check`
   - `npm run lint`
   - `npm run build`
4. Documenta cambios de comportamiento en README y/o comentarios.
5. Abre un pull request con:
   - alcance
   - capturas (si hay cambios visuales)
   - evidencia de pruebas

### Notas para contribuir
- Mantén responsabilidades acotadas por componente (UI vs lógica de servicio/datos).
- Prefiere abstracciones en `src/lib/services` para integraciones externas.
- Conserva estándares de SEO y accesibilidad en nuevas páginas/componentes.

## Roadmap
- Conectar formularios públicos directo al pipeline de leads en Supabase.
- Completar ciclo de pagos (webhooks, update status, historial, reembolsos).
- Reemplazar contenido mock/estático por CMS o contenido persistido en base de datos.
- Fortalecer flujos de autenticación y áreas admin protegidas por rol.
- Agregar pruebas end-to-end para los journeys críticos de conversión.
- Mejorar estrategia de service worker con versionado y fallbacks offline robustos.
- Incorporar pipeline CI (lint/type-check/test/build) para mayor confiabilidad de despliegue.

## License
Esto es personal y privado, creado y desarrollado por **JootaCee**.

## Author
Esto es personal y privado, creado y desarrollado por **JootaCee**.
