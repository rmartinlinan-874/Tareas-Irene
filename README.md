# Panel de tareas — Irene

App de tareas semanales, pensada para usarse desde el móvil del padre/madre y el de la hija, con los datos sincronizados entre ambos.

## Antes de publicarla: configura Firebase (una vez, gratis)

1. Ve a https://console.firebase.google.com y crea un proyecto nuevo (cualquier nombre, ej. "panel-irene").
2. En el menú lateral, entra en **Compilación → Realtime Database** → "Crear base de datos".
   - Elige una ubicación (Europa si quieres, va bien cualquiera).
   - Empieza en **modo de prueba** (lo aseguraremos después, ver más abajo).
3. Ve a **Configuración del proyecto** (el icono de engranaje) → pestaña **General** → baja hasta "Tus apps" → pulsa el icono `</>` (Web) para registrar una app web.
   - Ponle un nombre (ej. "panel-web") y pulsa "Registrar app". No hace falta Firebase Hosting.
4. Firebase te mostrará un bloque de código con un objeto `firebaseConfig`. Copia esos valores.
5. Abre el archivo `index.html` de este proyecto, busca `window.FIREBASE_CONFIG = { ... }` cerca del principio, y sustituye los valores `PEGA_AQUI_...` por los tuyos reales.

### Asegurar la base de datos (recomendado)

Por defecto, el "modo de prueba" deja la base de datos abierta a cualquiera durante 30 días. Para cerrarla a solo vosotros dos, ve a **Realtime Database → Reglas** y pon algo así:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Esto sigue siendo abierto (cualquiera con el enlace de tu app podría, en teoría, leer/escribir), pero como nadie más conocerá la URL de tu proyecto, es razonable para un uso familiar. Si más adelante quieres cerrarlo del todo, se puede añadir un login sencillo con Firebase Authentication — dímelo y te ayudo con ese paso extra.

## Publicarla como página web (GitHub Pages)

Sigue la guía paso a paso que te doy en la conversación. En resumen:
1. Crea un repositorio en GitHub y sube estos archivos (`index.html`, `README.md`).
2. Activa GitHub Pages en la configuración del repositorio, apuntando a la rama `main` y carpeta raíz `/`.
3. GitHub te dará una URL tipo `https://tu-usuario.github.io/panel-tareas-irene/` — esa es la que usaréis desde el móvil.

## Notas

- No hace falta instalar nada ni usar terminal para que la app funcione: es un único archivo HTML que carga React y Firebase desde internet.
- "Modo hija" marca casillas como propuestas (borde punteado dorado); "Modo padre" (protegido con PIN) las confirma (relleno cian). El PIN se guarda también en Firebase.
- Los datos de cada semana se guardan bajo una clave tipo `week:2026-W35`, así que el histórico de semanas anteriores se conserva.
