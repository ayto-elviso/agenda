# Agenda Pública de Eventos · Ayuntamiento de El Viso

Aplicación web progresiva (PWA) estática en HTML, CSS y JavaScript puro diseñada para alojarse en **GitHub Pages** y mostrar en tiempo real los eventos publicados en la hoja de cálculo **Agenda de Eventos - El Viso**.

## Archivos del repositorio

- `index.html`: Aplicación web completa (estructura, estilos, registro del Service Worker y lectura de Google Sheets).
- `sw.js`: Service Worker con caché versionada (`agenda-el-viso-v2`) y estrategia *Network-First* para que los cambios en la web se apliquen al instante cuando haya conexión y funcione sin conexión.
- `manifest.json`: Manifiesto PWA para permitir instalar la agenda como aplicación en móviles.
- `.nojekyll`: Indica a GitHub Pages que sirva los archivos estáticos directamente sin pasar por Jekyll.
- `README.md`: Documentación básica de mantenimiento y estructura de datos.

## Estructura de la hoja de cálculo (`Eventos`)

La web lee la pestaña `Eventos` de Google Sheets esperando las siguientes columnas:

| Columna | Descripción | Ejemplo |
|---|---|---|
| `Tipo` | Relevancia visual (`Pequeño`, `Mediano`, `Grande`) | `Mediano` |
| `Emoji` | Icono representativo del acto | `🎄` |
| `Titulo` | Nombre del evento | `INAUGURACIÓN DEL ALUMBRADO NAVIDEÑO Y EL BELÉN` |
| `Fecha_Inicio` | Fecha de inicio (`AAAA-MM-DD`) | `2026-12-04` |
| `Fecha_Fin` | Fecha de finalización (`AAAA-MM-DD`) | `2026-12-04` |
| `Hora` | Hora de inicio o tramo horario | `18:00 h` |
| `Lugar` | Ubicación del evento (opcional) | `Plaza de la Constitución` |
| `Programa` | Hitos horarios separados por `|` (opcional) | `18:00 h · El Belén | 18:30 h · Alumbrado` |
| `Inscripcion` | Instrucciones o enlace de inscripción (opcional) | `En el Ayuntamiento hasta el 2 de diciembre` |
| `Descripcion` | Resumen breve de la actividad | `Inauguración del Belén y encendido oficial.` |
