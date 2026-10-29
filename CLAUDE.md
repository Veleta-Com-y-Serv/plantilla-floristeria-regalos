# Plantilla «Floristería y regalos» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **suave**.
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = verde hoja, acento = rosa viejo, fondo = crema, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…, y calcula `--c-sobre-primario`/`--c-sobre-acento`, el color de texto legible encima) y Tailwind los expone como `bg-primario`, `text-acento`… Los tonos derivados están en `src/styles/global.css` con `color-mix` (`--polvo` rosa empolvado, `--salvia` verde muy claro, `--honda` verde oscuro del pie, `--rosa-legible`, `--hoja-legible`).
- **Bandas**: cada sección es una banda a todo el ancho (`.banda` + `banda--crema|polvo|salvia|hoja|rosa|honda`), que fija `--banda` (fondo) y `--tinta` (texto). `src/components/ui/Onda.astro` pinta la onda orgánica que asoma por encima de una banda con su mismo color; `Mancha.astro`, las manchas decorativas (dentro de una capa `.deco` recortada); `Seccion.astro` junta banda, onda y contenedor de 90 rem. Las partidas 50/50 a sangre usan `.celdas`, `.celda--izq`, `.celda--der` y `.celda-foto`.
- **Tipografías y aspecto general**: `src/styles/global.css` (serif cursiva del sistema para títulos, sans del sistema para el texto; botones en forma de hoja `.btn`/`.btn-sec`, `.antetitulo` con raya, fotos con borde de pétalo `.petalo-1..3`, cabecera `.cabecera--hoja` y pie `.pie--hoja`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Las fotos de la demo se generan a partir de `fotos.json`; mientras una foto `/fotos/x.jpg` no exista, `Imagen.astro` usa su respaldo `/placeholders/x.svg`. Las fotos nuevas del cliente van en `public/fotos/`.
- **Personas**: si algún apartado añade `personas[].foto`, usa la silueta `/placeholders/persona.svg` salvo que el cliente aporte su foto. No se generan caras.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = flor en un pétalo + nombre en cursiva.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. `hero` y `contacto` son obligatorias.
- `hero` → `src/components/secciones/hero.astro` (portada partida: color | foto a sangre, y cinta verde con `items`)
- `productos` → `productos.astro` (ramos y regalos por ocasión, con filtro)
- `sobre` → `sobre.astro` (el taller: foto a sangre | banda verde con cita grande y valores)
- `cifras` → `cifras.astro` (banda rosa con números grandes; sin `items` no se pinta)
- `servicios` → `servicios.astro` (servicios con icono | foto a sangre)
- `encargos` → `encargos.astro` (pasos y formulario de encargo con fecha de entrega)
- `galeria` → `galeria.astro` (mosaico de borde a borde)
- `opiniones` → `opiniones.astro` (banda verde, la primera opinión en grande)
- `preguntas` → `preguntas.astro` (acordeón `details/summary`; sin preguntas no se pinta)
- `contacto` → `contacto.astro` (datos y plano en rosa | formulario)
- Diseño extra para apartados nuevos: `texto` (genérico).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. **Precios siempre como cadena** (`precio: "35 €"`, `precio: "desde 120 €"`); precio vacío = no se muestra.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para agrupar productos usa el campo `categoria` (la ocasión), no listas anidadas. Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Apartado nuevo**: añade `secciones.<id-nuevo>` en `site.yaml` con `tipo:` igual al diseño que quieras (`texto`, `productos`, `servicios`, `cifras`, `preguntas`, `galeria`…). Si ninguno sirve, crea `src/components/secciones/<id>.astro` copiando la estructura de uno existente (`seccion(Astro.props.id)`, `Seccion` con su `banda`, `Titular`). `src/pages/index.astro` lo recoge solo: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (el filtro de productos funciona sin JavaScript), 16 px de margen lateral (`.contenedor`), bandas a todo el ancho, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Nunca inventes precios, cifras, opiniones ni datos que el cliente no haya dado: deja el campo vacío o la lista vacía (los componentes lo ocultan).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.imagen`: foto de la mitad derecha (vertical 3:4 queda mejor; sin foto, el título va centrado). `hero.items`: frases cortas de la cinta verde (solo `titulo`). `hero.cta_secundario` opcional.
- `productos.productos[]`: `{ nombre, texto, precio, categoria, imagen, destacado }`. `categoria` es la ocasión; con más de una salen los botones de filtro («Todo» y cada ocasión). `destacado: true` pone la etiqueta `etiqueta_destacado` (por defecto «Favorito»). Cada producto lleva un enlace `boton` (por defecto «Pedir») que abre WhatsApp con el nombre del producto o, sin WhatsApp, va a encargos. `productos.nota` y `productos.cta` opcionales.
- `sobre.declaracion`: cita grande. `sobre.texto`: párrafos separados por una línea en blanco. `sobre.items`: valores (`titulo`, `texto`, `icono`). `sobre.imagen`, `sobre.cta`.
- `cifras.items[]`: `titulo` = el número («30», «+1.200»), `texto` = qué significa. Sin items no se pinta.
- `servicios.items[]`: `{ titulo, texto, icono, precio }` (precio opcional: «desde 19 € a la semana», «Consultar»). `servicios.imagen`, `servicios.cta`.
- `encargos.items`: pasos. `encargos.cta`: botón de WhatsApp (si su `url` está vacía usa `contacto.whatsapp`). `encargos.formulario_titulo`, `encargos.boton` (texto del botón del formulario), `encargos.nota`. Las ocasiones del formulario salen de las `categoria` de los productos.
- `galeria.galeria`: rutas de fotos cuadradas (la 1.ª y cada cinco salen en grande; 5 o 10 quedan mejor). `galeria.cta` opcional (enlace al perfil de Instagram).
- `opiniones.testimonios[]` (`texto`, `autor`) y `opiniones.nota`. Sin testimonios, la sección no se pinta.
- `contacto.imagen`: plano que enlaza a mapas. `contacto.boton`: texto del botón del formulario.
