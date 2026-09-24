# Primeros pasos

[English](GETTING_STARTED.md) | Español | [Català](GETTING_STARTED-ca.md)

## Qué hace

MoneyPrinterTurbo convierte un **tema o palabra clave** en un vídeo corto en HD terminado. Le das un tema y escribe el guion, busca o genera el material visual, graba la locución, añade subtítulos y música de fondo, y lo monta todo en un único vídeo. Puedes intervenir y cambiar cualquier etapa del proceso.

## Capacidades

- **Cuatro formas de usarlo:** una WebUI en el navegador, una API REST, una herramienta de línea de comandos (`cli.py`) o un agente de IA que siga [`docs/skill/SKILL.md`](docs/skill/SKILL.md).
- **Guiones:** escritos por IA o propios, en muchos idiomas. Funciona con la mayoría de proveedores de LLM: OpenAI, Anthropic Claude, Gemini, DeepSeek, Qwen, Kimi/Moonshot, Azure OpenAI, Grok, Groq, MiniMax, OpenRouter, Ollama, LiteLLM, OneAPI y otras pasarelas compatibles con OpenAI.
- **Material visual:** tus propias imágenes y vídeos, clips de stock gratuitos de Pexels y Pixabay, Coverr, o clips generados por IA (MiniMax H3, Seedance, WaveSpeed, OFox, MuAPI, Shengsuan Cloud, texto a imagen).
- **Voz:** Edge TTS es gratuito y no necesita clave. También admite Azure, SiliconFlow, Gemini, MiniMax, ElevenLabs, Fish Audio, Kokoro, Chatterbox, VoxCPM y otros. Puedes subir tu propio audio o prescindir de la locución.
- **Subtítulos y música:** la fuente, el color, la posición y el contorno de los subtítulos son configurables. La música de fondo puede ser aleatoria, local o generada por IA, con su propio volumen.
- **Salida:** vertical 9:16, horizontal 16:9 o cuadrado 1:1. Puede generar variantes por lotes, guarda un historial de tareas y publica directamente en TikTok, Instagram y YouTube Shorts.
- **Idiomas de la interfaz:** English, Español, Català, 简体中文 y más. Cambia el idioma desde la configuración de la WebUI.

## Instalación

**Requisitos:** Python 3.11+, al menos 4 núcleos de CPU y 4 GB de RAM (se recomiendan 8 GB). No necesitas GPU.

### Opción A: instalación local con [uv](https://docs.astral.sh/uv/) (recomendada)

```shell
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
uv python install 3.11
uv sync --frozen
```

Si no usas uv, pip también funciona: `python3.11 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`.

### Opción B: Docker

```shell
cp config.example.toml config.toml
docker compose -f docker-compose.release.yml up
```

### Opción C: paquete de un clic para Windows

Descarga el `.7z` desde [Releases](https://github.com/harry0703/MoneyPrinterTurbo/releases/latest) y descomprímelo. Ejecuta primero `update.bat` y después `start.bat`.

### Configuración

En el primer arranque, se crea `config.toml` a partir de `config.example.toml`. Añade tus claves en el panel **Configuración básica** de la WebUI o edita `config.toml` directamente. Como mínimo necesitas:

1. **Un proveedor de LLM** y su clave de API, para escribir el guion. Para un modelo local, usa Ollama, que no necesita clave.
2. **Una clave de fuente de material**. Las claves de Pexels y Pixabay son gratuitas. Puedes omitirla si usas tus propios archivos locales.

## Ejecución

| Modo | Comando | Abrir |
| ---- | ------- | ----- |
| WebUI (macOS/Linux) | `sh webui.sh` | http://127.0.0.1:8501 |
| WebUI (Windows) | `.\webui.bat` | http://127.0.0.1:8501 |
| API | `uv run python main.py` | http://127.0.0.1:8080/docs |
| CLI | `uv run python cli.py --video-subject "Cómo la IA está cambiando la vida cotidiana"` | — |
| Docker | `docker compose -f docker-compose.release.yml up` | :8501 (WebUI) y :8080 (API) |

- Para exponer la WebUI en tu red local, ejecuta `MPT_WEBUI_HOST=0.0.0.0 sh webui.sh` (Windows: `set MPT_WEBUI_HOST=0.0.0.0`).
- Para ver todas las opciones de la CLI, incluidas las ejecuciones por lotes desde un manifiesto JSON (`--batch-file`), ejecuta `uv run python cli.py --help`.
- Los vídeos generados se guardan en `storage/tasks/<task-id>/`.

Para opciones avanzadas, ajustes de voz y subtítulos y solución de problemas, consulta el [README](README-es.md) completo.
