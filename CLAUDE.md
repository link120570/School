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

## Pendiente a futuro
- Pasar a Firebase para que cada papá tenga un link fijo de su hijo que se actualice solo.
