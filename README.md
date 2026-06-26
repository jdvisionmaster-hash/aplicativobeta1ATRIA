# Atria · Generador de Cartas de Cobranza (Beta)

Aplicativo web que genera **cartas de cobranza en PDF** a partir de una
plantilla fija. El usuario rellena los campos variables (nombre, cédula,
monto de la deuda, días en mora, etc.) y descarga el documento ya diligenciado.

> **Beta:** una sola plantilla (carta de cobranza), con dos modos de uso:
> **Individual** (un documento) y **Base de datos** (carga masiva desde Excel).

---

## ✨ Características

### 📝 Modo Individual
- Formulario con campos agrupados: entidad, deudor, obligación y firmante.
- **Vista previa en vivo:** la hoja A4 se actualiza mientras escribes.
- **🎤 Dictado por voz** en cada campo — el permiso se solicita **una sola vez**
  al inicio; todos los micrófonos de la página quedan habilitados sin volver a
  preguntar. Lo dictado se corrige automáticamente:
  - Nombres de personas y ciudades → mayúsculas correctas
    (*"juan perez gomez" → "Juan Perez Gomez"*, *"cali" → "Cali"*).
  - Campos de cédula/monto/días → solo dígitos.
- **Corrección al escribir a mano:** al salir del campo, los nombres se
  formatean con mayúsculas automáticamente.
- **Descarga en PDF vectorial** (texto nítido y seleccionable) generado con jsPDF.
- **Persistencia local:** los datos se guardan en `localStorage` y sobreviven recargas.

### 📊 Modo Base de datos (masivo)
- **Descargar plantilla Excel** con las columnas correctas y una fila de ejemplo.
- **Subir archivo** `.xlsx`, `.xls` o `.csv` con tantos deudores como se quiera.
- **Vista de registros** con indicadores de válidos / sin nombre.
- **PDF individual** por fila, descargable desde la tabla.
- **🗑 Quitar archivo:** botón que aparece al cargar el archivo para poder
  eliminarlo y subir uno nuevo sin recargar la página.
- **⬇ Descargar todos los PDF (.zip):** genera un PDF por persona y los
  comprime en un único archivo `.zip`. Si algún registro falla, los demás
  se generan igual y se informa cuántos tuvieron error.
- Las columnas de entidad/firmante vacías en el Excel se completan con los
  datos escritos en la pestaña Individual (valores por defecto compartidos).

### Formato automático
- Monto en pesos colombianos: `$1.250.000`
- Fechas en español largo: `26 de junio de 2026`

---

## ⚠️ Requisitos del navegador

| Función | Requisito |
|---------|-----------|
| 🎤 Dictado por voz | Chrome o Edge (Web Speech API) |
| ⬇ Descarga PDF / ZIP | Conexión a internet (carga jsPDF y JSZip desde CDN) |
| 📂 Lectura de Excel | Conexión a internet (carga SheetJS desde CDN) |

> Al estar desplegado en Vercel (HTTPS) todas las funciones funcionan sin restricciones.

---

## 🗂️ Estructura del proyecto

```
aplicativo Atria beta/
├── index.html        ← La aplicación completa (HTML + CSS + JS en un solo archivo)
├── vercel.json       ← Configuración de despliegue en Vercel
├── .gitignore        ← Archivos que Git debe ignorar
├── README.md         ← Este archivo
└── DESPLIEGUE.md     ← Guía paso a paso: GitHub + Vercel
```

---

## ▶️ Probar en local

No requiere instalación ni build. Solo abre el archivo:

```bash
# Opción 1: doble clic sobre index.html

# Opción 2: desde terminal (macOS)
open index.html

# Opción 3: servidor local (entorno más parecido a producción)
npx serve .
```

> La opción 3 (`npx serve`) es la más recomendada para probar el dictado por voz,
> ya que Chrome restringe la Web Speech API en `file://` pero la permite en `localhost`.

---

## 🚀 Despliegue

Esta app es **estática**: Vercel la publica directamente sin compilar nada.
Sigue la guía en **[DESPLIEGUE.md](./DESPLIEGUE.md)**.

Resumen:
1. Sube esta carpeta a un repositorio de **GitHub**.
2. Importa el repositorio en **Vercel** (Framework Preset: *Other*, sin build command).
3. Deploy → URL pública tipo `https://atria-cartas-cobranza.vercel.app`.

Cada `git push` posterior redespliega automáticamente.

---

## 🧪 Checklist de verificación

**Modo Individual**
- [ ] Llenar campos → vista previa se actualiza en tiempo real.
- [ ] (Chrome/Edge) Pulsar 🎤 en "Nombre completo", dictar → aparece con mayúsculas.
  Pulsar otro 🎤 sin que vuelva a pedir permiso.
- [ ] Pulsar **⬇ Descargar PDF** → se descarga la carta como PDF.
- [ ] Recargar la página → los datos siguen ahí (localStorage).
- [ ] Pulsar **Limpiar** → formulario y vista previa se reinician.

**Modo Base de datos**
- [ ] **Descargar plantilla Excel** → se descarga `plantilla_atria.xlsx`.
- [ ] Llenar 2-3 filas y **subir el archivo** → aparece la tabla con los registros.
- [ ] Aparece el botón **🗑 Quitar archivo** junto al input.
- [ ] Pulsar 🗑 → tabla desaparece, se puede subir un nuevo archivo.
- [ ] Pulsar **PDF** en una fila → descarga un PDF individual.
- [ ] Pulsar **⬇ Descargar todos los PDF (.zip)** → se descarga el `.zip` con un PDF por persona.

---

## 📊 Columnas del Excel

Una fila por persona. El encabezado acepta estos nombres (sin importar tildes ni mayúsculas):

| Campo en Excel | Campo en la carta |
|----------------|-------------------|
| `Empresa` / `Razon social` | Nombre de la entidad |
| `NIT` | NIT |
| `Telefono` / `Tel` / `Celular` | Teléfono |
| `Direccion` / `Dir` | Dirección |
| `Ciudad` | Ciudad de emisión |
| `Nombre del deudor` / `Nombre` / `Deudor` | Nombre del deudor |
| `Cedula` / `Documento` / `CC` | Número de cédula |
| `No Obligacion` / `Referencia` / `Credito` | No. de obligación |
| `Monto` / `Valor` / `Saldo` / `Deuda` | Monto de la deuda |
| `Dias en mora` / `Dias mora` / `Mora` | Días en mora |
| `Fecha limite` / `Vencimiento` | Fecha límite de pago |
| `Fecha carta` / `Fecha` | Fecha de la carta |
| `Firmante` / `Nombre firmante` | Nombre del firmante |
| `Cargo` / `Cargo firmante` | Cargo del firmante |

**Único campo obligatorio:** `Nombre del deudor`. Todos los demás son opcionales
y se completan con los valores de la pestaña Individual si están vacíos.

---

## 🛣️ Siguientes pasos (post-beta)

- Añadir más formatos de documento (estado de cuenta, acuerdo de pago) con un selector de plantilla.
- Corrección ortográfica avanzada más allá de mayúsculas (integración con IA/API).
- Modo offline completo: alojar jsPDF, SheetJS y JSZip en carpeta `vendor/` local.
