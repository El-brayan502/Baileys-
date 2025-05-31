# <div align='center'>Baileys - API de WhatsApp Web para Typescript/Javascript</div>

<div align="center"><img src="https://iili.io/2Zpjtlp.jpg"></div>

## Nota Importante

El repositorio original fue inicialmente eliminado por su creador y posteriormente fue retomado por [WhiskeySockets](https://github.com/WhiskeySockets). Basándome en esta fundación, he implementado varias mejoras e introducido nuevas características que no estaban presentes en el repositorio original. Estas mejoras buscan elevar la funcionalidad y proporcionar una experiencia más robusta y versátil.

## Instalación

Instalar en package.json:
```json
"dependencies": {
    "baileys": "github:nstar-y/bail"
}
```
o instalar en terminal:
```
npm install baileys@github:nstar-y/bail
```

Luego importa la función por defecto en tu código:
```ts 
// tipo esm
import makeWASocket from 'baileys'
```

```js
// tipo cjs
const { default: makeWASocket } = require("baileys")
```

## Características y Mejoras Añadidas
Aquí están algunas de las características y mejoras que he añadido:

- **Soporte para Envío de Mensajes a Canales**: Ahora puedes enviar mensajes a canales fácilmente.

- **Soporte para Mensajes con Botones y Mensajes Interactivos**: Se añadió la capacidad de enviar mensajes con botones y mensajes interactivos.

- **Icono de Mensaje IA**: Se añadieron configuraciones personalizables de iconos IA para mensajes.

- **Configuraciones de Foto de Perfil**: Permite a los usuarios subir fotos de perfil en su tamaño original sin recortar, asegurando mejor calidad y presentación visual.

- **Código de Emparejamiento Personalizado**: Los usuarios ahora pueden crear y personalizar códigos de emparejamiento como deseen, mejorando la conveniencia y seguridad al conectar dispositivos.

- **Correcciones de Libsignal**: Se limpiaron los logs para una salida más limpia e informativa.

Más características y mejoras serán añadidas en el futuro.

## Ejemplos de Características

### BOLETÍN/NEWSLETTER

- **Para obtener información del boletín**
``` ts
const metadata = await sock.newsletterMetadata("invite", "xxxxx")
// o
const metadata = await sock.newsletterMetadata("jid", "abcd@newsletter")
console.log(metadata)
```
- **Para actualizar la descripción de un boletín**
``` ts
await sock.newsletterUpdateDescription("abcd@newsletter", "Nueva Descripción")
```
- **Para actualizar el nombre de un boletín**
``` ts
await sock.newsletterUpdateName("abcd@newsletter", "Nuevo Nombre")
```  
- **Para actualizar la foto de perfil de un boletín**
``` ts
await sock.newsletterUpdatePicture("abcd@newsletter", buffer)
```
- **Para remover la foto de perfil de un boletín**
``` ts
await sock.newsletterRemovePicture("abcd@newsletter")
```
- **Para silenciar notificaciones de un boletín**
``` ts
await sock.newsletterMute("abcd@newsletter")
```
- **Para activar notificaciones de un boletín**
``` ts
await sock.newsletterUnmute("abcd@newsletter")
```
- **Para crear un boletín**
``` ts
const metadata = await sock.newsletterCreate("Nombre del Boletín", "Descripción del Boletín")
console.log(metadata)
```
- **Para eliminar un boletín**
``` ts
await sock.newsletterDelete("abcd@newsletter")
```
- **Para seguir un boletín**
``` ts
await sock.newsletterFollow("abcd@newsletter")
```
- **Para dejar de seguir un boletín**
``` ts
await sock.newsletterUnfollow("abcd@newsletter")
```
- **Para enviar reacción**
``` ts
// jid, id del mensaje y emoticón
// la forma de obtener el ID es copiar la URL del mensaje del canal
// Ejemplo: [ https://whatsapp.com/channel/xxxxx/175 ]
// El último número de la URL es el ID
const id = "175"
await sock.newsletterReactMessage("abcd@newsletter", id, "🥳")
```

### MENSAJES CON BOTONES Y MENSAJES INTERACTIVOS

- **Para enviar botón con texto**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Botón 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Botón 2' }, type: 1 }
]

const buttonMessage = {
    text: "Hola, es un mensaje con botones",
    footer: 'Hola Mundo',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })
```
- **Para enviar botón con imagen**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Botón 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Botón 2' }, type: 1 }
]

const buttonMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer o ruta
    caption: "Hola, es un mensaje con botones e imagen",
    footer: 'Hola Mundo',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })

```
- **Para enviar botón con video**
```ts
const buttons = [
  { buttonId: 'id1', buttonText: { displayText: 'Botón 1' }, type: 1 },
  { buttonId: 'id2', buttonText: { displayText: 'Botón 2' }, type: 1 }
]

const buttonMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer o ruta
    caption: "Hola, es un mensaje con botones y video",
    footer: 'Hola Mundo',
    buttons,
    headerType: 1,
    viewOnce: true
}

await sock.sendMessage(id, buttonMessage, { quoted: null })
```

- **Para enviar mensaje interactivo**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Respuesta Rápida",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "¡Toca Aquí!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copiar Código",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    text: "¡Hola Mundo!",
    title: "este es el título",
    footer: "este es el pie de página",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```
- **Para enviar mensaje interactivo con imagen**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Respuesta Rápida",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "¡Toca Aquí!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copiar Código",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    image: { url: "https://example.com/abcd.jpg" }, // image: buffer o ruta
    caption: "esta es la descripción",
    title: "este es el título",
    footer: "este es el pie de página",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```
- **Para enviar mensaje interactivo con video**
```ts
const interactiveButtons = [
     {
        name: "quick_reply",
        buttonParamsJson: JSON.stringify({
             display_text: "Respuesta Rápida",
             id: "ID"
        })
     },
     {
        name: "cta_url",
        buttonParamsJson: JSON.stringify({
             display_text: "¡Toca Aquí!",
             url: "https://www.example.com/"
        })
     },
     {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
             display_text: "Copiar Código",
             id: "12345",
             copy_code: "12345"
        })
     }
]

const interactiveMessage = {
    video: { url: "https://example.com/abcd.mp4" }, // video: buffer o ruta
    caption: "esta es la descripción",
    title: "este es el título",
    footer: "este es el pie de página",
    interactiveButtons
}

await sock.sendMessage(id, interactiveMessage, { quoted: null })
```

### Icono IA

```ts
// solo añade "ai: true" a la función sendMessage
await sock.sendMessage(id, { text: "Hola Mundo", ai: true })
```

### Código de Emparejamiento Personalizado

```ts
if(usePairingCode && !sock.authState.creds.registered) {
    const phoneNumber = await question('Por favor ingresa tu número de teléfono móvil:\n')
    const custom = "NSTRCODE" // debe ser de 8 dígitos, pueden ser letras o números
    const code = await sock.requestPairingCode(phoneNumber, custom)
    console.log(`Código de emparejamiento: ${code?.match(/.{1,4}/g)?.join('-') || code}`)
}
```

## Reportar Problemas
Si encuentras algún problema mientras usas este repositorio o cualquier parte del mismo, por favor siéntete libre de abrir un [nuevo issue](https://github.com/nstar-y/Bail/issues) aquí.

## Notas
Todo lo demás aparte de las modificaciones mencionadas anteriormente permanece igual que en el repositorio original. Puedes revisar el repositorio original en [WhiskeySockets](https://github.com/WhiskeySockets/Baileys)
