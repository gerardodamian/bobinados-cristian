# SERV & REP Mantenimiento

Web app del taller de bobinado y reparación de motores **SERV & REP Mantenimiento**, en Cosquín, Córdoba. Sirve para que los clientes consulten y pidan presupuesto por WhatsApp, y para promocionar el negocio.

**Web:** https://gerardodamian.github.io/bobinados-cristian/

## Qué incluye

- Portada con el logo, botón de presupuesto y botón de WhatsApp.
- Lista de servicios: bombas de agua, motores de lavarropas, amoladoras, motores domésticos, monofásicos y trifásicos, transformadores y alternadores.
- Formulario de presupuesto: arma el mensaje y abre WhatsApp listo para enviar. No usa servidor.
- Guía "¿Necesita bobinado?": orienta al cliente según el síntoma del equipo.
- Preguntas frecuentes.
- Dos sucursales con horario y botón "Cómo llegar" a Google Maps.
- Código QR, botón para compartir y botón para instalar como app (PWA, funciona sin conexión).

## Datos del negocio

| | |
|---|---|
| Casa central | San Martín 1348, Cosquín, Córdoba |
| Sucursal Pasaje | Santa Fe 454, Pasaje, Cosquín, Córdoba |
| Horario | Lunes a viernes de 9 a 13 hs |
| WhatsApp | 3541 55-2523 |

## Archivos

```
index.html            Página completa (HTML, CSS y JS en un solo archivo)
logo.png              Logo con fondo transparente
manifest.webmanifest  Datos de la app instalable
sw.js                 Service worker (modo sin conexión)
icon-192.png          Ícono de la app
icon-512.png          Ícono de la app
qr.png                QR con el enlace de la web
```

## Cómo modificar los datos

Todo se edita en el bloque `CFG` y en las listas `SERVICIOS` y `SINTOMAS`, al principio del `<script>` de `index.html`.

- **WhatsApp:** `CFG.wa` (sin `+`, con código de país) y `CFG.tel` para el botón de llamar. Si el enlace no abre bien el chat, probá agregando el `9` después del `54`.
- **Sucursales:** `CFG.sucursales`. Cada una tiene nombre (`n`), dirección (`d`) y link de Google Maps (`map`).
- **Servicios:** lista `SERVICIOS`, con título y descripción. El formulario toma las opciones de esta misma lista.
- **Guía de síntomas:** objeto `SINTOMAS`.
- **Horario:** está escrito en la sección de contacto del HTML (`id="contacto"`).
- **Mensajes de WhatsApp:** están en el script. El saludo cambia según la hora (`saludo()`).

## Publicar cambios (GitHub Pages)

```
git add <archivos modificados>
git commit -m "Descripción del cambio"
git push origin master
```

En el repo, **Settings → Pages** debe apuntar a la rama `master`, carpeta raíz.

### Actualizar la app instalada

La app instalada guarda archivos en el celular. Cada vez que cambies algo, subí el número de versión en `sw.js` para que se actualice:

```js
const C='servrep-v5'  // cambiar a servrep-v6, v7, etc.
```

## Regenerar el código QR

Si cambia la dirección de la web:

```
pip install qrcode pillow
python -c "import qrcode; q=qrcode.QRCode(border=3,box_size=12,error_correction=qrcode.constants.ERROR_CORRECT_M); q.add_data('https://gerardodamian.github.io/bobinados-cristian/'); q.make(); q.make_image(fill_color='#0e1a2b',back_color='white').save('qr.png')"
```

## Respuestas automáticas de WhatsApp

Los mensajes de bienvenida y de ausencia no se configuran en la web. Se activan en la app **WhatsApp Business**, en Herramientas para la empresa.

## Pruebas locales

Abrir la carpeta con VS Code y Live Server. El service worker y la instalación como app solo funcionan en `localhost` o con HTTPS.

## Tecnologías

HTML, CSS y JavaScript sin frameworks ni dependencias. Tipografías Barlow y Barlow Condensed desde Google Fonts.
