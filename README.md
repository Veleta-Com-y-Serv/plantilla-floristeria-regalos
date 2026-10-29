# Plantilla NoExpertise · Floristería y regalos

Web suave y a todo color para floristerías y tiendas de regalos, con ramos por ocasión y encargos.

- Sectores: floristeria, regalos, papeleria, decoracion-eventos. Estilo: suave. Plan mínimo: gratis.
- Secciones: hero, productos, sobre, cifras, servicios, encargos, galeria, opiniones, preguntas, contacto (más el diseño `texto` para apartados nuevos).
- Diseño a ancho completo: bandas de borde a borde (rosa viejo, verde hoja, crema y rosa empolvado) unidas por ondas orgánicas, portada partida con foto a sangre, partidas 50/50 a sangre, mosaico de galería sin márgenes y pie verde con columnas. Fotos de producto con borde de pétalo; títulos en serif cursiva grande.
- Campos propios: `productos[]` (nombre, texto, precio, categoria = ocasión, imagen, destacado) con filtro por ocasión sin JavaScript; `sobre.declaracion`; `cifras.items`; `servicios.items[].precio`; `encargos.formulario_titulo` y formulario de encargo con fecha de entrega, recogida o envío y mensaje para la tarjeta.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`Florist`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos de la demo en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
