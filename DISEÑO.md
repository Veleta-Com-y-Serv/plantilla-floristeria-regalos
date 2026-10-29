# Floristería y regalos: brief de diseño

Plantilla `floristeria-regalos` creada el 29/10/2026 a partir de `belleza-estetica` con `php artisan plantillas:nueva`
y rediseñada entera (fila 9 del brief de la tanda «a ancho completo»). Este fichero se queda en el repo: es lo que
lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: floristerías de barrio, tiendas de regalos y papelerías con detalle, y decoradores de eventos y
  bodas. Su cliente entra para ver qué ramos hay y cuánto cuestan, encargar uno para una fecha concreta (cumpleaños,
  boda, un tanatorio) o pedir presupuesto para un evento.
- **Qué tiene que conseguir la web**: que el encargo sea fácil. Acciones: «Lo quiero» en cada producto (WhatsApp con
  el nombre del ramo), «Encargar por WhatsApp» y el formulario de encargo con fecha de entrega.
- **Tono y estilo** (`estilo: suave`): suave, cálido y artesano, con color. Sí: el papel de seda, el cordel, los
  cubos de zinc de una floristería de verdad. No: la delicadeza blanca de `belleza-estetica` (serif fina espaciada,
  arcos, chips nude) ni el «caja centrada con tarjetas blancas».
- **Ancho completo**: todas las secciones son bandas de borde a borde; fotos a sangre en mitades 50/50 y en el
  mosaico sin márgenes; contenido hasta 90 rem con 16 px de margen lateral en móvil.

## Concepto visual

- **Paleta de ejemplo**: primario `#2f5b3c` (verde hoja: botones, bandas verdes), acento `#a85862` (rosa viejo:
  portada, cifras, contacto), fondo `#f8f1e6` (crema), texto `#26302a`. Derivados con `color-mix`: `--polvo` (rosa
  empolvado), `--salvia` (verde muy claro), `--honda` (verde oscuro del pie), `--rosa-legible` y `--hoja-legible`
  (versiones oscurecidas para texto sobre crema). El texto sobre verde y sobre rosa lo calcula `Base.astro`
  (`--c-sobre-primario`, `--c-sobre-acento`), así aguanta que el cliente cambie los cuatro colores.
- **Formas orgánicas**: ondas (`Onda.astro`) que asoman por encima de cada banda con su mismo color, en lugar de
  cortes rectos; manchas tipo pétalo (`Mancha.astro`, rellenas o de contorno) dentro de capas recortadas; fotos de
  producto e iconos con borde de pétalo (`--petalo-1..3`); el borde interior de la foto de portada y de servicios,
  ondulado; botones y etiquetas en forma de hoja (dos esquinas redondas y dos casi rectas).
- **Tipografía**: serif del sistema en cursiva para todos los títulos («Iowan Old Style», «Palatino Linotype»,
  Palatino, Georgia), grande: portada hasta 6,75 rem en escritorio y 2,75 rem en móvil, títulos de sección hasta
  4,75 rem, cifras hasta 6,5 rem. Texto en la sans del sistema. Antetítulos en mayúsculas espaciadas con una raya.
- **Ritmo de bandas**: portada rosa | foto → cinta verde → productos crema → taller foto | verde → cifras rosa →
  servicios crema | foto → encargos rosa empolvado → galería crema + mosaico a sangre → opiniones verde → preguntas
  crema → contacto rosa | salvia → pie verde hondo.
- **Cabecera**: barra crema sólida, fija arriba, flor en pétalo + nombre en cursiva, menú y botón verde; en móvil,
  menú plegable `<details>`.

## Apartados (en orden)

1. `hero`: portada partida (min. 88svh en escritorio): título enorme, párrafo, dos botones; foto a sangre a la
   derecha; `items` en una cinta verde a todo el ancho.
2. `productos` («Ramos y regalos»): titular + filtro por ocasión (botones de opción con `:has`, sin JavaScript);
   rejilla de 2 columnas (móvil y tableta) y 4 (escritorio); foto con borde de pétalo, ocasión, nombre, texto,
   precio y «Lo quiero».
3. `sobre` («El taller»): foto a sangre | banda verde con titular, cita grande (`declaracion`), párrafos y valores.
4. `cifras`: banda rosa con números enormes en cursiva (2 columnas en móvil, 4 en escritorio).
5. `servicios`: servicios con icono en pétalo y precio «desde» opcional | foto a sangre con borde ondulado.
6. `encargos`: titular + WhatsApp, pasos con el número en un pétalo verde, formulario ancho del encargo.
7. `galeria`: titular y botón a Instagram; mosaico sin márgenes de borde a borde (una grande cada cinco).
8. `opiniones`: banda verde; la primera opinión como cita gigante y las demás en tres columnas.
9. `preguntas`: titular fijo a la izquierda y acordeón a la derecha.
10. `contacto`: datos grandes y plano con borde de pétalo en rosa | formulario sobre salvia.

## Fotos (`fotos.json`, 16)

Portada (gran ramo en jarrón sobre mesa de madera), ocho productos (ramo de gerberas, caja sorpresa, ramo de novia,
centro de mesa, corona, ramo de condolencia, orquídea, kokedama), el taller (mesa de trabajo con cubos de zinc),
servicios (arco floral de boda en una finca castellana) y cinco cuadradas para la galería. Luz natural cálida, tonos
rosa viejo, verde hoja y crema, sin texto legible, sin logotipos, sin personas.

## Qué no hacer

- Volver a la caja centrada estrecha con tarjetas blancas, o a los arcos y chips nude de `belleza-estetica`.
- Cortes rectos entre bandas de distinto color sin la onda (es la seña de la plantilla).
- Fuentes externas, dependencias nuevas o JavaScript más allá del de la cabecera.
- Precios, cifras u opiniones fijos en los componentes: todo sale de `site.yaml` y los componentes pintan bien vacíos.
