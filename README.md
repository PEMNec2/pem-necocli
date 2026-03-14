# 📋 PEM Necoclí 2025-2035 — Sistema de Seguimiento

Plataforma web para el seguimiento del Plan Educativo Municipal de Necoclí, Urabá Antioqueño.

## Archivos del proyecto

```
pem-neclocli/
├── index.html        ← Dashboard / Tablero de indicadores
├── formulario.html   ← Formulario de registro de avances (con Google Auth)
├── netlify.toml      ← Configuración de despliegue en Netlify
└── README.md         ← Este archivo
```

---

## 🚀 Despliegue paso a paso

### Paso 1 — Subir a GitHub

1. Ve a [github.com](https://github.com) → **New repository**
2. Nombre del repo: `pem-neclocli` (o el que prefieras)
3. Visibilidad: **Public** (necesario para Netlify gratuito)
4. Haz clic en **Create repository**
5. Sube los 4 archivos (drag & drop o Git):

```bash
git clone https://github.com/TU_USUARIO/pem-neclocli.git
# Copia los 4 archivos a la carpeta
cd pem-neclocli
git add .
git commit -m "Primer despliegue PEM Necoclí"
git push origin main
```

---

### Paso 2 — Conectar con Netlify

1. Ve a [netlify.com](https://netlify.com) → **Add new site** → **Import an existing project**
2. Elige **GitHub** y autoriza el acceso
3. Selecciona el repo `pem-neclocli`
4. Configuración de build:
   - **Build command**: (dejar vacío)
   - **Publish directory**: `.` (punto)
5. Haz clic en **Deploy site**
6. Netlify te dará una URL como `https://pem-neclocli-xxxxx.netlify.app`

---

### Paso 3 — Configurar Google Sign-In (OBLIGATORIO para el formulario)

#### 3a. Crear proyecto en Google Cloud Console

1. Ve a [console.cloud.google.com](https://console.cloud.google.com)
2. Crea un nuevo proyecto: `PEM-Necoclí`
3. Busca **"APIs & Services"** → **"Credentials"**
4. Haz clic en **"Create Credentials"** → **"OAuth 2.0 Client ID"**
5. Application type: **Web application**
6. Nombre: `PEM Necoclí Web`

#### 3b. Agregar dominios autorizados

En la sección **"Authorized JavaScript origins"** agrega:
```
https://TU-SUBDOMINIO.netlify.app
http://localhost:3000   ← (opcional, para pruebas locales)
```

#### 3c. Copiar el Client ID

Copia el valor que parece:
```
123456789-abcdefghijk.apps.googleusercontent.com
```

#### 3d. Pegarlo en formulario.html

Abre `formulario.html`, línea ~165, cambia:
```javascript
const GOOGLE_CLIENT_ID = 'TU_CLIENT_ID_AQUI.apps.googleusercontent.com';
```
por tu Client ID real. Luego haz commit y push → Netlify actualiza automáticamente.

---

### Paso 4 — Configurar la Pantalla de Consentimiento OAuth

En Google Cloud Console → **OAuth consent screen**:
- User Type: **External**
- App name: `PEM Necoclí`
- Email de soporte: tu correo
- En **"Test users"**: agrega los correos de los docentes/funcionarios autorizados

> 💡 Mientras la app esté en modo "Testing", solo los usuarios agregados como testers podrán iniciar sesión. Para acceso abierto solicita la verificación de la app.

---

## 🔧 Personalización adicional

### Cambiar dominio Netlify
En Netlify → **Site settings** → **Domain management** → puedes agregar un dominio propio.

### Actualizar datos del tablero
El `index.html` usa datos de demostración. Para conectarlo al Google Sheet real, modifica la función `renderDataEntry()` para hacer fetch al mismo `API_URL`.

### Variables de entorno en Netlify (alternativa segura para el Client ID)
En **Netlify → Site settings → Environment variables** puedes guardar el Client ID y usarlo via una Edge Function, pero para este proyecto el approach directo en el HTML es suficiente.

---

## 📊 Backend (Google Apps Script)

El formulario envía datos a un Google Apps Script que guarda en Google Sheets.
El endpoint actual está en `API_URL` dentro de `formulario.html`.

Si necesitas crear uno nuevo:
1. Ve a [script.google.com](https://script.google.com)
2. Crea un nuevo proyecto vinculado a tu Google Sheet
3. Despliega como **Web App** con acceso "Anyone"
4. Reemplaza el `API_URL` en `formulario.html`

---

## 👥 Instituciones registradas (19)

CER Bobal La Playa · CER El Paraíso · CER Melilto Arriba · CER Vale Pavas · IER Caribia · IE Antonio Roldán Betancur · IER El Totumo · IER Melilto · IER Mulaticos Piedrecitas · IER Mulatos · IER San Sebastián de Urabá · IER Tulapita · IER Zapata · IER Indígena José Elías Suárez · IE Eduardo Espitia Romero · IER La Comarca · **IER Las Changas** · IER Mello Villavicencio · IER Pueblo Nuevo

---

*Mesa Educativa Municipal de Necoclí — Urabá Antioqueño, Colombia*
