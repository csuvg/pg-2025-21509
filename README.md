# 🌱📋 Santa Ana — Plataforma de Formularios Adaptables (PG-2025-21240)

## Descripción
Plataforma compuesta por una **API (NestJS + PostgreSQL)** y una **app móvil (React Native + Expo)** para crear, llenar y centralizar formularios adaptables en el Ingenio Azucarero. Soporta **captura offline-first**, **sincronización idempotente** y consolidación de datos en **JSONB** para análisis y trazabilidad.

Responde a la necesidad de digitalizar procesos agroindustriales ante el crecimiento de la demanda alimentaria, optimizando recursos y mejorando la toma de decisiones con datos precisos. Estudios reportan hasta **+30%** en productividad y **−15–20%** en uso de insumos con la adopción de tecnologías digitales.

## 🧰 Tecnologías Utilizadas
- 🧠 Backend: Node.js 20, NestJS 10, TypeScript 5, Swagger/OpenAPI
- 🗄️ Base de datos: PostgreSQL 15+ (relacional + JSONB)
- 📱 Móvil: React Native 0.79 + Expo SDK 53, Expo Router
- 🔌 Networking/Validación: Axios + TanStack Query, Formik + Yup
- 💾 Offline/Estado: SQLite, Redux Toolkit + Redux Persist, AsyncStorage/MMKV
- ✅ Calidad: Jest (unit/integration/e2e con Testcontainers), ESLint + Prettier
- 🚀 DevOps: Docker + Docker Compose, EAS Build (móvil), Locust (desempeño)

## ✅ Requisitos Previos
- Node.js v20+ y npm o Yarn
- PostgreSQL 15+ (local o contenedor)
- Docker + Docker Compose (opcional, DB y e2e)
- Expo CLI y app Expo Go; Android Studio o Xcode (opcional para emuladores)
- Python 3.10+ (opcional, para Locust)
- Git

## ⚙️ Instalación

1) Clonar el repositorio
```bash
git clone https://github.com/usuario/repositorio.git
cd repositorio
```

2) Backend (API) — `src/api`
```bash
cd src/api

# Instalar dependencias
npm install   # o: yarn install

# Configurar variables de entorno
cp .env.example .env   # En Windows PowerShell: copy .env.example .env

# Editar .env con tus valores:
# - PORT, NODE_ENV
# - JWT_SECRET
# - PG_HOST, PG_PORT, PG_USER, PG_DB, PG_PASS
# - (Opcional) CORS_ORIGIN, LOG_LEVEL, etc.

# (Opcional) Levantar DB local con Docker
# docker compose up -d

# Ejecutar en desarrollo
npm run start:dev       # o: yarn start:dev
```

3) Móvil (Expo) — `src/mobile`
```bash
cd ../mobile

# Instalar dependencias
npm install   # o: yarn install

# Configurar variables de entorno
cp .env.example .env   # En Windows PowerShell: copy .env.example .env

# Editar .env con tus valores EXPO_PUBLIC_:
# - EXPO_PUBLIC_BASE_URL (URL del backend)
# - EXPO_PUBLIC_API_BASE_KEY
# - EXPO_PUBLIC_ACCESS_KEY / EXPO_PUBLIC_ACCESS_SECRET
# - EXPO_PUBLIC_REFRESH_KEY / EXPO_PUBLIC_REFRESH_SECRET
# - EXPO_PUBLIC_QR_MAGIC_CODE

# Ejecutar la app en desarrollo
npm start               # o: yarn start
# luego: npm run android / npm run ios
```

4) 📝 Notas útiles
- En Windows, reemplaza `cp` por `copy`.
- Para e2e del backend se requiere Docker Desktop activo (Testcontainers).
- Detalles avanzados en `src/api/README.md` y `src/mobile/README.md`.
- Dev Client móvil: el archivo `src/mobile/dev-client/devclient.zip` contiene el Dev Client utilizado (comprimido para poder subirlo al repositorio). Puedes usarlo directamente para trabajar con la app si prefieres evitar compilar tu propio Dev Client.
 - Dev Client móvil: el archivo `src/mobile/dev-client/devclient.zip` contiene el Dev Client utilizado (comprimido para poder subirlo al repositorio). Puedes usarlo directamente para trabajar con la app.
 - Recomendado: crea tu propio Dev Client con EAS para evitar incompatibilidades y firmar con tus credenciales. Desde `src/mobile`:
   ```bash
   cd src/mobile
   eas login              # una vez
   eas build:configure    # primera vez del proyecto

   # Android (Dev Client)
   eas build --profile development --platform android

   # Android (APK instalable rápido)
   eas build --profile apk --platform android

   # iOS (Dev Client; requiere Apple Developer)
   eas build --profile development --platform ios
   ```

## 🧪 Pruebas (API)

Desde `src/api`:

Unitarias e Integración (Jest)
```bash
# con npm
npm test

# con Yarn
yarn test
```

Cobertura
```bash
npm run test:cov    # o: yarn test:cov
```

End-to-End (Jest + Testcontainers)
```bash
# Requiere Docker Desktop (WSL2 en Windows)
npm run test:e2e    # o: yarn test:e2e
```

Lint/format y build
```bash
npm run lint        # o: yarn lint
npm run build       # o: yarn build
```

Pruebas de Desempeño (opcional, Locust)
```bash
# Instalar Locust con Python 3.10+
# pip install locust

# Ejecutar contra API local
locust -H http://localhost:3000
```

## 📁 Estructura del Repositorio
```
.
├─ src/
│  ├─ api/       # Backend NestJS (API REST, contratos, pruebas)
│  └─ mobile/    # App móvil React Native (Expo)
├─ docs/         # Documentación del trabajo de graduación
├─ demo/         # Material de demostración (si aplica)
└─ README.md     # Este archivo
```

## 🧩 Arquitectura en Breve
```
React Native (SQLite)  <--offline-->  Cola de envíos  --(HTTP/JWT)-->  NestJS (API REST)
       |                                                        |
       |                              Swagger / Validación DTOs |  PostgreSQL (JSONB + relacional)
       |                                                        |
       └── Sesiones locales, formularios, cursor               └── Consolidación idempotente
```

## 🔗 Enlaces y Documentación
- Documentación API (local): `http://localhost:3000/api` (Swagger UI) y `http://localhost:3000/api-json` (OpenAPI JSON)
- Backend: ver `src/api/README.md`
- Móvil: ver `src/mobile/README.md`
  
# Demo
El video demostrativo se encuentra en [/demo/demo.mp4](https://github.com/Danval-003/PG-2025-21240/blob/main/demo/demo.mp4)

# Documentación
El informe final del proyecto está disponible en [/docs/informe_final.pdf](https://github.com/Danval-003/PG-2025-21240/blob/main/docs)

# Autor
Daniel Armando Valdez Reyes - 21240

