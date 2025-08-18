# Práctica Final DevOps — CI/CD con GitHub Actions, Docker y Render

Este repositorio contiene una app **Hola Mundo** con Express (Node.js), pruebas unitarias con **Jest + Supertest**, un **Dockerfile**, y un workflow de **GitHub Actions** que:
1) instala dependencias, 2) ejecuta las pruebas, 3) construye y sube la imagen a Docker Hub, y 4) dispara un deploy en Render vía **Deploy Hook**.

## Requisitos
- Node.js 20+ y npm
- Cuenta en **GitHub**, **Docker Hub** y **Render**
- En tu repo de GitHub, crea estos **Secrets** en *Settings → Secrets and variables → Actions*:
  - `DOCKERHUB_USERNAME` → tu usuario de Docker Hub
  - `DOCKERHUB_TOKEN` → *Access Token* de Docker Hub
  - `RENDER_DEPLOY_HOOK_URL` → URL del Deploy Hook de tu servicio en Render

## Ejecutar local
```bash
npm ci
npm test
npm start
# http://localhost:3000
```

## Docker local
```bash
docker build -t devops-hola-mundo:local .
docker run -p 3000:3000 devops-hola-mundo:local
# http://localhost:3000
```

## Estructura
```
.
├── .dockerignore
├── .gitignore
├── .github/workflows/ci-cd.yml
├── Dockerfile
├── README.md
├── app.js
├── package.json
├── server.js
└── tests/app.test.js
```

## Pasos rápidos para Render (una vez creado el repo en GitHub)
1. En Render, **New → Web Service**.
2. Conecta tu repo de GitHub y elige *Docker* (usará este `Dockerfile`). Crea el servicio.
3. En Render → *Settings* del servicio → **Deploy Hooks** → Generate Hook → copia la URL.
4. Ve a tu repo de GitHub → *Settings → Secrets and variables → Actions* → **New repository secret** con el nombre `RENDER_DEPLOY_HOOK_URL` y pega la URL.
5. En Docker Hub crea un repositorio (por ejemplo `devops-hola-mundo`) y un **Access Token**. Guarda usuario y token como `DOCKERHUB_USERNAME` y `DOCKERHUB_TOKEN` en **Secrets**.
6. Haz push al branch `main`. El workflow hará **test → build & push Docker → deploy**.
