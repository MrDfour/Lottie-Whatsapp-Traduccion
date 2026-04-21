# 🧩 Lottie Sticker Builder (WAS) — Beta

Transforma una imagen (**buffer** o **archivo**) en un sticker animado `.was` (Lottie) listo para usar en WhatsApp.

---

## ⚡ Instalación

### 1. Clona o descarga el proyecto

```bash
git clone https://github.com/Pedrozz13755/Lottie-Whatsapp.git
cd Lottie-Whatsapp
```

O, si prefieres, simplemente coloca los archivos dentro de tu propio proyecto.

---

### 2. Instala las dependencias necesarias

Este código utiliza solo módulos nativos de Node.js, pero necesita que el comando `zip` esté instalado en el sistema.

En Linux / Termux / Ubuntu:

```bash
pkg install zip
# o
apt install zip
```

---

## 📦 Estructura esperada

Necesitas una carpeta base con los archivos de Lottie. Ejemplo:

```
src/
 └── exemple/
      └── animation/
           └── animation_secondary.json
```

Este archivo JSON debe contener previamente una imagen en base64, ya que el builder la reemplazará de forma automática.

---

## 🚀 Cómo usarlo

### Importa la función

```js
const { buildLottieSticker } = require("./src/index");
```

---

### Ejemplo básico

```js
const path = require("path");
const { buildLottieSticker } = require("./src/index");

const output = await buildLottieSticker({
  baseFolder: path.resolve(__dirname, "src", "exemple"),
  buffer: dfileBuffer,
  mime: "image/jpeg",
  output: path.resolve(__dirname, "jurubeba.was")
});
```

---

### Enviar en WhatsApp con Baileys

```js
const fs = require("fs");

await client.sendMessage(from, {
  sticker: fs.readFileSync("./jurubeba.was"),
  mimetype: "application/was"
});
```

---

## 🧠 Parámetros

| Nombre | Tipo | Requerido | Descripción |
|--------|------|-----------|-------------|
| `baseFolder` | string | ✅ | Carpeta base del Lottie |
| `buffer` | Buffer | ❌ | Imagen en memoria |
| `imagePath` | string | ❌ | Ruta de la imagen |
| `mime` | string | ❌ | Tipo de imagen (se detecta automáticamente si usas `imagePath`) |
| `output` | string | ❌ | Ruta del archivo `.was` final |
| `jsonRelativePath` | string | ❌ | Ruta del JSON dentro de la carpeta base |

---

## ⚠️ Reglas importantes

- Debes enviar **`buffer` o `imagePath`**
- Formatos soportados:
  - PNG
  - JPG / JPEG
  - WEBP
- El JSON del Lottie debe tener ya una imagen en base64 embebida
- El código solo reemplaza la imagen existente, no crea la estructura del Lottie desde cero

---

## 💥 Errores comunes

### `Mime não detectado`
No enviaste `mime` ni `imagePath`

### `JSON sem assets`
El archivo JSON es inválido o no tiene la estructura esperada

### `Nenhuma imagem base64 encontrada no Lottie`
Tu archivo Lottie no contiene una imagen embebida en base64 para reemplazar

### `zip não encontrado`
El comando `zip` no está instalado en el sistema

---

## 🛠️ Consejo útil

Si quieres usarlo directamente con una imagen recibida por WhatsApp, puedes obtener el buffer y enviárselo al builder:

```js
const buffer = await getFileBuffer(message, "image");

const output = await buildLottieSticker({
  baseFolder: path.resolve(__dirname, "src", "exemple"),
  buffer,
  mime: "image/jpeg",
  output: path.resolve(__dirname, "jurubeba.was")
});
```

---

## 🚧 Estado del proyecto

> ⚠️ **VERSIÓN BETA**
>
> Este proyecto aún se encuentra en fase beta.
> Dependiendo del archivo Lottie utilizado, algunas animaciones pueden no funcionar correctamente.
> Todavía no existe soporte garantizado para todos los tipos de estructura Lottie.

---

## 👑 Créditos

Desarrollado por **Pedrozz Mods**

Este proyecto todavía está en desarrollo y en versión beta.
Si lo usas, modificas o compartes, mantén los créditos.

Grupo: https://chat.whatsapp.com/C21cogFUmKABh9e3qyexSQ?mode=gi_t
Canal: https://whatsapp.com/channel/0029Vb8CYiZChq6RIEfS7K1D

---

### Footer

Hecho por **Pedrozz Mods**  
Proyecto en **versión beta**, sujeto a cambios y posibles errores.
