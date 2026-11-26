# Invitación — Cena de Despedida Grado 11 · 2026

Invitación interactiva: sobre que se abre, birretes, cuenta regresiva, pase personal y **confirmación por WhatsApp con número consecutivo**.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La invitación (lo que ven los invitados) |
| `preview.jpg` | Imagen que muestra WhatsApp al pegar el enlace |
| `apps-script/Code.gs` | Contador de confirmaciones (va en una Hoja de Google, **no** se sube a GitHub) |

## Cómo funciona

1. El invitado escribe su nombre y toca **Confirmar por WhatsApp**.
2. La Hoja de Google le asigna el siguiente número (1, 2, 3…) y guarda su nombre con la fecha.
3. Se abre WhatsApp hacia el **302 749 9567** con el mensaje listo:
   > Yo, Ana Pérez, confirmo mi asistencia a la Cena de Despedida del Grado 11 – 2026 (viernes 27 de noviembre, 7:00 p.m., Salón de Evento Sabas).
   > Confirmación número 12.
4. Si el mismo nombre confirma dos veces, conserva su número y no se suma de nuevo.
5. La invitación muestra "Ya confirmaron N personas".

---

## Paso 1 · Crear el contador (Hoja de Google + Apps Script)

1. Crea una Hoja de Google nueva: **Confirmaciones Grado 11**.
2. **Extensiones → Apps Script**.
3. Borra lo que trae, pega todo `apps-script/Code.gs` y guarda (ícono del disquete).
4. **Implementar → Nueva implementación**:
   - Engranaje → **Aplicación web**.
   - *Ejecutar como*: **Yo**.
   - *Quién tiene acceso*: **Cualquier usuario** (sin esto los invitados no pueden confirmar).
   - **Implementar** y acepta permisos (si dice "app no verificada": **Configuración avanzada → Ir a…**).
5. Copia la **URL de la aplicación web** (termina en `/exec`).

Prueba: abre en el navegador `TU_URL?action=count`. Debe responder `{"ok":true,"total":0}`.

## Paso 2 · Configurar la invitación

En `index.html`, bloque **CONFIGURACIÓN** (cerca del final):

```js
const WHATSAPP='573027499567';                   // número que recibe los mensajes
const API='PEGA_AQUI_LA_URL_DE_APPS_SCRIPT';     // pega aquí la URL /exec
```

Las URLs del `<head>` (`og:url`, `og:image`, `twitter:image`) ya apuntan a `https://jerson0915.github.io/cena-grado11-2026/`.

## Paso 3 · Publicar en GitHub Pages

```bash
git init
git add index.html preview.jpg LEEME.md
git commit -m "Invitación cena de despedida"
git branch -M main
git remote add origin https://github.com/jerson0915/cena-grado11-2026.git
git push -u origin main
```

GitHub → **Settings → Pages → Branch: main / (root) → Save**. Queda en
`https://jerson0915.github.io/cena-grado11-2026/`

## Paso 4 · Probar antes de enviar

1. Abre el enlace en el celular y confirma con el nombre "Prueba".
2. Revisa que WhatsApp se abra hacia tu número con "Confirmación número 1".
3. **Borra la fila de prueba** en la Hoja para que el conteo real empiece en 1.
4. Pega el enlace en un chat y verifica que salga la tarjeta con la imagen.

## Si cambias Code.gs después

**Implementar → Gestionar implementaciones → lápiz → Versión: Nueva versión → Implementar**. La URL no cambia.

## Para trabajar con Claude Code en VS Code

Abre esta carpeta y pídele, por ejemplo:
- "Pega esta URL de Apps Script en la configuración de index.html"
- "Agrega un campo de acompañantes que también llegue a la hoja y al mensaje"
- "Haz commit y push a GitHub"
