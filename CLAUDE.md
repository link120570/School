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
- `alumnos[]`: `id`, `token`, `nombre`, `edad`, `nivel` (Starter, A1, A2, B1), `color`, `meses[]`,
  `dias[]` ('lun'…'dom'), `horaIni`, `horaFin` (HH:MM)
- Cada mes: `mes` (AAAA-MM), `speaking`, `listening`, `reading`, `writing` (1 a 5),
  `asist`, `clases`, `tareas`, `tareasTot`, `stickers`, `temas[]`, `comentario`,
  `practica` (texto para practicar en casa), `practicaFecha` (AAAA-MM-DD), `meta` (meta para el próximo mes), `lista` ({'AAAA-MM-DD': true/false} del pase de lista)
- El pase de lista solo incluye a quien le toca ese día (o no tiene días marcados); suma o corrige `asist` según la fecha; `lista` no se sube a Firebase.
- Los logros de la boleta se calculan solos (función `logros`), no se guardan.
- La app ya no registra pagos (se quitó `pagado` con migración).

## Link para papás
- `preview.png` es la imagen que muestra WhatsApp al compartir el link (etiquetas og: en el `<head>`). Es genérica:
  el `#` no llega al servidor, así que la vista previa no puede llevar el nombre; el nombre va en el texto del mensaje.
- Desde "Ver como papá" → "Compartir con papás" se genera un link `#r=<base64url>` con la boleta de un solo alumno (últimos 6 meses).
- Los datos viajan dentro del link (el `#` no llega al servidor); quien abre el link solo ve esa boleta, sin el panel.
- Al leer el link (`leerLink`) siempre validar y limpiar los datos: vienen de afuera.

## Links fijos con Firebase
- Configuración en la constante `FIREBASE` de `index.html` (si es `null`, solo hay links de foto `#r=`).
- La maestra entra con Google. Cada alumno tiene un `token` aleatorio; su boleta (últimos 6 meses) se sube a
  Firestore en `boletas/{token}` cada vez que se guarda. El papá abre `#p=<token>` y ve solo esa boleta.
- Los datos completos siguen en localStorage; Firestore solo guarda las boletas. Con alumnos de ejemplo no se sube nada.
- Reglas de Firestore (cambiar el correo por el de la maestra):
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /boletas/{token} {
      allow get: if true;
      allow list: if false;
      allow write: if request.auth != null && request.auth.token.email == 'CORREO_DE_LA_MAESTRA'
                   && request.auth.token.email_verified;
    }
  }
}
```
