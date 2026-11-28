# Agenda de El Viso · Ayuntamiento de El Viso

Aplicación web progresiva (PWA) estática en HTML, CSS y JavaScript puro, pensada para alojarse en **GitHub Pages** y mostrar en tiempo real los eventos que se apuntan en la hoja de cálculo **Agenda de Eventos - El Viso** (Google Drive).

## Archivos del repositorio

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La aplicación completa: diseño, lectura del Excel, avisos, calendario y compartir. |
| `sw.js` | Service Worker (caché `agenda-el-viso-v6`). Red primero para la página, caché si no hay conexión. |
| `manifest.json` | Permite instalar la agenda como app en el móvil. |
| `icon-192.png`, `icon-512.png` | Iconos redondos con fondo transparente (uso normal: ordenador, accesos directos). |
| `icon-maskable-192.png`, `icon-maskable-512.png` | Iconos cuadrados a sangre con fondo blanco y el escudo centrado (zona segura del 80 %). Android los recorta en círculo; son los que se ven en el móvil. **No deben tener fondo transparente.** |
| `apple-touch-icon.png` | Icono para «Añadir a pantalla de inicio» en iPhone (fondo opaco). |
| `cabecera.jpg` | Foto de cabecera. |
| `escudo.png` | Escudo de la cabecera, ya centrado y con el tamaño correcto dentro del círculo. |
| `logo.jpg` | Escudo original (ya no lo usa la web; se conserva como archivo de origen). |
| `.nojekyll` | Hace que GitHub Pages sirva los archivos tal cual, sin Jekyll. |

> Cuando cambies `index.html` u otros archivos, sube también `sw.js` con el número de versión de la caché aumentado (`v6` → `v7`) para que los móviles reciban el cambio al instante.

## Funciones

- Meses con encabezado fijo al hacer scroll.
- Una tarjeta por evento: fecha, hora, lugar, inscripción, descripción y programa desplegable.
- Avisos: **Hoy**, **Mañana**, **Esta semana** (próximos 7 días) y **En curso** (eventos de varios días ya iniciados).
- Las direcciones web (con o sin `https://`), los correos y los enlaces de inscripción escritos en la descripción, el programa o la inscripción se convierten en enlaces pulsables.
- Botón **Ver cartel** (si el evento tiene cartel) que lo abre a pantalla completa.
- Botón **Guardar** (Google Calendar o archivo `.ics`) y botón de **compartir**: abre el menú del móvil (WhatsApp, Telegram, SMS…) con un mensaje de texto con emojis y toda la información del evento. Termina con un único enlace a la agenda. Si el dispositivo no lo permite, copia el texto.
- Se guarda el último listado en el móvil: si no hay cobertura, se muestra con el aviso "Sin conexión".
- Los títulos escritos todo en mayúsculas se muestran con mayúscula inicial por palabra. Se puede desactivar con `NORMALIZE_UPPERCASE_TITLES = false` en `index.html`.

## Estructura de la hoja de cálculo (`Eventos`)

La web lee la pestaña `Eventos` (la hoja debe estar compartida como «cualquiera con el enlace puede ver»). Columnas:

| Columna | Descripción | Ejemplo |
|---|---|---|
| `Emoji` | Icono representativo del acto | `🎄` |
| `Titulo` | Nombre del evento | `Inauguración del alumbrado navideño y el Belén` |
| `Fecha_Inicio` | Fecha de inicio (`AAAA-MM-DD`) | `2026-12-04` |
| `Fecha_Fin` | Fecha de fin (`AAAA-MM-DD`); si se deja vacía, es el mismo día | `2026-12-04` |
| `Hora` | Hora de inicio o tramo (`18:00 a 20:00 h`) | `18:00 h` |
| `Lugar` | Ubicación (opcional) | `Plaza de la Constitución` |
| `Programa` | Una actividad por línea (`Alt+Enter` dentro de la celda), o separadas por `\|` (opcional). Se muestran como lista con puntos | `18:00 h · El Belén` ↵ `18:30 h · Alumbrado` |
| `Inscripcion` | Instrucciones o enlace (opcional) | `En el Ayuntamiento hasta el 2 de diciembre` |
| `Descripcion` | Resumen breve. Se muestra dividido en párrafos: uno por frase y uno por cada salto de línea | `Inauguración del Belén y encendido oficial.` |
| `Cartel` | Enlace al cartel del evento (opcional). Aparece el botón «Ver cartel» | `https://drive.google.com/file/d/…/view` |

### Carteles

1. Sube el cartel (mejor JPG o PNG) a una carpeta de Google Drive compartida como **«Cualquier persona con el enlace: Lector»**.
2. Copia el enlace del archivo y pégalo en la columna `Cartel` de esa fila **como texto** (que se vea `https://drive.google.com/...`, no como «chip» de archivo).
3. También valen un enlace `https://` a una imagen o el nombre de un archivo subido al repositorio (por ejemplo `carteles/belen.jpg`).

Si la columna `Cartel` no existe o está vacía en una fila, el botón no aparece.

La columna `Tipo` ya no se usa: puede quedarse en la hoja sin problema.

Las filas sin título o con la fecha de inicio ilegible se ignoran; en ese caso aparece un aviso en la consola del navegador con el número de fila.
