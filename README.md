<p align="center">
  <a href="https://www.medusajs.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://user-images.githubusercontent.com/59018053/229103275-b5e482bb-4601-46e6-8142-244f531cebdb.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://user-images.githubusercontent.com/59018053/229103726-e5b529a3-9b3f-4970-8a1f-c6af37f087bf.svg">
    <img alt="Medusa logo" src="https://user-images.githubusercontent.com/59018053/229103726-e5b529a3-9b3f-4970-8a1f-c6af37f087bf.svg">
    </picture>
  </a>
</p>

<h1 align="center">Medusa — README técnico</h1>

<p align="center">
  Instrucciones de instalación local con Docker Compose, variables de entorno y estructura del proyecto.
</p>

<p align="center">
  <a href="https://github.com/medusajs/medusa/blob/develop/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="Medusa is released under the MIT license." />
  </a>
  <a href="https://github.com/medusajs/medusa/blob/develop/CONTRIBUTING.md">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat" alt="PRs welcome!" />
  </a>
  <a href="https://discord.gg/medusajs">
    <img src="https://img.shields.io/badge/chat-on%20discord-7289DA.svg" alt="Discord Chat" />
  </a>
</p>

---

## 🚀 Instalación local con Docker Compose

Este proyecto utiliza **Docker Compose** para levantar todos los servicios necesarios con un único comando.

### Requisitos previos

- [Docker](https://docs.docker.com/get-docker/) >= 20.x
- [Docker Compose](https://docs.docker.com/compose/install/) >= 2.x
- [Node.js](https://nodejs.org/) >= 20.x (solo para desarrollo fuera de Docker)

### Pasos para levantar el entorno

```bash
# 1. Clonar el repositorio
git clone https://github.com/<tu-usuario>/medusa-project.git
cd medusa-project

# 2. Copiar el archivo de variables de entorno
cp .env.example .env

# 3. Levantar todos los servicios con Docker Compose
docker compose up --build
```

Los servicios disponibles después del arranque serán:

| Servicio       | URL                         | Descripción                        |
|----------------|-----------------------------|------------------------------------|
| Backend API    | http://localhost:9000       | API REST de MedusaJS               |
| Admin Panel    | http://localhost:7001       | Panel administrativo (React)       |
| Storefront     | http://localhost:8000       | Tienda en línea (Next.js)          |
| PostgreSQL     | localhost:5432              | Base de datos principal            |
| Redis          | localhost:6379              | Caché y colas de trabajo           |

---

## 🔐 Variables de entorno

Copia el archivo `.env.example` como `.env` y ajusta los valores según tu entorno local.

```env
# Base de datos
DATABASE_URL=postgres://medusa:medusa@postgres:5432/medusadb

# Redis
REDIS_URL=redis://redis:6379

# JWT y cookies
JWT_SECRET=tu_secreto_jwt_aqui
COOKIE_SECRET=tu_secreto_cookie_aqui

# Admin
MEDUSA_ADMIN_EMAIL=admin@ejemplo.com
MEDUSA_ADMIN_PASSWORD=adminpass123

# Entorno
NODE_ENV=development
```

> ⚠️ **Nunca subas tu archivo `.env` real al repositorio.** Está incluido en `.gitignore`.

---

## 🗂️ Estructura del proyecto

```
medusa-project/
├── backend/                  # Servidor MedusaJS (Node.js + TypeScript)
│   ├── src/
│   │   ├── api/              # Endpoints personalizados
│   │   ├── modules/          # Módulos extendidos (Productos, Pedidos)
│   │   ├── subscribers/      # Listeners de eventos
│   │   └── workflows/        # Flujos de negocio
│   ├── medusa-config.ts      # Configuración principal de Medusa
│   └── Dockerfile
│
├── storefront/               # Frontend de la tienda (Next.js)
│   ├── src/
│   │   ├── app/              # App Router de Next.js
│   │   ├── components/       # Componentes reutilizables
│   │   └── lib/              # Utilidades y cliente de la API
│   └── Dockerfile
│
├── .github/
│   └── workflows/
│       ├── ci.yml            # Pipeline CI/CD (lint + test + build)
│       └── burndown.yml      # Generación automática de burndown chart
│
├── docker-compose.yml        # Orquestación de todos los servicios
├── .env.example              # Plantilla de variables de entorno
└── README.md
```

---

## 🧪 Ejecutar pruebas

```bash
# Dentro del contenedor de backend
docker compose exec backend npm run test

# O directamente desde la raíz (requiere Node.js local)
cd backend && npm run test
```

---

## 🔄 Pipeline CI/CD

El proyecto cuenta con un pipeline automatizado en **GitHub Actions** que se ejecuta en cada `push` o `pull request`:

1. **Lint** — Verifica el estilo del código con ESLint
2. **Test** — Ejecuta la suite de pruebas unitarias
3. **Build** — Compila el proyecto TypeScript
4. **Deploy** — Despliega a staging en GitHub Pages (solo en rama `main`)

---

## 👥 Equipo de trabajo

| Integrante | Rol Scrum |
|---|---|
| Rodrigo Flores Núñez | Scrum Master (Sprint 0, 4) |
| Mijael Leon Ramos | Scrum Master (Sprint 1) |
| Mauricio Paredes Miranda | Scrum Master (Sprint 2) |
| Fabricio Jimenez Paredes | Scrum Master (Sprint 3) |

> Todos los integrantes forman parte del **Development Team**: desarrollo, pruebas y documentación técnica.

---

## 📄 Licencia

Licenciado bajo la [MIT License](https://github.com/medusajs/medusa/blob/develop/LICENSE).
