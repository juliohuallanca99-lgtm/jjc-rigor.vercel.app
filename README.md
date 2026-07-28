# JJC Contratistas Generales — El Legado del Rigor

Sitio web corporativo de una sola página (landing page).

## Estructura del proyecto

```
jjc-web/
├── index.html                 ← el sitio web (44 KB, ligero y editable)
├── README.md                  ← este archivo
└── assets/
    └── img/
        ├── edinson.jpg        ← Edinson Visuña — Gerente de SSOMA
        ├── jimmy.jpg          ← Jimmy Mora — Gerente de Proyecto
        ├── humberto.jpg       ← Humberto Fernandez — Gerente de Construcción
        └── johnny.jpg         ← Johnny Villanueva — Gerente Corporativo de Operaciones
```

## Cómo subir a Vercel (vía GitHub)

1. Crea un repositorio nuevo en GitHub (por ejemplo `jjc-rigor`).
2. Sube **toda la carpeta** `jjc-web` manteniendo la estructura:
   - `index.html` en la raíz
   - la carpeta `assets/img/` con las 4 fotos
3. En Vercel, importa el repositorio.
4. Deploy automático. Vercel detecta el `index.html` y publica el sitio.

**Importante:** las fotos deben mantener la ruta `assets/img/` para que se carguen.
Si cambias el nombre de una foto, actualiza también la referencia dentro de
`index.html` (busca `assets/img/` en el código).

## Cómo cambiar una foto

Reemplaza el archivo correspondiente en `assets/img/` manteniendo el mismo
nombre (por ejemplo, para cambiar la foto de Jimmy, reemplaza `jimmy.jpg`).
No necesitas tocar el código.

## Características del sitio

- Diseño responsive (PC, laptop, tablet, celular) con menú hamburguesa en móvil
- Selector de idioma ES / EN con preferencia guardada
- Carrusel animado del equipo (Expertos del Rigor)
- 6 certificaciones ISO (9001, 14001, 45001, 50001, 37001, 37301)
- Contadores animados de estadísticas
- Paleta corporativa azul marino + dorado

## Editar textos

Todos los textos están en `index.html`. Los elementos con dos idiomas usan
atributos `data-es` (español) y `data-en` (inglés). Si cambias un texto,
actualiza ambos atributos para mantener la traducción.

## Cómo agregar una nueva reunión (PDF permanente)

1. Guarda el PDF en la carpeta `assets/pdf/` (por ejemplo `reunion-2025-04.pdf`).
2. Abre `index.html` y busca `id="reuGrid"`.
3. Copia una de las tarjetas `<div class="reu-card">...</div>` existentes y pégala.
4. En la copia, cambia:
   - La fecha del badge: `<div class="reu-badge-date">Abril 2025</div>`
   - El título y la descripción
   - La ruta del PDF en los dos lugares: `openPdf('assets/pdf/reunion-2025-04.pdf', ...)` y `href="assets/pdf/reunion-2025-04.pdf"`
5. Sube los cambios a GitHub/Vercel.

El PDF quedará visible para todos de forma permanente.

## Vista rápida (temporal)

En la sección Reuniones hay una zona para arrastrar o seleccionar un PDF y verlo
al instante. Esta vista es solo para el momento — el PDF NO se guarda ni se
publica. Para publicar una reunión de forma permanente, usa el método de arriba.

## Sistema de Reuniones (actualizado)

El sistema de Reuniones ahora usa almacenamiento en la nube (Supabase) para que
puedas subir PDFs cada semana desde la web, sin editar código.

**IMPORTANTE:** Antes de que funcione la carga de PDFs, debes configurar Supabase
una sola vez. Sigue las instrucciones en `GUIA-SUPABASE.md`.

Mientras no configures Supabase, la sección Reuniones se verá con los 12 meses
vacíos y un aviso de "almacenamiento no configurado".
