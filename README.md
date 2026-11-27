# Agenda de El Viso · Ayuntamiento de El Viso

Aplicación web progresiva (PWA) estática en HTML, CSS y JavaScript puro, pensada para alojarse en **GitHub Pages** y mostrar en tiempo real los eventos que se apuntan en la hoja de cálculo **Agenda de Eventos - El Viso** (Google Drive).

## Archivos del repositorio

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La aplicación completa: diseño, lectura del Excel, avisos, calendario y compartir. |
| `sw.js` | Service Worker (caché `agenda-el-viso-v4`). Red primero para la página, caché si no hay conexión. |
| `manifest.json` | Permite instalar la agenda como app en el móvil. |
| `icon-192.png`, `icon-512.png` | Iconos de la app instalada. |
| `cabecera.jpg`, `logo.jpg` | Foto de cabecera y escudo. |
| `.nojekyll` | Hace que GitHub Pages sirva los archivos tal cual, sin Jekyll. |

> Cuando cambies `index.html` u otros archivos, sube también `sw.js` con el número de versión de la caché aumentado (`v4` → `v5`) para que los móviles reciban el cambio al instante.

## Funciones

- Meses con encabezado fijo al hacer scroll.
- Una tarjeta por evento: fecha, hora, lugar, inscripción, descripción y programa desplegable.
- Avisos: **Hoy**, **Mañana**, **Esta semana** (próximos 7 días) y **En curso** (eventos de varios días ya iniciados).
- Botón **Guardar** (Google Calendar o archivo `.ics`) y botón de **compartir por WhatsApp**.
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
| `Programa` | Hitos separados por `\|` (opcional) | `18:00 h · El Belén \| 18:30 h · Alumbrado` |
| `Inscripcion` | Instrucciones o enlace (opcional) | `En el Ayuntamiento hasta el 2 de diciembre` |
| `Descripcion` | Resumen breve | `Inauguración del Belén y encendido oficial.` |

La columna `Tipo` ya no se usa: puede quedarse en la hoja sin problema.

Las filas sin título o con la fecha de inicio ilegible se ignoran; en ese caso aparece un aviso en la consola del navegador con el número de fila.
