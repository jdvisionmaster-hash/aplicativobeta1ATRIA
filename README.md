# Atria · Generador de Cartas de Cobranza (Beta)

Aplicativo web que genera **cartas de cobranza en PDF** a partir de una
plantilla fija. El usuario solo rellena los campos variables (nombre, cédula,
monto de la deuda, días en mora, etc.) y descarga el documento ya diligenciado.

> **Beta:** una sola plantilla (carta de cobranza), pensada para validar el
> flujo completo *llenar formulario → vista previa en vivo → descargar PDF*.

---

## ✨ Características

- **Sin instalación ni servidor.** Es un único archivo `index.html` estático.
- **Vista previa en vivo:** la hoja A4 se actualiza mientras escribes.
- **Descarga en PDF** usando la impresión nativa del navegador (PDF vectorial,
  sin librerías externas).
- **Formato automático:** monto en pesos colombianos (`$1.250.000`) y fechas en
  español largo (`26 de junio de 2026`).
- **Persistencia local:** tus datos se guardan en el navegador (`localStorage`).
- **100% offline:** no depende de internet ni de CDNs.

---

## 🗂️ Estructura del proyecto

```
aplicativo Atria beta/
├── index.html        ← La aplicación (todo el código está aquí)
├── vercel.json       ← Configuración de despliegue en Vercel
├── .gitignore        ← Archivos que Git debe ignorar
├── README.md         ← Este archivo
└── DESPLIEGUE.md     ← Guía paso a paso: GitHub + Vercel
```

---

## ▶️ Probar en local

No requiere build. Solo abre el archivo:

```bash
# Opción 1: doble clic sobre index.html
# Opción 2: desde terminal (macOS)
open index.html
```

> Para un entorno más cercano a producción puedes servirlo con cualquier
> servidor estático, por ejemplo: `npx serve .`

---

## 🚀 Despliegue

Esta app es **estática**, así que Vercel la publica tal cual sin configuración
extra. Sigue la guía detallada en **[DESPLIEGUE.md](./DESPLIEGUE.md)**.

Resumen rápido:

1. Sube esta carpeta a un repositorio de **GitHub**.
2. Importa el repositorio en **Vercel** (Framework Preset: *Other*).
3. Deploy → obtienes una URL pública `https://<tu-proyecto>.vercel.app`.

---

## 🧪 Cómo verificar que funciona

1. Llena los campos y confirma que la vista previa cambia en tiempo real.
2. Pulsa **⬇ Descargar PDF** → en el diálogo elige *"Guardar como PDF"*.
3. Verifica que el PDF muestra **solo la carta** (sin formulario ni botones).
4. Recarga la página: los datos siguen ahí (localStorage).
5. Pulsa **Limpiar** para reiniciar.

---

## 🛣️ Siguientes pasos (post-beta)

La plantilla está parametrizada con atributos `data-var`, por lo que añadir más
formatos (estado de cuenta, acuerdo de pago, etc.) será cuestión de sumar
plantillas y un selector, sin reescribir la base.
