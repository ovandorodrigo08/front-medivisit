# MediVisit – Frontend

Interfaz web del sistema **MediVisit**, para el control de visitas del **Hospital Luis A. Güemes** (Aguaray, Salta).
Proyecto de la Tecnicatura Superior en Análisis de Sistemas y Desarrollo de Software – IES N° 6.039.

- **Sitio en producción:** https://medivisit-final.vercel.app
- **Backend (API):** https://github.com/ovandorodrigo08/back-medivisit

## Funcionalidades

- Registro e inicio de sesión con **Firebase Authentication** (email y verificación por correo).
- Gestión de **pacientes** (alta, edición, baja, búsqueda).
- Registro de **visitas** con datos del visitante, parentesco, horario y **foto con la cámara**.
- Control de tiempo de visita: la hora de salida se calcula según el límite configurado, con notificaciones.
- Límite de **2 visitantes simultáneos por paciente** (el mensaje del servidor se muestra al usuario).
- Panel con **estadísticas y gráficos** (Chart.js).
- Descarga del **informe semanal en PDF**.
- Validaciones de formularios del lado del cliente.

## Tecnologías

| Parte | Tecnología |
|---|---|
| Estructura / estilos / lógica | HTML5, CSS3, JavaScript (vanilla, sin framework) |
| Autenticación | Firebase Auth 10.14.1 (versión *compat*, por CDN) |
| Gráficos | Chart.js 4.4.1 (CDN) |
| Íconos | Tabler Icons (CDN) |
| Cámara | `navigator.mediaDevices.getUserMedia` |
| Comunicación con el servidor | `fetch` a la API REST |
| Hosting | Vercel |

No hay `package.json` ni paso de *build*: es un sitio estático.

## Estructura

```
frontend/
├── index.html    # Pantallas y carga de librerías
├── script.js     # Lógica, validaciones, llamadas a la API, Firebase
├── styles.css    # Estilos
└── logo.jpeg
```

## Configuración

### URL de la API

En la parte superior de `script.js`:

```js
const API_URL = 'https://medivisit-final-1.onrender.com/api';
// Para probar con el backend local:
// const API_URL = 'http://localhost:3000/api';
```

Para desarrollo local, comentá la línea de producción y descomentá la local. **Volvé a dejar la de producción antes de subir los cambios.**

### Firebase

La configuración (`firebaseConfig`) está en `index.html`. Para usar otro proyecto:

1. Crear un proyecto en https://console.firebase.google.com
2. Activar *Authentication → Email/Password*.
3. En *Authentication → Settings → Authorized domains* agregar el dominio de Vercel.
4. Reemplazar `firebaseConfig` en `index.html`.

## Ejecutar en local

1. Levantar el backend (`npm run dev` en `back-medivisit/backend`).
2. Cambiar `API_URL` a `http://localhost:3000/api`.
3. Abrir el sitio con un servidor estático (necesario para la cámara y Firebase):

```bash
git clone https://github.com/ovandorodrigo08/front-medivisit.git
cd front-medivisit/frontend
npx serve .
# o con Python:  python -m http.server 5500
```

4. Entrar a `http://localhost:3000` o `http://localhost:5500` según el servidor elegido.

> En el backend, `FRONTEND_ORIGIN` debe coincidir con el origen desde el que se abre el front (o dejarlo sin definir para permitir todos).

## Despliegue (Vercel)

| Ajuste | Valor |
|---|---|
| Framework Preset | Other |
| Root Directory | `frontend` |
| Build Command | *(vacío)* |
| Output Directory | *(vacío)* |

Cada `push` a `master` publica automáticamente.

## Notas

- La primera petición puede tardar unos segundos si el backend en Render estaba en reposo.
- La cámara solo funciona en **HTTPS** (Vercel) o en `localhost`.

## Autor

Rodrigo Ovando y Florencia Vera – IES N° 6.039, Aguaray, Salta.
