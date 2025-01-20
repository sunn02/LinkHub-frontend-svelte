
# 🌟 Frontend Svelte

Este repositorio contiene la versión del frontend del proyecto **LinkHub**, desarrollada con **Svelte**.

## ✅ Requisitos Previos

- [Node.js](https://nodejs.org/) instalado en tu sistema.

---

## 🛠️ Cómo Instalar

1. Clona este repositorio:
   ```bash
   git clone https://github.com/sunn02/LinkHub-frontend-svelte
   cd LinkHub-frontend-svelte/link-project
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

---

## ▶️ Cómo Ejecutar

1. Inicia el servidor de desarrollo:
   ```bash
   npm run dev
   ```

2. Abre tu navegador y visita [http://localhost:5173](http://localhost:5173).

---

## 🚀 Cómo Desplegar

1. Genera una versión optimizada para producción:
   ```bash
   npm run build
   ```

2. Sube la carpeta `build/` a cualquier servicio de hosting estático, como:
   - **Netlify**
   - **Vercel**
   - **GitHub Pages**
   - Cualquier servidor estático.

---

## 📜 Notas

- Este proyecto es una **Single Page Application (SPA)** que se conecta a un backend RESTful para manejar enlaces, comentarios y votos.
- Configura la URL del backend en el archivo `api.js`:
   ```
   const API_URL = "http://localhost:3005";
   ```

