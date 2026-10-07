# Sistema de Gestión de Proyectos FCT

> [!NOTE]
> **Proyecto archivado (agosto de 2025).** Fue mi primer enfoque para el proyecto de fin de ciclo de DAM: backend NestJS con Clean Architecture y cliente Flutter.
> Lo abandoné en favor de [proyecto_flutter_supabase](https://github.com/jualas/proyecto_flutter_supabase), que evolucionó después en **[TaskBoard](https://github.com/jualas/taskboard)** (FastAPI + PostgreSQL + Flutter Web, con asistente IA y servidor MCP).
> Se conserva como referencia; no recibe mantenimiento.

![Flutter](https://img.shields.io/badge/Flutter-3.16.0-blue)
![NestJS](https://img.shields.io/badge/NestJS-11.0-red)
![Node.js](https://img.shields.io/badge/Node.js-20.19.4-green)
![License](https://img.shields.io/badge/license-MIT-green)

Sistema completo para la gestión de proyectos de FCT, desarrollado con NestJS (backend) y Flutter (frontend) siguiendo principios de Clean Architecture.

## 🚀 Inicio Rápido

### 📋 Requisitos del Sistema

- **Node.js**: Versión 20.11.0 o superior (recomendado: 20.19.4)
- **npm**: Versión 10.8.2 o superior
- **PostgreSQL**: Versión 13 o superior
- **Docker & Docker Compose**: Para despliegue con contenedores

#### Instalación de Node.js (si no lo tienes):

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install nodejs -y
node --version  # Debe mostrar v20.x.x
```

### Configuración Automática

```bash
# Linux/macOS
./setup.sh

# Windows (PowerShell)
.\setup.ps1
```

### Configuración Manual

Ver [CONTRIBUTING.md](CONTRIBUTING.md) para instrucciones detalladas.

### 🔑 Configuración de Google OAuth

Para autenticación con Google, sigue la [guía completa](backend/docs/GOOGLE_OAUTH_SETUP.md).

## � Backend API - Proyecto FCT (Production Ready)

## 📋 Descripción

**Backend API NestJS** optimizado para producción con arquitectura Clean Architecture, Docker multi-stage builds y configuración de seguridad robusta.

### ✨ Características de Producción

- 🔒 **Seguridad**: Usuario no privilegiado, multi-stage builds
- 🐳 **Docker Optimizado**: Healthchecks robustos, imágenes ligeras
- 🔧 **Crypto Polyfill**: Compatibilidad completa con Alpine Linux
- 📊 **Monitoreo**: Logs estructurados, métricas de salud
- 🗃️ **Base de Datos**: PostgreSQL con scripts de inicialización

## 🚀 Despliegue Rápido

### Prerrequisitos

- Docker & Docker Compose
- Variables de entorno configuradas

### Opción 1: Desarrollo Local

```bash
git clone https://github.com/elmosca/proyecto-fct-NetJs.git -b production-backend
cd proyecto-fct-NetJs/backend
cp .env.example .env
# Editar .env con tus configuraciones
docker compose up -d
```

### Opción 2: Producción

```bash
# Clonar rama de producción
git clone https://github.com/elmosca/proyecto-fct-NetJs.git -b production-backend

# Variables de entorno para producción
export NODE_ENV=production
export DATABASE_URL="postgresql://user:pass@your-db-host:5432/tfg_production"
export JWT_SECRET="your-ultra-secure-jwt-secret"
export CORS_ORIGIN="https://tu-app.com,https://www.tu-app.com"

# Build y deploy
cd proyecto-fct-NetJs/backend
docker build -t tfg-backend-api:latest .
docker run -d \
  --name tfg-api \
  -p 3000:3000 \
  -e NODE_ENV=production \
  -e DATABASE_URL=$DATABASE_URL \
  -e JWT_SECRET=$JWT_SECRET \
  -e CORS_ORIGIN=$CORS_ORIGIN \
  --restart unless-stopped \
  tfg-backend-api:latest
```

## 🏗️ Arquitectura

```
backend/
├── src/
│   ├── auth/              # Autenticación y autorización
│   ├── users/             # Gestión de usuarios
│   ├── projects/          # Gestión de proyectos TFG
│   ├── anteprojects/      # Anteproyectos
│   ├── evaluations/       # Sistema de evaluaciones
│   ├── files/             # Gestión de archivos
│   ├── notifications/     # Sistema de notificaciones
│   ├── common/            # Utilidades compartidas
│   ├── polyfill.js        # Crypto polyfill para Alpine
│   └── main.ts            # Punto de entrada
├── init-scripts/          # Scripts inicialización DB
├── docs/                  # Documentación técnica
├── Dockerfile             # Multi-stage optimizado
└── docker-compose.yml     # Orquestación de servicios
```

## 🔧 Configuración

```
proyecto-fct/
├── .github/                  # Configuración de GitHub (CI/CD, templates)
├── .vscode/                  # Configuración de VS Code optimizada
├── backend/                  # Backend en NestJS
│   ├── src/                 # Código fuente del backend
│   ├── test/                # Pruebas del backend
│   └── docs/                # Documentación técnica
├── frontend/                # Frontend en Flutter
│   ├── lib/                 # Código fuente de Flutter
│   └── test/                # Pruebas de Flutter
└── docs/                    # Documentación general del proyecto
```

## 🛠️ Stack Tecnológico

### Backend

- **Framework**: NestJS + TypeScript
- **Base de datos**: PostgreSQL
- **ORM**: TypeORM
- **Autenticación**: JWT + Google OAuth
- **Documentación**: Swagger/OpenAPI
- **Testing**: Jest + Supertest

### Frontend

- **Framework**: Flutter + Dart
- **Arquitectura**: Clean Architecture
- **Estado**: Riverpod
- **Navegación**: AutoRoute
- **DI**: GetIt
- **Generación de código**: build_runner + freezed
- **Testing**: flutter_test + mockito
- **Internacionalización**: Soporte completo bilingüe (Castellano/Inglés)

## 🌍 Internacionalización (i18n)

### **Soporte Bilingüe Completo**

El proyecto incluye **soporte completo para dos idiomas** para facilitar el trabajo en un entorno educativo bilingüe:

#### **Idiomas Soportados**
- 🇪🇸 **Castellano**: Idioma principal del centro educativo
- 🇬🇧 **Inglés**: Idioma secundario para estudiantes internacionales y contenido bilingüe

#### **Características de Internacionalización**

##### **🔄 Cambio de Idioma en Tiempo Real**
- Selector de idioma integrado en el perfil de usuario
- Cambio instantáneo sin necesidad de reiniciar la aplicación
- Persistencia automática de la preferencia de idioma
- Detección automática del idioma del sistema operativo

##### **📱 Contenido Dinámico Multilingüe**
- **Interfaz de usuario**: Todos los textos, botones, etiquetas y mensajes
- **Contenido de usuario**: Títulos de proyectos, descripciones, comentarios
- **Documentación**: Ayuda, tutoriales, mensajes de error y validación
- **Notificaciones**: Emails, push notifications, mensajes del sistema

##### **🏗️ Arquitectura de Internacionalización**

```
frontend/
├── lib/
│   ├── core/
│   │   ├── i18n/                    # Configuración de i18n
│   │   │   ├── locale_provider.dart # Gestión de idioma
│   │   │   └── i18n_config.dart     # Configuración
│   │   └── widgets/
│   │       └── language_selector.dart # Selector de idioma
├── assets/
│   └── i18n/
│       ├── app_es.arb              # Traducciones en castellano
│       └── app_en.arb              # Traducciones en inglés
```

##### **🔧 Configuración Técnica**

```dart
// Configuración en MaterialApp
MaterialApp(
  localizationsDelegates: const [
    AppLocalizations.delegate,
    GlobalMaterialLocalizations.delegate,
    GlobalWidgetsLocalizations.delegate,
    GlobalCupertinoLocalizations.delegate,
  ],
  supportedLocales: const [
    Locale('es', ''), // Castellano
    Locale('en', ''), // Inglés
  ],
  locale: context.watch<LocaleProvider>().locale,
)
```

##### **📝 Uso en el Código**

```dart
// Ejemplo de uso en widgets
Text(AppLocalizations.of(context)!.loginTitle)
Text(AppLocalizations.of(context)!.projectDescription)

// Cambio de idioma programático
final localeNotifier = ref.read(localeProvider.notifier);
localeNotifier.setLocaleFromLanguageCode('en');
```

##### **🧪 Testing de Internacionalización**
- Tests unitarios para verificar traducciones
- Tests de widgets con diferentes idiomas
- Tests de integración con cambio de idioma
- Verificación de textos largos en ambos idiomas
- Tests de accesibilidad en ambos idiomas

##### **⚡ Comandos de Desarrollo**

```bash
# Generar archivos de localización
flutter gen-l10n

# Ejecutar tests de internacionalización
flutter test test/core/i18n/

# Verificar traducciones
flutter analyze lib/core/i18n/
```

##### **🎯 Beneficios para el Centro Educativo**
- **Inclusividad**: Acceso para estudiantes internacionales
- **Flexibilidad**: Contenido adaptable según necesidades
- **Escalabilidad**: Fácil adición de nuevos idiomas
- **Consistencia**: Experiencia uniforme en ambos idiomas
- **Accesibilidad**: Mejora la experiencia para usuarios no nativos

## 🏗️ Requisitos Previos

### Backend

- Node.js 18+
- PostgreSQL 13+
- Docker y Docker Compose

### Frontend

- Flutter 3.16+
- Android Studio / VS Code
- Android SDK / iOS SDK

## Configuración del Entorno de Desarrollo

### Backend

1. Navegar al directorio del backend:

   ```bash
   cd backend
   ```

2. Instalar dependencias:

   ```bash
   npm install
   ```

3. Configurar variables de entorno:

   ```bash
   cp .env.example .env
   ```

4. Iniciar la base de datos con Docker:

   ```bash
   docker-compose up -d
   ```

5. Ejecutar migraciones:

   ```bash
   npm run migration:run
   ```

6. Iniciar el servidor de desarrollo:
   ```bash
   npm run start:dev
   ```

### Frontend

1. Navegar al directorio del frontend:

   ```bash
   cd frontend
   ```

2. Instalar dependencias:

   ```bash
   flutter pub get
   ```

3. Ejecutar la aplicación:
   ```bash
   flutter run
   ```

## Documentación

- [Documentación Técnica del Backend](./backend/docs/TECHNICAL_DOCUMENTATION.md)
- [Estado del Proyecto](./backend/docs/PROJECT_STATUS.md)

## Scripts Disponibles

### Backend

```bash
# Desarrollo
npm run start:dev

# Producción
npm run build
npm run start:prod

# Pruebas
npm run test
npm run test:e2e
```

### Frontend

```bash
# Desarrollo
flutter run

# Construir APK
flutter build apk

# Ejecutar pruebas
flutter test
```

## Estrategia de Ramas y Contribución (Git Flow Simplificado)

Este proyecto utiliza una estrategia de ramas simplificada basada en Git Flow para mantener el código organizado y estable.

### Ramas Principales

- `main`: Contiene el código de producción. Es una rama estable y solo se actualiza con versiones probadas desde `develop`. No se debe trabajar directamente en ella.
- `develop`: Es la rama principal de integración. Todo el nuevo desarrollo se concentra aquí antes de pasar a producción.

### Flujo de Trabajo para Contribuir

1.  **Asegúrate de estar en la rama `develop` y tener la última versión:**

    ```bash
    git checkout develop
    # git pull origin develop  (Cuando el repositorio remoto esté configurado)
    ```

2.  **Crea una rama para la nueva funcionalidad (feature):**
    El nombre debe ser descriptivo, en minúsculas y separado por guiones.

    ```bash
    # Ejemplo: git checkout -b feature/login-con-google
    git checkout -b feature/nombre-de-la-funcionalidad
    ```

3.  **Realiza tus cambios y haz commits:**
    Sigue las [convenciones de commits](#convenciones-de-commits) definidas.

    ```bash
    git add .
    git commit -m "feat(auth): implementar nueva funcionalidad"
    ```

4.  **Sube tus cambios a tu rama remota:**

    ```bash
    # git push origin feature/nombre-de-la-funcionalidad
    ```

5.  **Crea una Pull Request (PR)** en la plataforma remota (GitHub, GitLab, etc.) desde tu rama `feature` hacia la rama `develop`. Esto permitirá revisar el código antes de integrarlo.

## Convenciones de Commits

Para mantener un historial de cambios limpio y legible, todos los commits deben seguir las siguientes reglas:

- **Idioma**: Todos los mensajes de commit deben estar escritos en **castellano**.
- **Formato**: Se debe seguir el estándar de [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/).

El formato general es:

```
<tipo>(<ámbito opcional>): <descripción>
```

**Tipos de commit permitidos:**

- `feat`: Una nueva funcionalidad (feature).
- `fix`: Una corrección de un error (bug fix).
- `docs`: Cambios en la documentación.
- `style`: Cambios que no afectan el significado del código (espacios, formato, etc.).
- `refactor`: Una refactorización de código que no arregla un bug ni añade una funcionalidad.
- `test`: Añadir o corregir tests.
- `chore`: Cambios en el proceso de build, dependencias o herramientas auxiliares.

**Ejemplo:**

```bash
git commit -m "feat(auth): implementar inicio de sesión con Google"
git commit -m "fix(api): corregir error en la paginación de usuarios"
```

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor lee nuestra [Guía de Contribución](CONTRIBUTING.md) para conocer:

- 📋 Cómo reportar bugs
- ✨ Cómo sugerir nuevas funcionalidades
- 💻 Cómo configurar el entorno de desarrollo
- 🔄 Proceso de Pull Requests
- 📝 Convenciones de código y commits

### Flujo Rápido para Contribuir

1. **Fork el repositorio** en GitHub
2. **Crea una rama** desde `develop`:
   ```bash
   git checkout -b feature/mi-nueva-funcionalidad
   ```
3. **Realiza tus cambios** siguiendo las convenciones
4. **Ejecuta los tests** localmente
5. **Crea un Pull Request** hacia `develop`

## 📄 Documentación Adicional

- 📖 [Guía de Contribución](CONTRIBUTING.md) - Cómo contribuir al proyecto
- 🔒 [Política de Seguridad](SECURITY.md) - Reportar vulnerabilidades
- 🤖 [Copilot Instructions](.github/copilot-instructions.md) - Guía para IA
- ⚙️ [Configuración VS Code](.vscode/README.md) - Setup del editor

## 🔗 Enlaces Útiles

- [Documentación de Flutter](https://flutter.dev/docs)
- [Documentación de NestJS](https://docs.nestjs.com/)
- [Clean Architecture en Flutter](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [Conventional Commits](https://www.conventionalcommits.org/)

## 📊 Estado del Proyecto

- ✅ Backend API con autenticación
- ✅ Frontend Flutter con navegación
- ✅ CI/CD Pipeline configurado
- ✅ **Internacionalización completa (Castellano/Inglés)**
- 🔄 Integración con base de datos
- 🔄 Testing automatizado
- 📋 Documentación en progreso

## 📧 Contacto

Para preguntas sobre el proyecto:

- 📧 Email: [jualas@gmail.com]
- 📱 Issues: [GitHub Issues](https://github.com/elmosca/proyecto-fct-NetJs/issues)

## 📜 Licencia

Este proyecto está bajo la Licencia [Creative Commons Attribution-NonCommercial 4.0 International](https://creativecommons.org/licenses/by-nc/4.0/).
Ver el archivo [LICENSE](./LICENSE) para más detalles.
