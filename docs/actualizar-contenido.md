# Tutorial para actualizar contenido del portfolio

Este proyecto esta hecho con Astro. La mayor parte del contenido editable vive en
`src/data/portfolio.ts`; las paginas `.astro` leen esos datos y los muestran en
la web.

## 1. Antes de empezar

Abri una terminal en la carpeta del proyecto:

```sh
cd /home/lu/Lu/Portfolio
```

Revisa que no haya cambios pendientes que no quieras pisar:

```sh
git status
```

Si vas a probar la web en local:

```sh
npm install
npm run dev
```

El comando te va a mostrar una URL local, normalmente `http://localhost:4321`.

## 2. Archivos importantes

- `src/data/portfolio.ts`: textos, proyectos, certificados, datos de perfil,
  menu de navegacion y secciones de About.
- `src/pages/index.astro`: home. Muestra el hero y todos los proyectos.
- `src/pages/work/[slug].astro`: plantilla de cada proyecto.
- `src/pages/about.astro`: pagina About.
- `src/pages/certificates.astro`: pagina Certificates.
- `src/pages/cv.astro`: pagina CV.
- `src/pages/contact.astro`: pagina Contact.
- `public/assets/`: imagenes, PDFs y otros archivos publicos.
- `src/styles/global.css`: estilos visuales.

No edites `dist/` ni `node_modules/`. `dist/` se genera solo cuando corres el
build.

## 3. Reglas generales para editar contenido

1. Usa imagenes y PDFs dentro de `public/assets/`.
2. En el codigo, las rutas de assets empiezan con `/assets/`.
3. Para archivos nuevos conviene usar nombres simples, sin espacios:
   `mi-proyecto-cover.webp`, `cv-lucia-2026.pdf`, etc.
4. Si un texto aparece en ingles y espanol, usa este formato:

```ts
{
  en: 'English text',
  es: 'Texto en espanol'
}
```

5. Si un campo acepta HTML, cada parrafo debe ir dentro de `<p>...</p>`.
6. Despues de cada bloque dentro de arrays, deja una coma final.
7. Cada imagen deberia tener un `alt` claro y descriptivo.

## 4. Cambiar textos existentes

La mayoria de los textos estan en `src/data/portfolio.ts`.

Ejemplos:

- Hero de la home: busca `export const profile`.
- Textos de botones, titulos y etiquetas: busca `export const ui`.
- Menu principal: busca `export const navItems`.
- Proyectos: busca `export const projects`.
- Certificados: busca `export const certificates`.
- About: busca `export const aboutSections`.

Ejemplo para cambiar el texto principal de la home:

```ts
export const profile = {
  name: 'Lucía Alegria',
  role: {
    en: 'Communications specialist & UX designer',
    es: 'Especialista en comunicacion y disenadora UX'
  },
  introBody: {
    en: [
      'I help organizations create clearer,',
      'more useful digital products',
      'and people-centered experiences.'
    ],
    es: [
      'Ayudo a organizaciones a crear productos',
      'y experiencias digitales mas claras,',
      'utiles y centradas en las personas.'
    ]
  }
};
```

## 5. Agregar contenido a una seccion/proyecto existente

Los proyectos estan dentro de `projects`, en `src/data/portfolio.ts`.
Cada proyecto tiene esta forma general:

```ts
{
  slug: 'buscarte-app',
  title: 'Buscarte APP',
  summary: {
    en: 'English summary',
    es: 'Resumen en espanol'
  },
  sections: [
    // aca van las secciones internas del caso
  ]
}
```

Para agregar contenido dentro de un proyecto existente:

1. Busca el proyecto por su `slug`, por ejemplo `slug: 'bem'`.
2. Dentro de ese proyecto, busca `sections: [`.
3. Agrega un nuevo bloque al final o en la posicion donde quieras que aparezca.
4. Guarda, corre el build y revisa visualmente.

### Seccion de texto

```ts
{
  type: 'text',
  heading: {
    en: 'New section title',
    es: 'Titulo de la nueva seccion'
  },
  body: {
    en: '<p>First paragraph in English.</p><p>Second paragraph.</p>',
    es: '<p>Primer parrafo en espanol.</p><p>Segundo parrafo.</p>'
  }
}
```

### Seccion con una imagen grande

```ts
{
  type: 'media',
  heading: {
    en: 'Research board',
    es: 'Tablero de investigacion'
  },
  body: {
    en: '<p>Short explanation in English.</p>',
    es: '<p>Explicacion breve en espanol.</p>'
  },
  image: '/assets/research-board.webp',
  alt: 'Research board with project findings',
  caption: {
    en: 'Research synthesis',
    es: 'Sintesis de investigacion'
  },
  wide: true
}
```

### Seccion partida: texto + imagen

```ts
{
  type: 'split',
  heading: {
    en: 'Design decision',
    es: 'Decision de diseno'
  },
  body: {
    en: '<p>Explanation in English.</p>',
    es: '<p>Explicacion en espanol.</p>'
  },
  image: '/assets/design-decision.webp',
  alt: 'Design decision example',
  caption: {
    en: 'Final UI detail',
    es: 'Detalle final de interfaz'
  }
}
```

Si queres invertir el orden imagen/texto, agrega:

```ts
reverse: true
```

### Galeria de pantallas

```ts
{
  type: 'screens',
  heading: {
    en: 'Final screens',
    es: 'Pantallas finales'
  },
  images: [
    {
      src: '/assets/screen-1.webp',
      alt: 'Home screen'
    },
    {
      src: '/assets/screen-2.webp',
      alt: 'Search results screen'
    }
  ]
}
```

Para una galeria de cinco pantallas, podes agregar:

```ts
layout: 'five-up'
```

### Slider de imagenes

```ts
{
  type: 'slider',
  images: [
    {
      src: '/assets/slide-1.webp',
      alt: 'First slide',
      caption: {
        en: 'First slide',
        es: 'Primera lamina'
      }
    },
    {
      src: '/assets/slide-2.webp',
      alt: 'Second slide',
      caption: {
        en: 'Second slide',
        es: 'Segunda lamina'
      }
    }
  ]
}
```

### Video embed

```ts
{
  type: 'embed',
  heading: {
    en: 'Final design',
    es: 'Diseno final'
  },
  url: 'https://www.youtube.com/embed/VIDEO_ID',
  title: 'Project video'
}
```

### Columnas

```ts
{
  type: 'columns',
  columns: [
    {
      heading: {
        en: 'Insight',
        es: 'Hallazgo'
      },
      body: {
        en: '<p>English content.</p>',
        es: '<p>Contenido en espanol.</p>'
      }
    },
    {
      heading: {
        en: 'Decision',
        es: 'Decision'
      },
      body: {
        en: '<p>English content.</p>',
        es: '<p>Contenido en espanol.</p>'
      }
    }
  ]
}
```

## 6. Crear un proyecto nuevo

Para crear un nuevo proyecto que aparezca en la home y tenga su propia URL:

1. Copia tus imagenes a `public/assets/`.
2. Abre `src/data/portfolio.ts`.
3. Busca `export const projects: Project[] = [`.
4. Agrega un nuevo objeto dentro del array.

Ejemplo minimo:

```ts
{
  slug: 'nuevo-proyecto',
  sourceId: 'nuevo-proyecto',
  title: {
    en: 'New Project',
    es: 'Nuevo proyecto'
  },
  category: {
    en: 'UX/UI case study',
    es: 'Caso de estudio UX/UI'
  },
  summary: {
    en: 'Short summary in English.',
    es: 'Resumen breve en espanol.'
  },
  tags: [
    'UX/UI',
    {
      en: 'Research',
      es: 'Investigacion'
    }
  ],
  thumbnail: ['/assets/nuevo-proyecto-thumb.webp'],
  heroImage: '/assets/nuevo-proyecto-hero.webp',
  heroAlt: 'New project hero image',
  sections: [
    {
      type: 'text',
      heading: {
        en: 'Context',
        es: 'Contexto'
      },
      body: {
        en: '<p>Project context in English.</p>',
        es: '<p>Contexto del proyecto en espanol.</p>'
      }
    },
    {
      type: 'media',
      image: '/assets/nuevo-proyecto-detail.webp',
      alt: 'New project detail',
      wide: true
    }
  ]
}
```

El `slug` define la URL:

```txt
/work/nuevo-proyecto/
```

No hace falta crear una pagina nueva para cada proyecto. La plantilla
`src/pages/work/[slug].astro` genera automaticamente una pagina por cada objeto
del array `projects`.

## 7. Crear una nueva pagina o seccion principal

Si queres una seccion nueva del sitio, por ejemplo `/servicios/`, hay que crear
una pagina nueva en `src/pages/`.

Ejemplo: `src/pages/servicios.astro`

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';

const description = 'Servicios de comunicacion digital, UX y contenido.';
---

<BaseLayout active="servicios" title="Lucía Alegria - Servicios" description={description}>
  <section class="page-shell">
    <div class="page-heading">
      <p class="meta">Servicios</p>
      <h1>Servicios de comunicacion digital y UX</h1>
    </div>

    <div class="prose">
      <p>Texto de la nueva pagina.</p>
    </div>
  </section>
</BaseLayout>
```

Para agregarla al menu, edita `navItems` en `src/data/portfolio.ts`:

```ts
export const navItems = [
  { href: '/', label: { en: 'Home', es: 'Inicio' }, key: 'home' },
  { href: '/about/', label: { en: 'About', es: 'Sobre mi' }, key: 'about' },
  { href: '/servicios/', label: { en: 'Services', es: 'Servicios' }, key: 'servicios' },
  { href: '/contact/', label: { en: 'Contact', es: 'Contacto' }, key: 'contact' }
] as const;
```

Si la pagina necesita estilos nuevos, agregalos al final de `src/styles/global.css`.

## 8. Actualizar About

About usa `aboutSections` en `src/data/portfolio.ts`.

Para agregar una nueva seccion:

```ts
{
  image: '/assets/about-nueva-foto.webp',
  alt: 'Description of the new about image',
  caption: {
    en: 'Optional caption in English',
    es: 'Epigrafe opcional en espanol'
  },
  html: {
    en: '<h3>New title</h3><p>Text in English.</p>',
    es: '<h3>Nuevo titulo</h3><p>Texto en espanol.</p>'
  }
}
```

Cada nueva entrada aparece una debajo de la otra en la pagina `/about/`.

## 9. Actualizar certificados

1. Copia la imagen del certificado a `public/assets/`.
2. Abre `src/data/portfolio.ts`.
3. Busca `export const certificates = [`.
4. Agrega una entrada:

```ts
{
  src: '/assets/certificate-7.webp',
  alt: 'Certificate name and institution'
}
```

La pagina `/certificates/` muestra automaticamente todos los certificados del
array.

## 10. Actualizar CV

La pagina de CV esta en `src/pages/cv.astro`.

Actualmente hay dos versiones:

- Ingles: `Resume Lucía Alegria Talon.pdf` y `resume-lucia-alegria-talon.webp`.
- Espanol: `CV Lucía Alegria Talon.pdf` y `cv-lucia-alegria-talon.webp`.

Para actualizar un CV:

1. Reemplaza el PDF en `public/assets/`.
2. Reemplaza tambien la imagen preview `.webp`.
3. Si el navegador sigue mostrando una version anterior, cambia el numero del
   query string:

```astro
src="/assets/cv-lucia-alegria-talon.webp?v=20260801"
href="/assets/CV Lucía Alegria Talon.pdf?v=20260801"
```

Ese `?v=YYYYMMDD` fuerza a GitHub Pages y al navegador a pedir el archivo nuevo.

## 11. Actualizar contacto

El email principal esta en `profile.email`, dentro de `src/data/portfolio.ts`.

Los textos de la pagina de contacto estan en `ui`:

```ts
contactEyebrow
contactTitle
contactBody
labels
```

La imagen de contacto esta directamente en `src/pages/contact.astro`:

```astro
image="/assets/fotolu-form.webp"
src="/assets/fotolu-form.webp"
```

## 12. Validar antes de publicar

Despues de editar, corre:

```sh
npm run check
npm run build
```

Si solo queres probar visualmente:

```sh
npm run dev
```

Revisa que no haya errores y mira las paginas afectadas en el navegador.

## 13. Publicar en GitHub

Revisa que archivos cambiaron:

```sh
git status
git diff --stat
```

Agrega los cambios:

```sh
git add src/data/portfolio.ts public/assets
```

Si cambiaste otros archivos, agregalos tambien:

```sh
git add src/pages/cv.astro src/styles/global.css README.md
```

Crea el commit:

```sh
git commit -m "Update portfolio content"
```

Subi a GitHub:

```sh
git push origin main
```

El deploy de GitHub Pages se ejecuta automaticamente despues del push. Puede
tardar entre algunos segundos y pocos minutos.

## 14. Si no ves el cambio publicado

1. Espera un minuto y recarga.
2. Prueba con recarga fuerte del navegador.
3. Abre la pagina en una ventana privada.
4. Si cambiaste una imagen o PDF con el mismo nombre, agrega o actualiza
   `?v=YYYYMMDD` en la URL del asset.
5. Confirma que el cambio esta en GitHub:

```sh
git status
git log -1 --oneline
```

Si `git status` muestra `main...origin/main`, el repo local esta sincronizado.

## 15. Checklist rapido

- Puse los assets nuevos en `public/assets/`.
- Use rutas que empiezan con `/assets/`.
- Agregue texto en ingles y espanol cuando corresponde.
- Agregue `alt` a cada imagen.
- No edite `dist/` ni `node_modules/`.
- Corri `npm run check`.
- Corri `npm run build`.
- Hice commit.
- Hice push a `origin/main`.
