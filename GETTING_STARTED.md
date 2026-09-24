# Getting Started

English | [Español](GETTING_STARTED-es.md) | [Català](GETTING_STARTED-ca.md)

## What it does

MoneyPrinterTurbo turns a **topic or keyword** into a finished HD short video. Give it a subject and it writes the script, finds or generates footage, records a voiceover, adds subtitles and background music, and edits it all into one video. You can step in and change any stage along the way.

## Capabilities

- **Four ways to use it:** a browser WebUI, a REST API, a command-line tool (`cli.py`), or an AI agent that follows [`docs/skill/SKILL.md`](docs/skill/SKILL.md).
- **Scripts:** AI-written or your own, in many languages. It works with most LLM providers: OpenAI, Anthropic Claude, Gemini, DeepSeek, Qwen, Kimi/Moonshot, Azure OpenAI, Grok, Groq, MiniMax, OpenRouter, Ollama, LiteLLM, OneAPI, and other OpenAI-compatible gateways.
- **Footage:** your own images and videos, free stock clips from Pexels and Pixabay, Coverr, or AI-generated clips (MiniMax H3, Seedance, WaveSpeed, OFox, MuAPI, Shengsuan Cloud, text-to-image).
- **Voice:** Edge TTS is free and needs no key. Azure, SiliconFlow, Gemini, MiniMax, ElevenLabs, Fish Audio, Kokoro, Chatterbox, VoxCPM and others are also supported. You can upload your own audio or skip the voiceover.
- **Subtitles and music:** subtitle font, color, position and outline are all configurable. Background music can be random, local or AI-generated, with its own volume.
- **Output:** portrait 9:16, landscape 16:9 or square 1:1. It can batch-generate variants, keeps a task history, and publishes directly to TikTok, Instagram and YouTube Shorts.
- **Interface languages:** English, Español, Català, 简体中文 and more. Switch the language from the WebUI settings.

## Setup

**Requirements:** Python 3.11+, at least 4 CPU cores and 4 GB of RAM (8 GB recommended). You don't need a GPU.

### Option A: Local install with [uv](https://docs.astral.sh/uv/) (recommended)

```shell
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
uv python install 3.11
uv sync --frozen
```

If you don't use uv, pip also works: `python3.11 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`.

### Option B: Docker

```shell
cp config.example.toml config.toml
docker compose -f docker-compose.release.yml up
```

### Option C: Windows one-click package

Download the `.7z` from [Releases](https://github.com/harry0703/MoneyPrinterTurbo/releases/latest) and extract it. Run `update.bat` first, then `start.bat`.

### Configure

On first launch, `config.toml` is created from `config.example.toml`. Add your keys in the WebUI **Basic Settings** panel, or edit `config.toml` directly. At minimum you need:

1. **An LLM provider** and its API key, to write the script. For a local model, use Ollama, which needs no key.
2. **A footage source key**. Pexels and Pixabay keys are free. You can skip this if you use your own local media.

## Run

| Mode | Command | Open |
| ---- | ------- | ---- |
| WebUI (macOS/Linux) | `sh webui.sh` | http://127.0.0.1:8501 |
| WebUI (Windows) | `.\webui.bat` | http://127.0.0.1:8501 |
| API | `uv run python main.py` | http://127.0.0.1:8080/docs |
| CLI | `uv run python cli.py --video-subject "How AI is changing everyday life"` | — |
| Docker | `docker compose -f docker-compose.release.yml up` | :8501 (WebUI) and :8080 (API) |

- To expose the WebUI on your LAN, run `MPT_WEBUI_HOST=0.0.0.0 sh webui.sh` (Windows: `set MPT_WEBUI_HOST=0.0.0.0`).
- To see every CLI option, including batch runs from a JSON manifest (`--batch-file`), run `uv run python cli.py --help`.
- Generated videos are saved under `storage/tasks/<task-id>/`.

For advanced options, voice and subtitle tuning, and troubleshooting, see the full [README](README-en.md) ([ES](README-es.md) · [CA](README-ca.md)).
