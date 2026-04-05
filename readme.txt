# 🎁 Baby Shower Registry

Una app web minimalista para organizar la lista de regalos de un baby shower. Los invitados eligen y reservan regalos en tiempo real — sin regalos repetidos.

**[Ver demo live →](TU_URL_DE_VERCEL)**

![Baby Shower Registry Preview](preview.png)

## ✨ Features

- **Vista invitados**: ven los regalos disponibles con foto, precio y link de compra. Reservan con un click.
- **Vista admin**: agrega, edita y elimina regalos. Libera reservas. Protegida con PIN.
- **Tiempo real**: cuando alguien reserva, todos lo ven al instante (Firebase Realtime Database).
- **Responsive**: funciona perfecto en celular, tablet y desktop.
- **Zero dependencies**: un solo archivo HTML. Sin frameworks, sin build, sin npm install.

## 🚀 Setup (5 minutos)

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

También cambia el PIN de admin:

```javascript
const ADMIN_PIN = "1234"; // Cámbialo por tu PIN secreto
```

### 3. Deploy

**Opción A — Vercel (recomendado)**

1. Sube este repo a GitHub
2. Ve a [vercel.com/new](https://vercel.com/new) e importa el repo
3. Click en Deploy — listo

**Opción B — Netlify**

1. Ve a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastra la carpeta con `index.html`
3. Listo — te da una URL pública

**Opción C — Terminal**

```bash
npx vercel
```

## 📖 Cómo usar

### Como organizador (admin)

1. Abre la app y toca **Admin**
2. Ingresa tu PIN
3. Agrega regalos con nombre, foto (URL), link de compra y precio
4. Comparte el link con los invitados

### Como invitado

1. Abre el link que te compartieron
2. Elige un regalo disponible → toca **"Lo llevo yo"**
3. Escribe tu nombre → confirmar
4. El regalo queda reservado para ti

## 🛠 Stack

- HTML + CSS + Vanilla JS
- Firebase Realtime Database
- Cero dependencias de build

## 📝 Personalización

Puedes cambiar el título y subtítulo editando estas variables en `index.html`:

```javascript
const PAGE_TITLE = "Baby Shower";
const PAGE_SUBTITLE = "Lista de Regalos";
```

Las imágenes de los regalos se agregan via URL — puedes usar links de la tienda o subir fotos a [imgur.com](https://imgur.com) o similar.

## ⚠️ Nota sobre seguridad

El modo de prueba de Firebase expira en 30 días. Para uso extendido, actualiza las reglas en Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    "gifts": {
      ".read": true,
      ".write": true
    }
  }
}
```

Esto mantiene la base de datos abierta solo para el nodo `gifts`.

## 📄 Licencia

MIT — úsalo, modifícalo, compártelo.

---

Hecho con ☕ por [Lucas Waltemath](https://linkedin.com/in/TU_LINKEDIN)
