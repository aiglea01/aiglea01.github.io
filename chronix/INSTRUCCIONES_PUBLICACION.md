# Chronix — Web pública para Google OAuth

**Estado:** paquete preparado para publicar; no está subido a GitHub ni verificado por Google.

## Ubicación correcta

GitHub del propietario ya contiene el repositorio público `aiglea01/aiglea01.github.io` con una página personal en su raíz. **No sobrescribas** `index.html` ni `DSCN3454.JPG` existentes.

Copia la carpeta `chronix/` de este paquete **tal cual** en la raíz de `aiglea01.github.io`:

```text
aiglea01.github.io/       (repositorio existente)
├── index.html           (se conserva)
├── DSCN3454.JPG         (se conserva)
└── chronix/
    ├── index.html       (presentación)
    ├── privacy.html     (privacidad)
    ├── styles.css
    └── chronix.svg
```

URLs una vez publicado GitHub Pages:
- Home: https://aiglea01.github.io/chronix/
- Privacidad: https://aiglea01.github.io/chronix/privacy.html

## Publicar con Git desde un ordenador

1. Descomprime el ZIP.
2. Ejecuta:

```bash
git clone https://github.com/aiglea01/aiglea01.github.io.git
cd aiglea01.github.io
cp -R /RUTA/DONDE/DESCOMPRIMISTE/chronix ./chronix
git add chronix/
git commit -m "Add Chronix website and privacy policy"
git push origin main
```

Si ya dispones de clon, ve a su carpeta y ejecuta `git pull --ff-only` antes de copiar.

## Publicar solo desde GitHub (sin terminal)

1. Abre https://github.com/aiglea01/aiglea01.github.io
2. En la rama `main`, crea primero el archivo `chronix/index.html` con **Add file → Create new file**. Copia el contenido del archivo `chronix/index.html` de este paquete y confirma el commit.
3. Entra en la carpeta `chronix` creada, pulsa **Add file → Upload files** y sube `privacy.html`, `styles.css` y `chronix.svg` (sin sobrescribir la página personal del directorio raíz).
4. En el repositorio, comprueba **Settings → Pages** y que la fuente de publicación sea `Deploy from a branch`, `main`, `/(root)`; si ya está funcionando, no cambies nada.
5. Abre los dos enlaces en una ventana privada y comprueba las referencias entre ambos.

## Google Cloud → Google Auth Platform

Proyecto: usa el proyecto de Google Cloud ya configurado para Chronix. **No crees un cliente nuevo si el actual ya funciona**.

1. Abre https://console.cloud.google.com/auth/branding
2. Completa nombre `Chronix`, correo de asistencia, correos del desarrollador y, en App domain:
   - Home page: `https://aiglea01.github.io/chronix/`
   - Privacy policy: `https://aiglea01.github.io/chronix/privacy.html`
   - Terms of service: opcional si la consola lo permite; si lo exige, habrá que publicar una página adicional que describa términos reales.
3. Si la consola pide "Authorized domains", prueba `aiglea01.github.io` como dominio de las páginas informativas. Si reclama propiedad, verifícala en Search Console como se explica abajo.
4. Comprueba que en **Data Access** figuran los scopes exactos usados por el backend: `openid`, `email`, `profile` y `https://www.googleapis.com/auth/calendar.readonly`. El permiso de Calendar es sensible; para uso personal puede aplicarse una excepción de verificación, pero eso no evita que Google muestre el aviso de app no verificada.
5. Comprueba que **Clients → Web application** sigue teniendo el callback HTTPS correcto de tu instancia privada. **NO lo cambies por la dirección de GitHub Pages**: GitHub Pages no atiende la respuesta OAuth de Chronix.
6. Abre https://console.cloud.google.com/auth/audience. Con audiencia `External`, una vez completados los campos requeridos, cambia el estado de `Testing` a `In production` pulsando **Publish app**.
7. Si Google solicita verificación de marca o permisos, sigue los avisos del panel. No está garantizada la aprobación de un dominio `github.io` ni de un callback bajo un dominio compartido `ts.net`. Si exige dominio propio, se necesita uno verificable.
8. En Chronix, desconecta y vuelve a conectar las cuentas de Google Calendar para renovar la concesión OAuth. Verifica con otra prueba después de 7 días.

## Verificar propiedad en Google Search Console (si se solicita)

1. https://search.google.com/search-console
2. Elige **Prefijo de URL** y escribe `https://aiglea01.github.io/` (no el dominio compartido `github.io` sin usuario).
3. En los métodos de verificación, selecciona **Archivo HTML** y descarga el archivo con el nombre que proporcione Google.
4. Sube **ese archivo a la raíz del repositorio `aiglea01.github.io`**, al lado de la página personal `index.html`, no dentro de `chronix/`. Conserva su nombre y su contenido exactos.
5. Comprueba que `https://aiglea01.github.io/NOMBRE_REAL_DEL_ARCHIVO.html` responde en el navegador y pulsa **Verificar** en Search Console.
6. Con la misma cuenta Google que es propietaria o editora del proyecto OAuth, regresa a `Branding` y comprueba la propiedad. Si Google exige verificación de un dominio diferente, usar Search Console para `aiglea01.github.io` puede ser insuficiente; ese caso requiere un dominio propio u otra solución admitida por Google.

## Seguridad y precisión

- Esta web pública **no contiene** secretos OAuth, credenciales, ni un enlace al servidor privado.
- La política menciona el correo `alvaroiglesiasavila01@gmail.com`, que aparece ya como correo propietario en la documentación publicada de Chronix. Revisa si deseas publicarlo como correo de contacto o sustituirlo antes de subirla.
- Google Pages y el servidor Chronix están separados. No actives `tailscale funnel` por este trámite.
- Mantén la configuración privada del servidor (`.env`, `TOKEN_KEY`, JSON secreto del cliente, SQLite) fuera del repositorio.
- La aplicación Chronix actualmente no enlaza esta política desde su propia pantalla de ajustes. Para verificación formal futura, conviene incluir ahí un enlace visible.
- Una autorización OAuth publicada en producción no caduca automáticamente por el período de Testing de siete días, pero puede revocarse o expirar por otros motivos.

## Referencias oficiales

- Google Branding: https://support.google.com/cloud/answer/15549049
- Google Publish status: https://support.google.com/cloud/answer/15549945
- Excepciones verificación personal: https://support.google.com/cloud/answer/13464323
- Google Search Console verificación: https://support.google.com/webmasters/answer/9008080
- GitHub Pages: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
