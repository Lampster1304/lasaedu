# 📚 LasaEdu - Learning Management System

<p align="center">
  <img src="public/logo.svg" alt="LasaEdu Logo" width="120" />
</p>

<p align="center">
  <strong>Plataforma completa de gestión educativa para instituciones</strong>
</p>

<p align="center">
  <a href="#características">Características</a> •
  <a href="#instalación">Instalación</a> •
  <a href="#uso">Uso</a> •
  <a href="#arquitectura">Arquitectura</a> •
  <a href="#módulos">Módulos</a>
</p>

---

## 🎯 Descripción

**LasaEdu** es un Sistema de Gestión de Aprendizaje (LMS) moderno y completo, desarrollado con React, TypeScript y Firebase. Diseñado para instituciones educativas que buscan digitalizar y optimizar sus procesos de enseñanza-aprendizaje.

## ✨ Características

### 👥 Multi-Rol
- **Administrador**: Gestión completa del sistema, usuarios, cursos y reportes
- **Profesor**: Creación de cursos, evaluaciones y seguimiento de estudiantes
- **Estudiante**: Acceso a cursos, evaluaciones, progreso y certificados
- **Soporte**: Gestión de tickets y atención a usuarios

### 📖 Gestión de Cursos
- Creación y edición de cursos con módulos y lecciones
- Soporte multimedia (video, audio, documentos)
- Catálogo público de cursos
- Sistema de inscripciones

### 📝 Evaluaciones
- Múltiples tipos: Quiz, Examen, Tarea, Proyecto
- Preguntas variadas: Opción múltiple, Verdadero/Falso, Respuesta corta
- Calificación automática y manual
- Retroalimentación personalizada

### 🏆 Gamificación
- Sistema de puntos por actividades
- Insignias y logros desbloqueables
- Rachas de aprendizaje
- Tabla de clasificación (Leaderboard)

### 🎓 Certificados
- Generación automática al completar cursos
- Diseños personalizables
- Código de verificación único
- Descarga en PDF

### 📊 Analytics y Reportes
- Dashboard con métricas en tiempo real
- Reportes de progreso por estudiante
- Estadísticas de cursos y evaluaciones
- Exportación de datos

### 💬 Comunicación
- Sistema de mensajería interna
- Notificaciones en tiempo real
- Foros de discusión por curso

### 🎫 Soporte
- Sistema de tickets
- Categorización y priorización
- Historial de conversaciones

---

## 🛠 Stack Tecnológico

### Frontend
| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| React | 19.2.0 | Framework UI |
| TypeScript | 5.x | Tipado estático |
| Vite | 7.3.1 | Build tool & Dev server |
| TailwindCSS | 3.x | Framework CSS |
| Zustand | 5.0.10 | Estado global |
| React Router | 7.12.0 | Enrutamiento SPA |
| React Hook Form | 7.71.0 | Gestión de formularios |
| Zod | 4.3.5 | Validación de schemas |
| Lucide React | 0.562.0 | Iconografía |

### Backend & Base de Datos
| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| Firebase Realtime DB | 12.7.0 | Base de datos NoSQL |
| Firebase Storage | 12.7.0 | Almacenamiento de archivos |
| Firebase Emulator | - | Desarrollo local |

### Testing
| Tecnología | Propósito |
|------------|-----------|
| Vitest | Unit & Integration testing |
| Testing Library | Component testing |
| jsdom | DOM simulation |

---

## 📦 Instalación

### Prerrequisitos

- **Node.js** >= 18.x
- **npm** >= 9.x o **yarn** >= 1.22
- **Java** >= 11 (para Firebase Emulators)
- **Firebase CLI** instalado globalmente

```bash
npm install -g firebase-tools
```

### Pasos de Instalación

1. **Clonar el repositorio**
```bash
git clone https://github.com/tu-usuario/lasaedu.git
cd lasaedu
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Configurar variables de entorno** (opcional para producción)
```bash
cp .env.example .env.local
# Editar .env.local con tus credenciales de Firebase
```

4. **Iniciar Firebase Emulators**
```bash
# En macOS, si Java está en Android Studio:
export JAVA_HOME="/Applications/Android Studio.app/Contents/jbr/Contents/Home"

# Iniciar emuladores
npm run firebase:emulator
```

5. **Poblar la base de datos** (ver sección de Seed Data)

6. **Iniciar servidor de desarrollo**
```bash
npm run dev
```

7. **Abrir en el navegador**
```
http://localhost:5173
```

---

## 🔥 Firebase Emulators

### Configuración

El proyecto usa Firebase Emulators para desarrollo local, evitando costos y permitiendo trabajar offline.

**Archivo de configuración:** `firebase.json`
```json
{
  "database": {
    "rules": "database.rules.json"
  },
  "storage": {
    "rules": "storage.rules"
  },
  "emulators": {
    "database": { "port": 9000, "host": "127.0.0.1" },
    "storage": { "port": 9199, "host": "127.0.0.1" },
    "ui": { "enabled": true, "port": 4000, "host": "127.0.0.1" }
  }
}
```

### Iniciar Emuladores

```bash
# Si Java está en Android Studio (macOS):
export JAVA_HOME="/Applications/Android Studio.app/Contents/jbr/Contents/Home"

# Iniciar emuladores
firebase emulators:start

# O usar el script npm:
npm run firebase:emulator
```

### URLs de los Emuladores

| Servicio | URL | Puerto |
|----------|-----|--------|
| Emulator UI | http://127.0.0.1:4000 | 4000 |
| Database | http://127.0.0.1:9000 | 9000 |
| Storage | http://127.0.0.1:9199 | 9199 |
| Hub | http://127.0.0.1:4400 | 4400 |

### Exportar/Importar Datos

```bash
# Exportar datos del emulador
npm run firebase:emulator:export

# Iniciar con datos previamente exportados
npm run firebase:emulator:import
```

---

## 🌱 Seed Data (Poblar Base de Datos)

La aplicación **NO usa datos mock hardcodeados**. Todo viene de Firebase. Para que funcione, debes poblar el emulador con datos iniciales.

### Método 1: Usando cURL (Recomendado)

Con los emuladores corriendo, ejecuta estos comandos:

```bash
# 1. Crear usuarios
curl -X PUT "http://127.0.0.1:9000/users.json?ns=demo-project" \
  -H "Content-Type: application/json" \
  -d '{
    "admin_1": {
      "id": "admin_1",
      "name": "Administrador Principal",
      "email": "admin@lasaedu.com",
      "role": "admin",
      "emailVerified": true,
      "createdAt": 1737399000000,
      "updatedAt": 1737399000000
    },
    "teacher_1": {
      "id": "teacher_1",
      "name": "Prof. María García",
      "email": "garcia@lasaedu.com",
      "role": "teacher",
      "emailVerified": true,
      "createdAt": 1737399000000,
      "updatedAt": 1737399000000
    },
    "student_1": {
      "id": "student_1",
      "name": "Ana López",
      "email": "ana@lasaedu.com",
      "role": "student",
      "emailVerified": true,
      "createdAt": 1737399000000,
      "updatedAt": 1737399000000
    }
  }'

# 2. Crear cursos
curl -X PUT "http://127.0.0.1:9000/courses.json?ns=demo-project" \
  -H "Content-Type: application/json" \
  -d '{
    "course_1": {
      "id": "course_1",
      "title": "Introducción a Python",
      "description": "Aprende los fundamentos de programación con Python desde cero.",
      "instructorId": "teacher_1",
      "instructor": "Prof. María García",
      "category": "programacion",
      "level": "principiante",
      "duration": "8 semanas",
      "status": "publicado",
      "rating": 4.8,
      "studentsCount": 0,
      "createdAt": 1737399000000,
      "updatedAt": 1737399000000,
      "modules": []
    }
  }'

# 3. Crear inscripciones (opcional)
curl -X PUT "http://127.0.0.1:9000/enrollments.json?ns=demo-project" \
  -H "Content-Type: application/json" \
  -d '{
    "enroll_1": {
      "id": "enroll_1",
      "userId": "student_1",
      "courseId": "course_1",
      "status": "active",
      "progress": 0,
      "enrolledAt": 1737399000000,
      "createdAt": 1737399000000,
      "updatedAt": 1737399000000,
      "completedLessons": [],
      "completedModules": [],
      "totalTimeSpent": 0,
      "source": "manual"
    }
  }'
```

### Método 2: Usando la UI del Emulador

1. Abre http://127.0.0.1:4000/database
2. Click en "+ Add" para agregar datos manualmente
3. Crea las colecciones: `users`, `courses`, `enrollments`, etc.

### Verificar Datos

```bash
# Ver todos los usuarios
curl "http://127.0.0.1:9000/users.json?ns=demo-project"

# Ver todos los cursos
curl "http://127.0.0.1:9000/courses.json?ns=demo-project"
```

---

## ⚠️ Importante: Sin Datos Mock

### Lo que se eliminó

El proyecto originalmente tenía datos hardcodeados en varios archivos. Se eliminaron para que **todo venga de la base de datos real**:

| Archivo | Cambio Realizado |
|---------|------------------|
| `src/main.tsx` | Removido `initializeLocalDB()` |
| `src/shared/hooks/useDashboard.ts` | Removidos stats/activities/metrics mock |
| `src/modules/courses/pages/CoursesPage.tsx` | Usa `courseService.getAll()` real |
| `src/modules/courses/pages/CourseCatalogPage.tsx` | Usa `courseService.getAll()` real |
| `src/modules/evaluations/pages/EvaluationsPage.tsx` | Usa `evaluationService.getAll()` real |
| `src/shared/services/firebaseDataService.ts` | `USE_FIREBASE = true` siempre |

### Configuración de Firebase

En `src/shared/services/firebaseDataService.ts`:
```typescript
// Siempre usa Firebase (no LocalDB mock)
const USE_FIREBASE = true;
```

### Comportamiento Esperado

- **Sin datos**: Dashboard muestra 0 usuarios, 0 cursos, listas vacías
- **Con seed data**: Dashboard muestra datos reales de Firebase
- **Todos los CRUD**: Operan directamente sobre Firebase Realtime Database

---

## 🚀 Uso

### Scripts Disponibles

| Comando | Descripción |
|---------|-------------|
| `npm run dev` | Inicia servidor de desarrollo |
| `npm run build` | Compila para producción |
| `npm run preview` | Preview de build de producción |
| `npm run lint` | Ejecuta ESLint |
| `npm run test` | Ejecuta tests en modo watch |
| `npm run test:run` | Ejecuta tests una vez |
| `npm run test:coverage` | Genera reporte de cobertura |
| `npm run firebase:emulator` | Inicia Firebase Emulators |

### Acceso al Sistema

**URLs de desarrollo:**
- **Aplicación**: http://localhost:5173
- **Firebase Emulator UI**: http://localhost:4000
- **Database Emulator**: http://localhost:9000
- **Storage Emulator**: http://localhost:9199

**Credenciales de prueba:**
| Rol | Email | Contraseña |
|-----|-------|------------|
| Admin | admin@lasaedu.com | admin123 |
| Profesor | garcia@lasaedu.com | teacher123 |
| Estudiante | ana@lasaedu.com | student123 |

---

## 🏗 Arquitectura

```
┌─────────────────────────────────────────────────────────────────┐
│                         FRONTEND (React)                         │
├─────────────────────────────────────────────────────────────────┤
│  Pages/Views    │    Components    │    Hooks    │    Store     │
├─────────────────────────────────────────────────────────────────┤
│                      SERVICE LAYER                               │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    dataService.ts                         │   │
│  │  dashboardService • courseService • userService • etc.   │   │
│  └──────────────────────────────────────────────────────────┘   │
├─────────────────────────────────────────────────────────────────┤
│                    DATA ABSTRACTION LAYER                        │
│  ┌───────────────────────┐    ┌────────────────────────────┐   │
│  │  firebaseDataService  │ OR │       localDB.ts           │   │
│  │  (Firebase Realtime)  │    │    (localStorage mock)     │   │
│  └───────────────────────┘    └────────────────────────────┘   │
├─────────────────────────────────────────────────────────────────┤
│                    Firebase Realtime Database                    │
└─────────────────────────────────────────────────────────────────┘
```

### Estructura de Directorios

```
lasaedu/
├── src/
│   ├── app/                    # Configuración core
│   │   ├── config/             # Firebase config
│   │   ├── router/             # Rutas de la aplicación
│   │   └── store/              # Estado global (Zustand)
│   │
│   ├── modules/                # Módulos funcionales
│   │   ├── analytics/          # Reportes y estadísticas
│   │   ├── auth/               # Autenticación
│   │   ├── certificates/       # Certificados
│   │   ├── communication/      # Mensajería
│   │   ├── courses/            # Gestión de cursos
│   │   ├── dashboard/          # Dashboards por rol
│   │   ├── enrollments/        # Inscripciones
│   │   ├── evaluations/        # Evaluaciones
│   │   ├── forums/             # Foros de discusión
│   │   ├── gamification/       # Puntos e insignias
│   │   ├── grades/             # Calificaciones
│   │   ├── notifications/      # Notificaciones
│   │   ├── progress/           # Progreso del estudiante
│   │   ├── settings/           # Configuración
│   │   ├── support/            # Sistema de tickets
│   │   └── users/              # Gestión de usuarios
│   │
│   ├── shared/                 # Recursos compartidos
│   │   ├── components/         # Componentes reutilizables
│   │   │   ├── layout/         # Header, Sidebar, MainLayout
│   │   │   ├── media/          # VideoPlayer
│   │   │   └── ui/             # Button, Card, Input, Label
│   │   ├── hooks/              # Hooks personalizados
│   │   ├── services/           # Servicios de datos
│   │   ├── types/              # Definiciones TypeScript
│   │   └── utils/              # Utilidades
│   │
│   ├── App.tsx                 # Componente raíz
│   ├── main.tsx                # Entry point
│   └── index.css               # Estilos globales
│
├── public/                     # Assets estáticos
├── firebase.json               # Configuración Firebase
├── database.rules.json         # Reglas de seguridad DB
├── storage.rules               # Reglas de Storage
└── package.json
```

---

## 📚 Módulos

### 🔐 Auth (Autenticación)
- Login/Logout
- Registro de usuarios
- Recuperación de contraseña
- Protección de rutas por rol

### 📊 Dashboard
- **AdminDashboard**: Métricas globales, gestión del sistema
- **TeacherDashboard**: Cursos asignados, estudiantes
- **StudentDashboard**: Cursos inscritos, progreso
- **SupportDashboard**: Tickets pendientes

### 📖 Courses (Cursos)
- CRUD completo de cursos
- Gestión de módulos y lecciones
- Editor de contenido multimedia
- Catálogo público con filtros

### 📝 Evaluations (Evaluaciones)
- Builder de evaluaciones
- Constructor de preguntas múltiples tipos
- Sistema de toma de evaluaciones
- Calificación automática/manual

### 🎓 Certificates (Certificados)
- Generación automática PDF
- Personalización de diseño
- Verificación con código único

### 🏆 Gamification (Gamificación)
- Puntos por completar actividades
- Sistema de insignias
- Rachas de aprendizaje consecutivo
- Leaderboard global y por curso

### 👥 Users (Usuarios)
- CRUD de usuarios
- Asignación de roles
- Gestión de perfiles

### 📈 Analytics (Analíticas)
- Reportes de progreso
- Estadísticas de cursos
- Métricas del sistema
- Exportación a CSV/Excel

### 🎫 Support (Soporte)
- Sistema de tickets
- Priorización y categorías
- Chat en tickets

---

## 🗄 Base de Datos

### Estructura de Colecciones Firebase

| Colección | Descripción | Campos Principales |
|-----------|-------------|-------------------|
| `users` | Usuarios del sistema | id, name, email, role, emailVerified, createdAt |
| `courses` | Cursos disponibles | id, title, description, instructorId, status, level, category |
| `modules` | Módulos de cursos | id, courseId, title, order, lessons |
| `lessons` | Lecciones | id, moduleId, title, type, content, duration |
| `enrollments` | Inscripciones | id, userId, courseId, status, progress, enrolledAt |
| `evaluations` | Evaluaciones | id, courseId, title, type, questions, timeLimit |
| `evaluationAttempts` | Intentos de evaluación | id, evaluationId, userId, score, answers |
| `grades` | Calificaciones | id, userId, courseId, evaluationId, score |
| `certificates` | Certificados emitidos | id, userId, courseId, certificateNumber, issuedAt |
| `messages` | Mensajes | id, senderId, receiverId, content, timestamp |
| `conversations` | Conversaciones | id, participants, lastMessage, updatedAt |
| `notifications` | Notificaciones | id, userId, title, message, read, createdAt |
| `supportTickets` | Tickets de soporte | id, userId, subject, status, priority |
| `activities` | Log de actividades | id, userId, action, timestamp, details |
| `userPoints` | Puntos de gamificación | id, points, history |
| `badges` | Insignias disponibles | id, name, description, icon, criteria |
| `userBadges` | Insignias de usuarios | id, badgeId, earnedAt |

### Tipos de Usuario (roles)

```typescript
type UserRole = 'admin' | 'teacher' | 'student' | 'support';
```

### Estados de Curso

```typescript
type CourseStatus = 'borrador' | 'publicado' | 'archivado';
```

### Estados de Inscripción

```typescript
type EnrollmentStatus = 'active' | 'completed' | 'paused' | 'cancelled';
```

### Ejemplo de Documento User

```json
{
  "id": "admin_1",
  "name": "Administrador Principal",
  "email": "admin@lasaedu.com",
  "role": "admin",
  "emailVerified": true,
  "avatar": null,
  "phone": null,
  "bio": "Administrador del sistema",
  "createdAt": 1737399000000,
  "updatedAt": 1737399000000
}
```

### Ejemplo de Documento Course

```json
{
  "id": "course_1",
  "title": "Introducción a Python",
  "description": "Aprende Python desde cero",
  "instructorId": "teacher_1",
  "instructor": "Prof. María García",
  "category": "programacion",
  "level": "principiante",
  "duration": "8 semanas",
  "status": "publicado",
  "rating": 4.8,
  "studentsCount": 156,
  "createdAt": 1737399000000,
  "updatedAt": 1737399000000,
  "modules": []
}
```

### Ejemplo de Documento Enrollment

```json
{
  "id": "enroll_1",
  "userId": "student_1",
  "courseId": "course_1",
  "status": "active",
  "progress": 65.5,
  "enrolledAt": 1737399000000,
  "createdAt": 1737399000000,
  "updatedAt": 1737399000000,
  "completedLessons": ["lesson_1", "lesson_2"],
  "completedModules": [],
  "totalTimeSpent": 1200,
  "lastAccessedAt": 1737485400000,
  "grade": null,
  "source": "manual"
}
```

---

## 🧪 Testing

```bash
# Ejecutar todos los tests
npm run test

# Ejecutar tests una vez
npm run test:run

# Ver cobertura
npm run test:coverage

# Modo UI interactivo
npm run test:ui
```

---

## 🚢 Deployment

### Build de Producción

```bash
npm run build
```

Los archivos compilados estarán en la carpeta `dist/`.

### Deploy a Firebase Hosting

```bash
firebase deploy --only hosting
```

### Variables de Entorno para Producción

```env
VITE_FIREBASE_API_KEY=your-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_DATABASE_URL=https://your-project.firebaseio.com
VITE_FIREBASE_PROJECT_ID=your-project
VITE_FIREBASE_STORAGE_BUCKET=your-project.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123456789:web:abcdef
VITE_USE_FIREBASE=true
```

---

## 📋 Roadmap

- [x] Sistema de autenticación
- [x] Dashboards por rol
- [x] Gestión de cursos
- [x] Sistema de evaluaciones
- [x] Generación de certificados
- [x] Gamificación básica
- [x] Sistema de soporte
- [x] Notificaciones
- [x] Foros de discusión
- [ ] Integración con videoconferencia
- [ ] App móvil (React Native)
- [ ] API REST pública
- [ ] Integración con pasarelas de pago
- [ ] Internacionalización (i18n)
- [ ] PWA (Progressive Web App)

---

## 🤝 Contribución

1. Fork el proyecto
2. Crea tu rama de feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add: AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

### Convenciones de Commits

```
feat:     Nueva funcionalidad
fix:      Corrección de bug
docs:     Documentación
style:    Formato (sin cambio de código)
refactor: Refactorización
test:     Tests
chore:    Mantenimiento
```

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

---

## 👨‍💻 Equipo

**LasaEdu Development Team**

---

<p align="center">
  Hecho con ❤️ para la educación
</p>

<p align="center">
  <sub>© 2026 LasaEdu. Todos los derechos reservados.</sub>
</p>
