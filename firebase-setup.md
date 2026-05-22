# Configurar Firebase (ya tienes el proyecto creado)

## 1. Activar Email/Password Auth

1. Ve a **Build > Authentication** en el menu izquierdo
2. Click **Get started**
3. Pestaña **Sign-in method**
4. Click en **Email/Password** > Habilitar > **Save**

## 2. Crear usuarios (tu creas las cuentas)

1. En Authentication, pestaña **Users**
2. Click **Add user**
3. Pone el email y una contraseña temporal
4. Repite para cada persona que quieras que tenga acceso (~20 personas)

## 3. Actualizar reglas de seguridad de Firestore

1. Ve a **Firestore Database > Rules**
2. Borra todo y pega esto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /graffiti/{docId} {
      allow read: if request.auth != null;
      allow create, update, delete: if request.auth != null && request.auth.uid == 'feT0EwBBA6VwFyJC3lUTKfU7Ug42';
    }
  }
}
```

3. Click **Publish**

> Estas reglas significan:
> - Solo usuarios autenticados pueden VER el mapa
> - Solo TU uid (admin) puede CREAR/EDITAR/ELIMINAR grafitis

## 4. Tu UID de admin

Tu UID es: `feT0EwBBA6VwFyJC3lUTKfU7Ug42`

Ya esta configurado en `config.js`. Cuando inicies sesion con tu cuenta, automaticamente tendras acceso de administrador.

## Flujo final

| Quien | Que ve | Que puede hacer |
|-------|--------|-----------------|
| Sin login | Pantalla de login | Nada |
| Usuario registrado | Mapa con todos los puntos | Ver, zoom, hover, click |
| Admin (tu) | Mapa + panel edicion | Agregar, editar, eliminar puntos |
