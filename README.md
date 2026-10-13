# Coffea — Landing Page (HTML + CSS)

Landing page estática de una sola página para la cafetería ficticia **Coffea**,
construida según el PRD de la materia Diseño UX-UI (TP4). Solo HTML5 semántico
y CSS3 — sin JavaScript, frameworks ni preprocesadores.

## Estructura

```
coffea-landing/
├── index.html
├── 404.html
├── netlify.toml
├── css/
│   ├── main.css          # importa todas las capas en orden
│   ├── tokens.css         # design tokens (colores, tipografía, espaciado)
│   ├── base.css           # reset, tipografía base, foco accesible
│   ├── layout.css         # .container y estructura general
│   ├── utilities.css      # .visually-hidden, etc.
│   └── components/        # un archivo CSS por componente BEM
│       ├── header.css
│       ├── hero.css
│       ├── categories.css
│       ├── product-card.css
│       ├── carousel.css
│       ├── promo.css
│       ├── testimonial-card.css
│       ├── newsletter.css
│       └── footer.css
└── assets/
    ├── img/
    └── icons/
```

## Cómo verlo en local

No necesita build ni instalación. Alcanza con abrir `index.html` en el
navegador, o levantar un servidor estático simple, por ejemplo:

```bash
npx serve .
```

## Cómo desplegarlo en Netlify

1. Subí esta carpeta a un repositorio en GitHub.
2. En [netlify.com](https://netlify.com) → **Add new site → Import an existing project**.
3. Conectá el repositorio. Build command: dejar vacío. Publish directory: `.`
4. Netlify toma automáticamente `netlify.toml` (headers de caché y seguridad).
5. Cada Pull Request genera un Deploy Preview; la rama `main` publica a producción.

## Decisiones y convenciones

- **BEM** en todos los componentes (`.product-card`, `.product-card__title`,
  `.testimonial-card--featured`, etc.).
- **Mobile-first**: estilos base pensados para 360 px, con `@media (min-width: …)`
  hacia 768 px (md), 1024 px (lg) y 1440 px (xl, fiel al Figma de 1920 px).
- **Design tokens** centralizados en `tokens.css`; ningún color, radio o
  tipografía está "suelto" en los componentes.
- **`@layer`** (`tokens, base, layout, components, utilities`) para controlar
  la cascada sin `!important`.
- **Interacciones sin JavaScript**:
  - Menú mobile con `<details>/<summary>`.
  - Carruseles con `scroll-snap-type: x mandatory` + flechas que son anclas
    (`<a href="#coffee-4">`) a cada tarjeta.
  - Favorito (corazón) con `<input type="checkbox">` + `<label>` y `:checked`.
  - Paginador de testimonios con anclas a cada `<figure>`.
  - Validación de newsletter 100% nativa (`type="email" required`).
  - `prefers-reduced-motion` respetado globalmente en `base.css`.
- **Accesibilidad**: skip link, landmarks (`header`, `nav`, `main`, `footer`),
  `:focus-visible` en todo elemento interactivo, `aria-label` en botones
  solo-ícono, `alt=""` en imágenes decorativas y descriptivo en las de producto.

## Pendiente / a revisar antes de la entrega final

- **Imágenes**: ya reemplazadas por fotos reales en `assets/img/` (coffee-1..4,
  dessert-1..4, hero, promo-hand, promo-beans, newsletter-beans). Los avatares
  de los testimonios usan `ui-avatars.com` (iniciales sobre color de marca) en
  vez de fotos de personas reales, para evitar problemas de licencia de imagen.
  Falta confirmar la licencia de las fotos usadas antes de publicar en
  producción si no son de stock libre.
- **`--color-star`**: no está publicado como variable en el Figma (se extrae
  del SVG del nodo 0:200); dejé un dorado estándar (`#E2B33C`) como
  placeholder — hay que confirmarlo contra el diseño real.
- **Breakpoints tablet/mobile**: el Figma solo trae el frame desktop (1920 px);
  los breakpoints `base`/`md`/`lg` de este proyecto son la propuesta de la
  sección 7 del PRD y deben validarse con el equipo de diseño antes de cerrar
  la Fase 3.
- **Typos del copy** (sección 11 del PRD): ya corregidos en este `index.html`
  ("get 15% off", "Our Products", "Our story", "Information", "Plans & pricing",
  "Sell your products"); falta unificar "Coffea" en vez de "Coffee" (ya está
  igual en este archivo — revisar que no se reintroduzca el error al traer
  contenido nuevo).
- **Moneda**: se mantuvo "Rs." (rupias) tal como en el diseño original;
  confirmar si se cambia a $ (ARS).
- **Lighthouse / W3C**: falta correr las validaciones de la sección 2 sobre
  la URL de producción de Netlify, no en local.
- **Performance**: faltan versiones AVIF/WebP de las imágenes y
  `fetchpriority="high"` fino-ajustado una vez estén los assets reales.
