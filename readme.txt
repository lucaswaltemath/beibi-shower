# Beibi Shower

Plataforma web para organizar listas de regalos de baby shower. Los invitados eligen y reservan regalos en tiempo real — sin regalos repetidos. Cualquier persona puede crear su propio baby shower en segundos.

**[Ver app live → beibi-shower.vercel.app](https://beibi-shower.vercel.app)**

## Features

- **Multi-sesion**: cada baby shower tiene su propia URL (`?s=kai`, `?s=emma`, etc.)
- **Landing page**: pagina de inicio para crear nuevos baby showers con stats globales en vivo
- **Vista invitados**: regalos disponibles con foto, precio y link de compra. Reserva con nombre y apellido.
- **Vista admin**: agrega, edita y elimina regalos. Libera reservas. Protegida con PIN.
- **Regalos ilimitados**: opcion para regalos que pueden ser llevados por varias personas (ropa, calcetines, etc.)
- **Personalizacion total**: nombre del bebe, color del tema (hex libre), emoji del bebe — todo desde el panel admin
- **Tiempo real**: cuando alguien reserva, todos lo ven al instante (Firebase Realtime Database)
- **PIN seguro**: hasheado con SHA-256 y guardado en Firebase, nunca en el codigo fuente
- **Logo y favicon personalizados**
- **Responsive**: funciona en celular, tablet y desktop
- **Zero dependencies**: un solo archivo HTML. Sin frameworks, sin build, sin npm install.

## Setup (5 minutos)

### 1. Crear proyecto en Firebase (gratis)

1. Ve a [console.firebase.google.com](https://console.firebase.google.com)
2. Crea un nuevo proyecto
3. Ve a **Build → Realtime Database → Create Database**
4. Elige `us-central1` y selecciona **"Start in test mode"**
5. Ve a **Project Settings → Your apps → Web (`</>`)** y registra una app
6. Copia el bloque `firebaseConfig`

### 2. Configurar la app

Abre `index.html` y reemplaza el bloque `FIREBASE_CONFIG` con tus datos:

```javascript
const FIREBASE_CONFIG = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_PROYECTO.firebaseapp.com",
  databaseURL: "https://TU_PROYECTO-default-rtdb.firebaseio.com",
  projectId: "TU_PROYECTO",
  storageBucket: "TU_PROYECTO.appspot.com",
  messagingSenderId: "TU_SENDER_ID",
  appId: "TU_APP_ID"
};
```

El PIN de admin se configura la primera vez que accedes al panel de Admin desde la app (ya no se define en el codigo).

### 3. Deploy

**Opcion A — Vercel (recomendado)**

1. Sube este repo a GitHub
2. Ve a [vercel.com/new](https://vercel.com/new) e importa el repo
3. Click en Deploy — listo

**Opcion B — Netlify**

1. Ve a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra la carpeta con `index.html`
3. Listo — te da una URL publica

## Como usar

### Crear un baby shower

1. Entra a la app (sin parametros en la URL)
2. Ingresa el nombre del bebe y presiona "Crear lista de regalos"
3. Se genera una URL unica (ej: `?s=kai`) — compartela con los invitados

### Como organizador (admin)

1. Abre tu URL de baby shower
2. Toca **Admin** e ingresa tu PIN (la primera vez te pedira crearlo)
3. Agrega regalos con nombre, foto (URL), link de compra y precio
4. Marca regalos como "ilimitados" si pueden ser llevados por multiples personas
5. Personaliza: cambia el nombre, color del tema, emoji del bebe
6. Usa el boton "Copiar" en el link para compartir con invitados

### Como invitado

1. Abre el link que te compartieron
2. Toca **?** en el header si necesitas instrucciones
3. Elige un regalo disponible → toca **"Lo llevo yo"**
4. Escribe tu nombre y apellido → confirmar
5. El regalo queda reservado para ti

## Estructura en Firebase

```
/sessions/{session-id}/
  /gifts/         → regalos de esa sesion
  /settings/      → nombre, color, emoji
  /admin/         → pinHash (SHA-256)
```

## Stack

- HTML + CSS + Vanilla JS
- Firebase Realtime Database
- Web Crypto API (SHA-256 para PIN)
- Cero dependencias de build

## Personalizacion

Desde el panel de Admin puedes cambiar:

- **Nombre del bebe**: aparece en el header y titulo del browser
- **Color del tema**: selector hex libre o color picker nativo
- **Emoji del bebe**: 12 opciones con distintos tonos de piel y estilos
- **PIN de admin**: cambialo cuando quieras

Las imagenes de los regalos se agregan via URL — puedes usar links de la tienda o subir fotos a [imgur.com](https://imgur.com) o similar.

## Nota sobre seguridad

El modo de prueba de Firebase expira en 30 dias. Para uso extendido, actualiza las reglas en Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    "sessions": {
      ".read": true,
      ".write": true
    }
  }
}
```

## Licencia

MIT — usalo, modificalo, compartelo.

---

Hecho con ❤️ por [Lucas Waltemath](https://www.linkedin.com/in/lucas-waltemath-292399104/) · [Instagram](https://www.instagram.com/lucas.waltemath)
