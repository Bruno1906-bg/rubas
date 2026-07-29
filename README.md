☁️ rubas — Despliegue en la Nube
**Vercel · TypeScript · Node.js · Express**

API serverless en TypeScript (Express + Firebase Admin + JWT) desplegada como **PaaS en Vercel**, con integración continua directamente desde GitHub.

🌐 **URL de Producción:** https://rubas-7vv3-xi.vercel.app

🩺 **Healthcheck:** https://rubas-7vv3-xi.vercel.app/health

📝 **Documentacion en word y ejercicios en postman** [U4A2_Mashup_Despliegue_Nube_CICD.docx](https://github.com/user-attachments/files/30489963/U4A2_Mashup_Despliegue_Nube_CICD.docx)

---

## 📌 Tabla de Contenidos
- [Stack de Despliegue](#-stack-de-despliegue)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Variables de Entorno](#-variables-de-entorno)
- [Proceso de Despliegue](#-proceso-de-despliegue)
- [Evidencia del Despliegue](#-evidencia-del-despliegue)
- [CI/CD](#-cicd)
- [Instalación y Uso Local](#-instalación-y-uso-local)
- [Seguridad](#-seguridad)

---

## 🚀 Stack de Despliegue

| Elemento | Valor |
|---|---|
| Plataforma | Vercel (PaaS) |
| Modelo | Serverless (`@vercel/node`) |
| Entry point | `src/server.ts` |
| Build | `tsc` |
| Start (local) | `node dist/server.js` |
| Rama conectada | `main` |
| Dominio | `*.vercel.app` |

Configuración en [`vercel.json`](./vercel.json): todas las rutas (`/(.*)`) se reescriben hacia `src/server.ts`, que actúa como handler serverless único.

---

## 📂 Estructura del Proyecto

```
rubas/
├── src/                  # Código fuente (TypeScript)
│   └── server.ts         # Punto de entrada / handler serverless
├── .gitignore             # Excluye .env, claves y artefactos de build
├── package.json
├── package-lock.json
├── tsconfig.json
├── vercel.json             # Configuración del motor Serverless de Vercel
└── README.md
```

⚠️ `.env`, `*.key`, `private.key`, `dist/` y `.vercel` **no** se versionan — ver [Seguridad](#-seguridad).

---

## 🔑 Variables de Entorno

Ninguna credencial vive en el código ni en el repositorio.

```bash
cp .env.example .env
# completar los valores reales
```

| Variable | Descripción |
|---|---|
| `JWT_SECRET` / claves RSA | Firma y verificación de tokens |
| Credenciales Firebase Admin | Conexión a Firestore |
| Otras claves de servicios externos | Integraciones consumidas por la API |

En producción estas mismas variables se cargan en **Vercel → Project Settings → Environment Variables**. Vercel permite subir el archivo `.env` completo en lugar de capturar variable por variable.

---

## 📦 Proceso de Despliegue

| Paso | Descripción |
|---|---|
| 1 | Crear `.gitignore` en la raíz **antes** del primer commit |
| 2 | Subir el proyecto a GitHub en la rama `main` |
| 3 | Importar el repositorio `rubas` desde el dashboard de Vercel |
| 4 | Cargar las variables de entorno en la sección *Environment Variables* |
| 5 | Disparar el despliegue: Vercel instala dependencias y ejecuta el build (`tsc`) |
| 6 | Verificar el endpoint `/health` en el dominio `*.vercel.app` publicado |

También puede desplegarse directo a producción desde la CLI:

```bash
vercel --prod
```

---

## 🔄 CI/CD

Cada `push` a `main` dispara automáticamente un nuevo build y despliegue en Vercel (integración y despliegue continuo), sin pasos manuales adicionales.

---

## 💻 Instalación y Uso Local

```bash
git clone https://github.com/Bruno1906-bg/rubas.git
cd rubas
npm install
cp .env.example .env   # completar variables
npm run dev
```

---

## 🔐 Seguridad

- Las credenciales y claves privadas nunca se suben al repositorio — están listadas en `.gitignore` desde el primer commit.
- El servidor no depende de un puerto fijo en el código; en el entorno serverless de Vercel el runtime gestiona el enrutamiento por handler.
- CORS debe restringirse en producción a los orígenes reales del frontend (nunca dejarse abierto como en desarrollo).
- `.env.example` documenta las variables necesarias sin exponer valores reales.

---

> Lo kiero mucho profe Julián <3 fue un gusto tenerlo como maestro
>
> <img width="236" height="231" alt="perrito" src="https://github.com/user-attachments/assets/3deae381-91c2-41e1-8001-b43bc93e3546" />
