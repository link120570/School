# Progreso de Inglés

App para una maestra de inglés particular (grupo de 7 alumnos de 7 a 13 años).
Panel para capturar el avance mensual de cada alumno y una vista de boleta para los papás.

## Reglas del proyecto
- Todo vive en un solo archivo: `index.html` (HTML, CSS y JavaScript juntos).
- JavaScript puro. No usar React, Babel ni frameworks.
- Sin librerías externas salvo que sea indispensable; si se usa una, versión fija.
- Datos en localStorage con la clave `progreso-ingles-v1`. No cambiar la estructura sin migrar los datos existentes.
- Toda la interfaz y los textos en español de México.
- Diseño pensado primero para celular; debe verse bien en modo claro y oscuro.
- Se publica con GitHub Pages desde la rama `main`.

## Privacidad
- Solo nombre de pila y edad del alumno. Sin fotos, apellidos, escuela ni dirección.
- Nunca subir datos reales de alumnos al repositorio (es público).

## Estructura de datos
- `alumnos[]`: `id`, `nombre`, `edad`, `nivel` (Starter, A1, A2, B1), `color`, `meses[]`
- Cada mes: `mes` (AAAA-MM), `speaking`, `listening`, `reading`, `writing` (1 a 5),
  `asist`, `clases`, `tareas`, `tareasTot`, `stickers`, `temas[]`, `comentario`, `pagado`

## Link para papás
- Desde "Ver como papá" → "Compartir con papás" se genera un link `#r=<base64url>` con la boleta de un solo alumno (últimos 6 meses).
- Los datos viajan dentro del link (el `#` no llega al servidor); quien abre el link solo ve esa boleta, sin el panel.
- Al leer el link (`leerLink`) siempre validar y limpiar los datos: vienen de afuera.

## Pendiente a futuro
- Pasar a Firebase para que cada papá tenga un link fijo de su hijo que se actualice solo.
