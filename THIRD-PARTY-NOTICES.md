# Componentes de terceros

En Reelith Studio usamos estos componentes de código abierto y de terceros. Cada uno conserva su propia licencia.

| Componente | Para qué lo usa | Licencia |
| --- | --- | --- |
| [GStreamer](https://gstreamer.freedesktop.org) 1.26.11 y sus plugins | Motor de vídeo y audio | LGPL 2.1 o posterior |
| [FFmpeg](https://ffmpeg.org), dentro de gst-libav | Codificar el audio AAC | LGPL 2.1 o posterior |
| [x264](https://www.videolan.org/developers/x264.html), dentro de GStreamer | Codificar el vídeo H.264 con el procesador | GPL 2.0 o posterior |
| [gstreamer-rs](https://gitlab.freedesktop.org/gstreamer/gstreamer-rs) | Unir la aplicación con GStreamer | MIT o Apache 2.0 |
| [Tauri](https://tauri.app) | Ventanas y empaquetado | MIT o Apache 2.0 |
| [React](https://react.dev), [Tailwind CSS](https://tailwindcss.com), [Lucide](https://lucide.dev) | Interfaz | MIT e ISC |
| [Simple Icons](https://simpleicons.org) | Logotipos de las plataformas | CC0 1.0 |
| [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2) | Mostrar páginas web en Windows | Licencia de Microsoft |
| Microsoft Visual C++ Redistributable | Bibliotecas de ejecución de Windows | Licencia de Microsoft |

## GStreamer y FFmpeg (LGPL)

El instalador de Windows y el DMG de Mac incluyen GStreamer 1.26.11 y solo los plugins que la aplicación usa, tal y como los publica el proyecto GStreamer.

- Código fuente de GStreamer 1.26.11: https://gstreamer.freedesktop.org/src/
- El FFmpeg que se usa es el que se compila dentro de gst-libav 1.26.11. Su código fuente va en el paquete `gst-libav` de esa misma versión: https://gstreamer.freedesktop.org/src/gst-libav/

Todas estas bibliotecas se enlazan de forma dinámica y puedes sustituirlas por otras versiones compatibles, compiladas por ti a partir de ese código fuente: Reelith Studio las usará.

- En Windows son archivos `.dll` independientes y sin modificar, en la carpeta de instalación junto al programa (los plugins, en la subcarpeta `gstreamer-1.0`).
- En Mac son archivos `.dylib` independientes dentro de la aplicación: las bibliotecas en `Contents/Frameworks` y los plugins en `Contents/PlugIns/gstreamer`. Su código es el que publica el proyecto GStreamer. Solo les quitamos la mitad para Mac con Intel, les indicamos que se busquen unas a otras dentro de la aplicación y las firmamos, como pide macOS. Si cambias alguna, tienes que volver a firmar la aplicación (`codesign --force --deep --sign - "Reelith Studio.app"`).

## Codificación de vídeo

El vídeo H.264 lo codifica la tarjeta gráfica (NVIDIA NVENC, Intel Quick Sync o AMD AMF en Windows; el chip de Apple, con VideoToolbox, en Mac). Cuando el equipo no tiene codificador de vídeo, o si eliges el procesador, se usa x264, que va incluido como plugin de GStreamer (`gstx264.dll` en Windows, `libgstx264.dylib` en Mac), con licencia GPL 2.0 o posterior. Su código fuente está en https://code.videolan.org/videolan/x264

## Contacto

Si crees que nos falta algún aviso de licencia o quieres pedirnos algo sobre estos componentes, [abre un aviso](https://github.com/ReelithLabs/reelith-studio-releases/issues/new/choose).
