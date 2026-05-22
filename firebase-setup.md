# Configurar Firebase (5 minutos, una sola vez)

## 1. Crear proyecto Firebase

1. Entra a https://console.firebase.google.com
2. Click en **Add project** (o Crear proyecto)
3. Nombre: `mapa-grafitis` (o el que quieras)
4. Desactiva Google Analytics (no lo necesitas)
5. Click **Create project**

## 2. Activar Firestore Database

1. En el menu izquierdo: **Build > Firestore Database**
2. Click **Create database**
3. Elige **Start in test mode** (modo prueba)
4. Elige ubicacion (cualquiera, ej: `nam5 (us-central)`)
5. Click **Enable**

## 3. Configurar reglas de seguridad

1. En Firestore Database, ve a la pestaña **Rules**
2. Pega esto y guarda:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /graffiti/{docId} {
      allow read: if true;
      allow create, update, delete: if true;
    }
  }
}
```

> Nota: allow write publico es seguro para este proyecto (datos de juego, no sensibles). Si necesitas mas seguridad, avisame.

## 4. Obtener configuracion

1. Ve al icono de engranaje > **Project settings**
2. En la pestaña **General**, baja hasta **Your apps**
3. Click en el icono **</>** (Web) para agregar una app web
4. Nombre: `mapa` (sin Firebase Hosting)
5. Registra y **copia el objeto `firebaseConfig`** que aparece
6. Pega esos valores en `config.js`:

```js
firebase: {
    apiKey: "AIzaSy...",
    authDomain: "mapa-grafitis.firebaseapp.com",
    projectId: "mapa-grafitis",
    storageBucket: "mapa-grafitis.appspot.com",
    messagingSenderId: "000000000000",
    appId: "1:000000000000:web:..."
}
```

## 5. Probar

Abre `index.html` en tu navegador. Los puntos se guardan automaticamente en Firestore y todos los visitantes los ven al instante.

## 6. Acceso admin

Para agregar/editar/eliminar puntos, usa la URL con la clave:

```
https://tusitio.com/?admin=grafiti2025
```

El modo admin:
- **Click en el mapa** = agregar nuevo grafiti
- **Click en marcador existente** = ver popup con botones editar/eliminar
- **Hover en marcador** = tooltip con botones editar/eliminar
