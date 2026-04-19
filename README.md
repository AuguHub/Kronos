# Kronos — Registro de tiempos

Time tracker personal. Funciona 100% offline, guarda datos en el navegador, se puede instalar como app en el celular.

## Contenido del paquete

```
kronos/
├── index.html               ← La app (antes se llamaba kronos-v2.html)
├── manifest.webmanifest     ← Configuración PWA (ícono, nombre, colores)
├── sw.js                    ← Service worker (funcionamiento offline)
├── icons/
│   ├── icon-192.png         ← Ícono PWA pequeño
│   ├── icon-512.png         ← Ícono PWA grande
│   ├── apple-touch-icon.png ← Ícono para iOS
│   └── favicon-32.png       ← Ícono pestaña del navegador
└── README.md                ← Este archivo
```

## Cómo subirlo a GitHub Pages (paso a paso)

### Desde la computadora

1. Andá a https://github.com y hacé login.
2. Tocá el botón **+** arriba a la derecha → **New repository**.
3. Poné un nombre, por ejemplo `kronos`. Dejalo **público**. No marques "Add README" porque ya tenés uno.
4. Creá el repo.
5. En la página del repo vacío, tocá **uploading an existing file**.
6. Arrastrá TODOS los archivos de esta carpeta (incluyendo la subcarpeta `icons/`). Asegurate de mantener la estructura: `icons/` tiene que seguir siendo una carpeta, no archivos sueltos.
7. Commiteá los cambios (botón verde abajo).
8. Andá a **Settings** (pestaña arriba del repo) → **Pages** (menú lateral izquierdo).
9. En "Source" elegí **Deploy from a branch**, rama `main`, carpeta `/ (root)`. Guardá.
10. Esperá 1-2 minutos. GitHub te va a mostrar la URL, algo como:
    ```
    https://TU-USUARIO.github.io/kronos/
    ```

### Desde el celular (más engorroso pero se puede)

1. Instalá la app de GitHub en el celular.
2. Creá el repo como arriba.
3. Para subir los archivos, lo más práctico es usar el navegador (Safari/Chrome) y entrar a `github.com` en modo desktop:
   - En Safari: `AA` → "Sitio web para computadora"
   - En Chrome: `⋮` → "Sitio para computadora"
4. Seguí los mismos pasos del punto 5 en adelante.

Alternativa: si tenés la app Working Copy (iOS, de pago) o Termux (Android), podés usar git normalmente.

## Cómo instalar como app en el celular

Una vez desplegada, abrí la URL en el celular:

**iOS (Safari):** tocá compartir (cuadrado con flecha) → "Agregar a pantalla de inicio". La app queda con el ícono del reloj, sin barra del navegador, y funciona offline.

**Android (Chrome):** tocá `⋮` → "Agregar a pantalla de inicio" o "Instalar app". Misma experiencia.

## Cómo actualizar la app

Si querés cambiar algo:
1. Editá los archivos en GitHub (podés hacerlo desde el navegador).
2. Los cambios se despliegan solos en 1-2 minutos.
3. En el celular, cerrá y abrí la app; puede que necesites forzar recarga una vez para que el service worker levante los nuevos archivos.

**Importante sobre el service worker:** cuando actualices el archivo `sw.js`, cambiá la línea `const CACHE_NAME = 'kronos-v2';` a `'kronos-v3'`, `'kronos-v4'`, etc. Eso fuerza a que se descarguen los archivos nuevos y no queden los viejos en caché.

## Datos y backup

- Todo se guarda en el `localStorage` del navegador del celular (no en GitHub ni en ningún servidor).
- GitHub solo hostea el código de la app, no tus datos.
- Para respaldar, usá el botón "Exportar JSON" del menú. Guardalo en iCloud/Drive/mail.
- Para restaurar, usá "Importar JSON".

## Privacidad

100% local. No hay servidor, no hay analytics, no hay tracking. Las fotos se guardan comprimidas en el navegador del celular como base64.
