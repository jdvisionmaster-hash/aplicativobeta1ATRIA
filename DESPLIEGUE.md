# 🚀 Guía de despliegue — GitHub + Vercel

Esta guía cubre dos escenarios:
- **Primera vez:** crear el repo y conectarlo a Vercel.
- **Actualizar:** subir cambios a un repo ya existente para que Vercel redespliegue.

La app es **estática** (un solo `index.html`): no hay que compilar nada.

---

## 📋 Requisitos previos

| Necesitas | Dónde conseguirlo |
|-----------|-------------------|
| Cuenta de GitHub | https://github.com/signup (gratis) |
| Cuenta de Vercel | https://vercel.com/signup (gratis — entra con tu GitHub) |
| Git instalado *(solo Ruta A)* | https://git-scm.com/downloads |

> 💡 Sin Git, salta directo a la **Ruta B (sin terminal)**.

---

## 🔁 Actualizar un despliegue ya existente

Si ya tienes el repo en GitHub y Vercel conectado, **solo necesitas subir los
archivos actualizados**. Vercel redespliegue automáticamente en segundos.

### Con Git (terminal)

```bash
cd ~/Desktop/"aplicativo Atria beta"
git add .
git commit -m "Actualización: dictado voz, limpiar archivo, descarga ZIP"
git push
```

Vercel detecta el `push` y publica la nueva versión sin que hagas nada más.

### Sin terminal (desde el navegador)

1. Abre tu repositorio en GitHub.
2. Haz clic en el archivo que quieres actualizar (p. ej. `index.html`).
3. Pulsa el ✏️ (lápiz) para editarlo, o usa el botón **"Add file → Upload files"**
   para reemplazar varios archivos a la vez arrastrándolos.
4. Al guardar, pulsa **Commit changes** → Vercel redespliegue automáticamente.

---

## 🆕 Primera vez — Crear repo y conectar a Vercel

### 🅰️ Ruta A — Con Git (terminal)

#### Paso 1 · Crear el repositorio en GitHub

1. Abre https://github.com/new
2. **Repository name:** `atria-cartas-cobranza` (sin espacios).
3. Visibilidad: **Private** (recomendado) o **Public**.
4. **No** marques "Add a README" (ya tienes uno).
5. Pulsa **Create repository** y deja esa pantalla abierta (muestra la URL del repo).

#### Paso 2 · Subir la carpeta desde Terminal

```bash
cd ~/Desktop/"aplicativo Atria beta"
git init
git add .
git commit -m "Beta inicial: generador de cartas de cobranza Atria"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/atria-cartas-cobranza.git
git push -u origin main
```

> 🔑 Cambia `TU_USUARIO` por tu usuario real de GitHub.
> Si te pide contraseña: GitHub ya no acepta contraseña normal. Crea un
> **Personal Access Token** en https://github.com/settings/tokens →
> *Generate new token (classic)* → marca el permiso `repo` → copia el token
> y úsalo como contraseña.

Recarga el repo en GitHub — deberías ver todos los archivos.

#### Paso 3 · Conectar a Vercel

1. Entra a https://vercel.com → login con GitHub.
2. Pulsa **Add New… → Project**.
3. Busca `atria-cartas-cobranza` y pulsa **Import**.
   *(Si no aparece: pulsa "Adjust GitHub App Permissions" y autoriza el repo.)*
4. Configura así:
   - **Framework Preset:** `Other`
   - **Root Directory:** `./` (dejar por defecto)
   - **Build Command:** *(dejar vacío)*
   - **Output Directory:** *(dejar vacío)*
5. Pulsa **Deploy** → espera ~20 segundos.
6. 🎉 Recibes una URL pública como `https://atria-cartas-cobranza.vercel.app`.

---

### 🅱️ Ruta B — Sin terminal (todo desde el navegador)

#### Paso 1 · Subir archivos a GitHub

1. Abre https://github.com/new y crea el repo (igual que Ruta A, Paso 1).
2. En la pantalla del repo vacío, pulsa **"uploading an existing file"**.
3. Arrastra los 5 archivos de la carpeta `aplicativo Atria beta`:
   - `index.html`
   - `vercel.json`
   - `README.md`
   - `DESPLIEGUE.md`
   - `.gitignore`
4. Pulsa **Commit changes**.

#### Paso 2 · Conectar a Vercel

Igual que **Ruta A, Paso 3**.

---

## 🌐 (Opcional) Dominio propio

En Vercel: abre tu proyecto → **Settings → Domains → Add** → escribe tu dominio
(p. ej. `atria.tuempresa.com`). Vercel indica los registros DNS que debes crear
en tu proveedor de dominio.

---

## 🧰 Solución de problemas

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| La página se ve en blanco | `index.html` no está en la raíz del repo | Verifica que el archivo esté directamente en la raíz, no dentro de una subcarpeta |
| El repo no aparece en Vercel | Falta permiso a la GitHub App | Vercel → "Adjust GitHub App Permissions" → autoriza el repo |
| `git push` pide contraseña y falla | GitHub ya no acepta contraseña | Usa un Personal Access Token (ver Paso 2, Ruta A) |
| Cambios publicados pero no se ven | Caché del navegador | Recarga con `Cmd+Shift+R` (macOS) |
| El PDF no se descarga | jsPDF no cargó (sin internet) | Verifica conexión; en Vercel/producción no ocurre |
| El .zip no se descarga | JSZip no cargó (sin internet) | Ídem; recarga la página con conexión activa |
| El dictado por voz no funciona | Navegador no compatible | Usa Chrome o Edge; Safari no soporta Web Speech API |
| El dictado pide permiso en cada campo | Instancia de reconocimiento duplicada | Esto está corregido en la versión actual; recarga la página |
| No puedo cambiar el archivo Excel | Falta el botón "Quitar archivo" | Está en la versión actual; si no aparece, recarga la página |

---

## ✅ Checklist de primer despliegue

- [ ] Repo creado en GitHub con los 5 archivos (`index.html`, `vercel.json`, `README.md`, `DESPLIEGUE.md`, `.gitignore`).
- [ ] Proyecto importado en Vercel (Framework: *Other*, sin build command).
- [ ] Deploy exitoso → URL pública funcionando.
- [ ] Probado en la URL de Vercel: Individual → llenar → PDF descargado.
- [ ] Probado: Base de datos → subir CSV/Excel → descargar ZIP.
- [ ] Probado: dictado por voz (Chrome/Edge) — permiso pedido una sola vez.
- [ ] (Opcional) Dominio propio configurado.
