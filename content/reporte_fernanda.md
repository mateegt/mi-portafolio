# Creación de Mi Portafolio con Hugo y GitHub Pages

**Alumna:** Fernanda Itzel Flores Valenzuela  
**Usuario GitHub:** pinapinv  
**Fecha:** 13 de noviembre de 2025  

---

## Introducción

En este reporte documento el proceso que seguí para crear mi portafolio personal utilizando Hugo como generador de sitios estáticos y GitHub Pages para el hosting. El objetivo principal fue aprender a integrar tecnologías de control de versiones, Markdown, y automatización con GitHub Actions para tener un sitio web profesional donde publicar mis prácticas y proyectos.

---

## Requisitos Previos

Antes de comenzar, me aseguré de tener instalado en mi computadora Windows:

- **Git para Windows**: Lo descargué desde [https://git-scm.com/downloads](https://git-scm.com/downloads)
- **Hugo Extended**: Necesario para el tema que elegí
- **Editor de texto**: Usé Visual Studio Code
- **Cuenta de GitHub**: Mi usuario es `pinapinv`

---

## Paso 1: Instalación de Hugo

Lo primero que hice fue instalar Hugo en mi computadora. Seguí estos pasos:

### Descarga de Hugo

1. Entré a [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases)
2. Busqué la versión más reciente (v0.146.0 o superior)
3. Descargué el archivo `hugo_extended_0.146.0_windows-amd64.zip`
4. Extraje el archivo en `C:\Hugo\bin`
5. Agregué esta ruta a las variables de entorno PATH de Windows

### Verificación

Abrí Git Bash y ejecuté:

```bash
hugo version
```

Confirmé que mostraba la versión instalada correctamente.

---

## Paso 2: Creación del Sitio Hugo

Una vez instalado Hugo, procedí a crear mi sitio web.

### Crear el proyecto

Abrí Git Bash y ejecuté los siguientes comandos:

```bash
# Crear el sitio
hugo new site mi-portafolio

# Entrar a la carpeta
cd mi-portafolio
```

Esto creó una carpeta llamada `mi-portafolio` con toda la estructura básica de Hugo.

### Inicializar Git

Dentro de la carpeta del proyecto, inicialicé Git:

```bash
git init
```

También configuré mi información personal:

```bash
git config --global user.name "Fernanda Itzel Flores Valenzuela"
git config --global user.email "mi-email@ejemplo.com"
```

Para evitar problemas con los formatos de línea en Windows, ejecuté:

```bash
git config --global core.autocrlf true
```

---

## Paso 3: Instalación del Tema PaperMod

Decidí usar el tema PaperMod porque tiene un diseño limpio y profesional.

### Agregar el tema

Ejecuté este comando para instalar el tema como un submódulo de Git:

```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

Luego actualicé el submódulo:

```bash
git submodule update --init --recursive
```

---

## Paso 4: Configuración Inicial

### Crear el archivo .gitignore

Antes de hacer mi primer commit, creé un archivo `.gitignore` para evitar subir archivos innecesarios a GitHub. 

Desde Git Bash ejecuté:

```bash
type nul > .gitignore
notepad .gitignore
```

Y agregué este contenido:

```
# Hugo
public/
resources/
.hugo_build.lock

# OS
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
*.swp
```

### Configurar hugo.toml

Abrí el archivo `hugo.toml` con VSCode y lo configuré así:

```toml
baseURL = 'https://pinapinv.github.io/mi-portafolio/'
languageCode = 'es-mx'
title = 'Portafolio de Fernanda Flores'
theme = 'PaperMod'

[params]
  description = "Portafolio personal y prácticas universitarias"
  author = "Fernanda Itzel Flores Valenzuela"
  ShowReadingTime = true
  ShowShareButtons = true
  ShowPostNavLinks = true
  ShowBreadCrumbs = true
  ShowCodeCopyButtons = true

[menu]
  [[menu.main]]
    name = "Inicio"
    url = "/"
    weight = 1
  
  [[menu.main]]
    name = "Blog"
    url = "/posts/"
    weight = 2
  
  [[menu.main]]
    name = "Prácticas"
    url = "/practicas/"
    weight = 3
  
  [[menu.main]]
    name = "Acerca de"
    url = "/about/"
    weight = 4
```

---

## Paso 5: Creación de Contenido

### Mi primera entrada

Creé mi primera entrada de blog con:

```bash
hugo new posts/bienvenida.md
```

Edité el archivo `content/posts/bienvenida.md`:

```markdown
---
title: "Bienvenida a Mi Portafolio"
date: 2025-11-13
draft: false
tags: ["inicio"]
---

# ¡Hola!

Soy Fernanda Flores y este es mi portafolio personal donde 
documentaré mis prácticas y proyectos universitarios.
```

### Sección de prácticas

Creé una carpeta para mis prácticas:

```bash
mkdir content/practicas
```

Y creé el archivo índice:

```bash
hugo new practicas/_index.md
```

Lo edité así:

```markdown
---
title: "Prácticas"
description: "Documentación de mis prácticas universitarias"
---

# 📚 Mis Prácticas

Aquí encontrarás la documentación de todas las prácticas 
que he realizado durante el curso.
```

### Página Acerca de

Creé mi página personal:

```bash
hugo new about.md
```

Y la edité:

```markdown
---
title: "Acerca de Mí"
date: 2025-11-13
---

# 👋 Hola, soy Fernanda

Estudiante apasionada por la tecnología y el desarrollo web.

## Contacto
- GitHub: [@pinapinv](https://github.com/pinapinv)
```

### Probar localmente

Antes de subir todo a GitHub, probé que funcionara correctamente:

```bash
hugo server -D
```

Abrí mi navegador en `http://localhost:1313` y verifiqué que todo se viera bien.

---

## Paso 6: Subir a GitHub

### Crear el repositorio

1. Entré a [https://github.com/new](https://github.com/new)
2. Nombre del repositorio: `mi-portafolio`
3. Lo dejé como público
4. NO marqué ninguna opción adicional
5. Clickeé en "Create repository"

### Conectar mi proyecto local

Desde Git Bash, en mi carpeta del proyecto, ejecuté:

```bash
# Agregar todos los archivos
git add .

# Hacer mi primer commit
git commit -m "Configuración inicial del portafolio"

# Conectar con GitHub
git remote add origin https://github.com/pinapinv/mi-portafolio.git

# Cambiar a la rama main
git branch -M main

# Subir los archivos
git push -u origin main
```

---

## Paso 7: Configurar GitHub Actions

Esta fue la parte más importante para lograr el despliegue automático.

### Crear el archivo de workflow

Desde Git Bash creé las carpetas necesarias:

```bash
mkdir .github
mkdir .github/workflows
```

Luego creé el archivo del workflow:

```bash
type nul > .github/workflows/hugo.yml
notepad .github/workflows/hugo.yml
```

Pegué este contenido:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.146.0
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb

      - name: Install Dart Sass
        run: sudo snap install dart-sass

      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5

      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"

      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
          TZ: America/Mexico_City
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Subir el workflow

```bash
git add .github/workflows/hugo.yml
git commit -m "Agregar GitHub Actions para despliegue automático"
git push
```

---

## Paso 8: Configurar GitHub Pages

### Habilitar GitHub Pages

1. Entré a mi repositorio: `https://github.com/pinapinv/mi-portafolio`
2. Clickeé en **Settings**
3. En el menú lateral busqué **Pages**
4. En **Source** seleccioné: **GitHub Actions**

### Configurar permisos

Este paso fue crucial. Muchas veces este paso causa errores si no se hace.

1. En **Settings**, fui a **Actions** → **General**
2. Bajé hasta **"Workflow permissions"**
3. Seleccioné: **"Read and write permissions"**
4. Marqué: **"Allow GitHub Actions to create and approve pull requests"**
5. Clickeé en **Save**

---

## Paso 9: Verificación del Despliegue

### Ver el proceso

1. Fui a la pestaña **Actions** de mi repositorio
2. Vi que había un workflow ejecutándose llamado "Deploy Hugo site to Pages"
3. Esperé aproximadamente 2 minutos

### Resultado

El workflow terminó exitosamente con un check verde ✅

Mi sitio quedó publicado en: **https://pinapinv.github.io/mi-portafolio/**

---

## Estructura Final del Proyecto

Así quedó organizado mi proyecto:

```
mi-portafolio/
├── .github/
│   └── workflows/
│       └── hugo.yml              # Automatización con GitHub Actions
├── .gitignore                    # Archivos a ignorar
├── content/
│   ├── posts/
│   │   └── bienvenida.md         # Primera entrada
│   ├── practicas/
│   │   └── _index.md             # Índice de prácticas
│   └── about.md                  # Acerca de mí
├── themes/
│   └── PaperMod/                 # Tema instalado
├── hugo.toml                     # Configuración principal
└── README.md
```

---

## Flujo de Trabajo para Futuras Actualizaciones

Ahora que tengo todo configurado, cada vez que quiera agregar una nueva práctica o entrada haré lo siguiente:

```bash
# 1. Crear nueva práctica
hugo new practicas/practica-2.md

# 2. Editar el archivo en content/practicas/

# 3. Probar localmente (opcional)
hugo server -D

# 4. Subir a GitHub
git add .
git commit -m "Agregar práctica 2"
git push
```

GitHub Actions se encarga automáticamente de construir y publicar mi sitio actualizado en aproximadamente 2 minutos.

---

## Conclusiones

---

## Referencias

### Documentación consultada

- **Hugo Documentation**: [https://gohugo.io/documentation/](https://gohugo.io/documentation/)
- **GitHub Pages Docs**: [https://docs.github.com/pages](https://docs.github.com/pages)
- **GitHub Actions Docs**: [https://docs.github.com/actions](https://docs.github.com/actions)
- **PaperMod Theme**: [https://github.com/adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod)
- **Markdown Guide**: [https://www.markdownguide.org/](https://www.markdownguide.org/)

### Recursos útiles

- **Git Bash para Windows**: [https://git-scm.com/downloads](https://git-scm.com/downloads)
- **Hugo Releases**: [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases)
- **Visual Studio Code**: [https://code.visualstudio.com/](https://code.visualstudio.com/)

---

**Repositorio del proyecto:** [https://github.com/pinapinv/mi-portafolio](https://github.com/pinapinv/mi-portafolio)  
**Sitio web publicado:** [https://pinapinv.github.io/mi-portafolio/](https://pinapinv.github.io/mi-portafolio/)

---

*Fernanda Itzel Flores Valenzuela*  
*13 de noviembre de 2025*