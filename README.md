# Kronos v3 — Registro de tiempos

Personal time tracker. Offline-first PWA. Datos en el navegador (no en GitHub).

## Contenido del paquete

```
kronos-v3/
├── index.html               ← La app (kronos-v3.html renombrado)
├── manifest.webmanifest     ← Config PWA
├── sw.js                    ← Service worker (CACHE_NAME = 'kronos-v3')
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   ├── apple-touch-icon.png
│   └── favicon-32.png
└── README.md
```

## Deploy a GitHub Pages — paso a paso

### Si es la primera vez (no tenés repo)

1. Andá a https://github.com y hacé login.
2. Botón **+** arriba a la derecha → **New repository**.
3. Poné un nombre, ej `kronos`. Dejalo **público**. No marques nada extra.
4. Crear repo.
5. En la página del repo vacío: **uploading an existing file**.
6. Arrastrá TODOS los archivos del paquete manteniendo la estructura (la carpeta `icons/` tiene que seguir siendo una carpeta).
7. Commit changes.
8. Settings → Pages → Source: `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.
9. Esperá 1-2 minutos. Tu URL: `https://TU-USUARIO.github.io/kronos/`

### Si ya tenés el repo de una versión anterior (v2)

1. Entrá al repo.
2. Borrá los archivos viejos: `index.html`, `manifest.webmanifest`, `sw.js`, y los íconos.
   - O directamente: tocá cada archivo → ícono del basurero → commit.
3. Subí los archivos nuevos: **Add file** → **Upload files** → arrastrá todo el contenido del nuevo paquete.
4. Commit changes.
5. Esperá 1-2 minutos. Tu URL es la misma de antes.
6. **En el celular**: cerrá la app, abrila de nuevo, y forzá recarga si te aparece la versión vieja (el `CACHE_NAME` cambió a `kronos-v3`, así que el service worker debería detectar el cambio y traer los archivos nuevos automáticamente).

## Cómo instalarla en el celular

Una vez desplegada, abrí tu URL en el celular:

- **iOS (Safari):** botón compartir → "Agregar a pantalla de inicio".
- **Android (Chrome):** `⋮` → "Agregar a pantalla de inicio" o "Instalar app".

Queda con el ícono del reloj, sin barra del navegador, funciona offline.

## Migrar tus datos desde v2

Importante: v3 usa claves de localStorage diferentes (`kronos.records.v3`), así que **no va a leer automáticamente** los registros de v2.

Para traer tu historial:

1. Abrí la URL de v2 que venías usando (o la versión local si la tenés).
2. Menú → Exportar JSON. Guardá el archivo.
3. Abrí la URL nueva de v3.
4. Menú → Importar JSON → elegí el archivo.
5. Te pregunta si fusionar o reemplazar. Como en v3 todavía no tenés nada, cualquiera de las dos sirve.

Tus 246 registros viejos se cargan sin etiquetas, productividad ni alarmas (esos campos son nuevos de v3). Podés enriquecerlos desde el editor cuando quieras, o simplemente dejarlos y empezar a usar las funciones nuevas en registros nuevos.

## Notas técnicas

- **CACHE_NAME:** está en `'kronos-v3'`. Cuando armemos v4, hay que cambiarlo a `'kronos-v4'` para que el service worker descarte el caché viejo y traiga los archivos nuevos. Sin ese cambio, los usuarios verían la versión vieja cacheada.
- **Storage:** todo en localStorage, claves `kronos.records.v3`, `kronos.active.v3`, `kronos.prefs.v3`, `kronos.reflections.v3`.
- **Privacidad:** GitHub solo aloja el código. Tus registros viven en el navegador del dispositivo donde usás la app. Nadie que mire tu repo público ve tus datos.

## Si algo sale mal

- **La app no aparece tras desplegar:** esperá 2-3 minutos más, GitHub Pages a veces tarda. Refrescá con Ctrl+F5 (desktop) o cerrá y abrí la pestaña (mobile).
- **Ves la versión vieja en el celular:** en iOS desde Safari, `AA` → "Configuración del sitio web" → borrar datos. En Android, `⋮` → Información del sitio → Borrar y restablecer. Después volvé a entrar a la URL.
- **El service worker no actualiza:** abrí la app en una pestaña incógnita para verificar que la nueva versión sí está desplegada. Si está, es problema de caché en tu sesión normal — borrar datos del sitio resuelve.
