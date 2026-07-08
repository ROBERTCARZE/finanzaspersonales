# Finanzas Personal

Panel privado de finanzas personales (caja diaria, compromisos, horario, pendientes,
flujo de caja y ciclo) en un solo archivo HTML, sin servidor. Los datos se guardan
localmente en el dispositivo y, si configuras Firebase, también en la nube (Firestore),
disponibles desde cualquier dispositivo.

## 1. Subir esto a GitHub

```bash
git init
git add .
git commit -m "Finanzas Personal"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

### Publicarlo como sitio web (GitHub Pages)
1. En el repo de GitHub → **Settings → Pages**.
2. En "Branch" elige `main` y carpeta `/ (root)` → **Save**.
3. En 1-2 minutos tu app quedará disponible en:
   `https://TU_USUARIO.github.io/TU_REPO/finanzas-personal.html`

Como es un solo archivo estático, también puedes abrirlo directo desde el
repositorio, subirlo a Netlify/Vercel arrastrando la carpeta, o simplemente
abrirlo en tu navegador desde el disco.

⚠️ Este repositorio debe ser **privado** si no quieres que cualquiera vea la
estructura de la app (aunque tus datos reales viven en Firestore, protegidos
por las reglas de seguridad, no en este archivo).

## 2. Conectar Firebase (para que tus datos estén siempre disponibles)

1. Crea un proyecto en [console.firebase.google.com](https://console.firebase.google.com).
2. Activa **Firestore Database** (modo producción).
3. Activa **Authentication → Sign-in method → Correo electrónico/contraseña**.
4. En **Configuración del proyecto → Tus apps → Web (`</>`)**, registra una app
   y copia el bloque `firebaseConfig`.
5. Sube las reglas de seguridad incluidas en `firestore.rules` (Firestore →
   Reglas, pega el contenido del archivo → Publicar).
6. Abre `finanzas-personal.html` en el navegador → ⚙️ **Configuración** → pega
   tu correo y el `firebaseConfig` → **Guardar y conectar**.
7. Vuelve a iniciar sesión con tu contraseña habitual: la primera vez que lo
   hagas, esa contraseña queda registrada como tu cuenta de Firebase
   (correo + contraseña). Desde otro dispositivo, usa el mismo correo y
   contraseña para ver los mismos datos.

Mientras no configures Firebase, la app sigue funcionando 100% local
(localStorage), igual que antes.

## 3. Estructura de datos en Firestore

```
usuarios/{tu_uid}/
  transacciones/{id}
  compromisos/{id}
  horario/{id}
  pendientes/{id}
  ciclos/{id}
  intimidad/{id}
  biomarcadores/{id}
  config/categorias
```

Cada usuario autenticado solo puede leer/escribir dentro de su propio
`usuarios/{uid}` — ver `firestore.rules`.

## Archivos

- `finanzas-personal.html` — la app completa (HTML + CSS + JS).
- `firestore.rules` — reglas de seguridad para Firestore.
- `.gitignore` — ignora archivos de sistema comunes.
