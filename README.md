# Portfolio — Álvaro García
## Instrucciones de personalización y despliegue

---

### Estructura de archivos

```
portfolio/
├── index.html          ← Inicio / Hero
├── projects.html       ← Galería de proyectos
├── skills.html         ← Habilidades & Stack
├── about.html          ← Sobre mí
├── contact.html        ← Contacto
├── css/
│   └── style.css       ← Todo el diseño (tokens, layout, componentes)
├── js/
│   ├── main.js         ← Lógica: idioma, nav, filtros, modal, formulario
│   └── layout.js       ← Nav y footer compartidos (se inyectan en cada página)
└── assets/
    ├── img/            ← Tus imágenes aquí
    ├── video/          ← Tus vídeos aquí
    └── cv-alvaro-garcia.pdf   ← Tu CV aquí
```

---

### Cómo añadir tus imágenes

#### En la página de inicio (index.html)
Busca la sección del hero y sustituye el placeholder:
```html
<!-- ANTES (placeholder) -->
<div class="placeholder placeholder--1" ...>...</div>
<img src="" alt="Render destacado" style="opacity:0;position:absolute;">

<!-- DESPUÉS -->
<img src="assets/img/tu-render-hero.jpg" alt="Render destacado">
```

#### En los proyectos (projects.html)
Cada `.project-item` tiene estos atributos de datos — edítalos:
```html
<div class="project-item"
  data-img="assets/img/loft-interior.jpg"
  data-title="Nombre del proyecto"
  data-cat="3d"          ← categoría para el filtro: 3d / art / game
  data-desc="Descripción larga que aparece en el modal."
  data-tags="3ds Max, Corona, Substance">
```
Y sustituye también el placeholder visual dentro del item:
```html
<img src="assets/img/loft-interior.jpg" alt="Loft Industrial" style="width:100%;height:100%;object-fit:cover;position:absolute;">
<!-- Borra el div.placeholder que hay encima -->
```

#### Imágenes 4K
Las imágenes se sirven directamente — puedes poner JPG/PNG a resolución máxima.
Para rendimiento web recomiendo exportar a WebP (mismo pipeline, menor peso):
```
ffmpeg -i tu-render.png -quality 92 tu-render.webp
```

---

### Cómo añadir vídeos

En cada `.project-item` añade el atributo `data-video`:
```html
<div class="project-item"
  data-video="assets/video/mi-proyecto.mp4"
  data-img="assets/img/thumbnail.jpg"
  ...>
```
Si `data-video` está presente, el modal reproduce el vídeo en lugar de mostrar la imagen.

Para la miniatura en la lista, pon el vídeo de fondo directamente:
```html
<!-- Sustituye el <img> del item por: -->
<video src="assets/video/mi-proyecto.mp4" autoplay muted loop playsinline
  style="width:100%;height:100%;object-fit:cover;position:absolute;"></video>
```

---

### Añadir un proyecto nuevo

Copia este bloque en `projects.html` dentro de `.project-list`:
```html
<div class="project-item fade-up"
  data-cat="3d"
  data-title="Nombre del proyecto"
  data-desc="Descripción completa para el modal lightbox."
  data-img="assets/img/mi-proyecto.jpg"
  data-tags="3ds Max, Corona, Substance Painter">

  <img src="assets/img/mi-proyecto.jpg"
       alt="Nombre del proyecto"
       style="width:100%;height:100%;object-fit:cover;position:absolute;">

  <div class="project-item__content">
    <div class="project-item__left">
      <div class="project-item__cat">3D / Arquitectura</div>
      <h2 class="project-item__title">Nombre del proyecto</h2>
      <p class="project-item__desc">Subtítulo corto</p>
    </div>
    <div class="project-item__arrow" aria-hidden="true">→</div>
  </div>
</div>
```

---

### Personalizar datos de contacto

En `contact.html`, edita los enlaces:
```html
<a href="mailto:TU@EMAIL.COM" class="contact__link">
<a href="https://linkedin.com/in/TU-PERFIL" ...>
<a href="https://artstation.com/TU-PERFIL" ...>
<a href="https://github.com/TU-USUARIO" ...>
```

En `js/main.js`, edita las traducciones (busca `TRANSLATIONS`):
```js
'contact.sub': 'Tu texto de disponibilidad aquí.',
```

---

### Añadir tu CV

Coloca tu PDF en:
```
assets/cv-alvaro-garcia.pdf
```
Los botones de descarga ya apuntan a esa ruta.

---

### Idioma bilingüe

El botón EN/ES en la nav alterna el idioma. Todas las cadenas están en `js/main.js`
dentro del objeto `TRANSLATIONS`. Para añadir una nueva cadena:
1. Añade la clave en ES y EN
2. En el HTML usa `data-i18n="tu.clave"` en el elemento

---

### Colores — cambiar el acento

En `css/style.css`, línea ~5:
```css
--accent: #b8955a;        ← color principal de acento
--accent-dim: rgba(184,149,90,0.15);   ← versión transparente
```
Sustitúyelos por tus colores de marca.

---

### Despliegue (hosting gratuito recomendado)

| Opción       | Pasos                                                       |
|--------------|-------------------------------------------------------------|
| **GitHub Pages** | Sube la carpeta a un repo → Settings → Pages → Deploy from branch `main` |
| **Netlify**  | Arrastra la carpeta a netlify.com/drop → URL instantánea    |
| **Vercel**   | `vercel` en la terminal dentro de la carpeta                |

El portfolio es 100% estático (HTML + CSS + JS puro), sin dependencias ni build steps.

---

### Formulario de contacto

El formulario actual muestra un mensaje de éxito simulado. Para que funcione de verdad,
las opciones gratuitas más sencillas son:

- **Formspree** — cambia el `action` del form: `<form action="https://formspree.io/f/TU-ID">`
- **EmailJS** — SDK de JS, sin backend
- **Web3Forms** — gratis hasta 250 mensajes/mes

---

*Diseño: oscuro minimalista · DM Serif Display + Inter + JetBrains Mono · Acento ocre #b8955a*
