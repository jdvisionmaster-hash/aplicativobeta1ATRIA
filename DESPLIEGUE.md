# 🚀 Guía de despliegue — GitHub + Vercel

Esta guía te lleva desde la carpeta en tu escritorio hasta una URL pública en
internet. **No necesitas saber programar**; solo seguir los pasos en orden.

La app es **estática** (un solo `index.html`), así que el despliegue es directo:
no hay que compilar nada.

---

## 📋 Requisitos previos

| Necesitas | Dónde conseguirlo |
|-----------|-------------------|
| Cuenta de GitHub | https://github.com/signup (gratis) |
| Cuenta de Vercel | https://vercel.com/signup (gratis — entra con tu GitHub) |
| Git instalado *(solo para la Ruta A)* | https://git-scm.com/downloads |

> 💡 Si no quieres instalar Git, salta a la **Ruta B (sin terminal)** más abajo.

---

## 🅰️ Ruta A — Con Git (terminal)

### Paso 1 · Crear el repositorio en GitHub

1. Entra a https://github.com/new
2. **Repository name:** `atria-cartas-cobranza` (o el nombre que prefieras).
3. Visibilidad: **Private** (recomendado) o **Public**.
4. **No** marques "Add a README" (ya tienes uno).
5. Clic en **Create repository**. Deja esa pantalla abierta: muestra la URL del
   repo (algo como `https://github.com/TU_USUARIO/atria-cartas-cobranza.git`).

### Paso 2 · Subir la carpeta a GitHub

Abre la **Terminal** y ejecuta estos comandos uno por uno.
Primero entra a la carpeta del proyecto:

```bash
cd ~/Desktop/"aplicativo Atria beta"
```

Inicializa Git y sube todo:

```bash
git init
git add .
git commit -m "Beta inicial: generador de cartas de cobranza Atria"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/atria-cartas-cobranza.git
git push -u origin main
```

> 🔑 Cambia `TU_USUARIO` por tu usuario real de GitHub.
> Si te pide usuario/contraseña, usa tu usuario y un **Personal Access Token**
> (GitHub ya no acepta contraseña normal): créalo en
> https://github.com/settings/tokens → *Generate new token (classic)* → marca
> el permiso `repo`.

Recarga la página del repo en GitHub: ya deberías ver tus archivos.

### Paso 3 · Conectar el repo a Vercel

1. Entra a https://vercel.com y haz login con **GitHub**.
2. Botón **Add New…** → **Project**.
3. En la lista, busca `atria-cartas-cobranza` y pulsa **Import**.
   *(Si no aparece, pulsa "Adjust GitHub App Permissions" y dale acceso al repo.)*
4. Configuración del proyecto:
   - **Framework Preset:** `Other`
   - **Root Directory:** `./` (déjalo por defecto)
   - **Build Command:** *(vacío — no hace falta)*
   - **Output Directory:** *(vacío)*
5. Pulsa **Deploy** y espera ~20 segundos.
6. 🎉 Vercel te da una URL como `https://atria-cartas-cobranza.vercel.app`.

---

## 🅱️ Ruta B — Sin terminal (todo desde el navegador)

Ideal si no quieres instalar Git.

### Paso 1 · Subir archivos a GitHub por la web

1. Entra a https://github.com/new y crea el repo (igual que en la Ruta A, Paso 1).
2. En la pantalla del repo vacío, pulsa el enlace **"uploading an existing file"**.
3. Arrastra **todos** los archivos de la carpeta `aplicativo Atria beta`
   (`index.html`, `vercel.json`, `README.md`, `DESPLIEGUE.md`, `.gitignore`).
4. Abajo pulsa **Commit changes**.

### Paso 2 · Importar en Vercel

Igual que la **Ruta A, Paso 3**.

---

## 🔁 Cómo publicar cambios después

Cada vez que actualices algo (por ejemplo el texto de la carta):

**Con Git (Ruta A):**
```bash
cd ~/Desktop/"aplicativo Atria beta"
git add .
git commit -m "Describe aquí tu cambio"
git push
```

**Sin terminal (Ruta B):** entra al repo en GitHub → abre el archivo → ✏️ (editar)
→ guarda con *Commit changes*, o vuelve a subir el archivo.

> ⚡ **Despliegue automático:** Vercel detecta cada `push`/cambio en GitHub y
> vuelve a publicar solo. No tienes que hacer nada más; en segundos tu URL
> muestra la versión nueva.

---

## 🌐 (Opcional) Dominio propio

En Vercel: abre tu proyecto → **Settings → Domains → Add** y escribe tu dominio
(p. ej. `atria.tudominio.com`). Vercel te indica los registros DNS que debes
crear en tu proveedor de dominio.

---

## 🧰 Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| La página se ve en blanco | Vercel no encontró `index.html` en la raíz | Asegúrate de que `index.html` esté en la raíz del repo, no dentro de otra carpeta |
| El repo no aparece en Vercel | Falta dar permiso a la GitHub App | En Vercel → "Adjust GitHub App Permissions" y autoriza el repo |
| `git push` pide contraseña y falla | GitHub ya no acepta contraseña | Usa un **Personal Access Token** (ver Paso 2 de la Ruta A) |
| Cambios no se reflejan | El navegador tiene caché | Recarga con `Cmd+Shift+R` (macOS) |
| El PDF sale con el formulario | Imprimiste la página entera | Usa el botón **Descargar PDF**; el CSS de impresión ya oculta el formulario |

---

## ✅ Checklist final

- [ ] Repo creado en GitHub con los 5 archivos.
- [ ] Proyecto importado en Vercel (Framework: *Other*).
- [ ] Deploy exitoso y URL pública funcionando.
- [ ] Probado: llenar formulario → vista previa → descargar PDF.
- [ ] (Opcional) Dominio propio configurado.
