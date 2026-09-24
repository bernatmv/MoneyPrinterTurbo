# Primers passos

[English](GETTING_STARTED.md) | [Español](GETTING_STARTED-es.md) | Català

## Què fa

MoneyPrinterTurbo converteix un **tema o paraula clau** en un vídeo curt en HD acabat. Li dones un tema i escriu el guió, cerca o genera el material visual, enregistra la locució, afegeix subtítols i música de fons, i ho munta tot en un únic vídeo. Pots intervenir i canviar qualsevol etapa del procés.

## Capacitats

- **Quatre maneres de fer-lo servir:** una WebUI al navegador, una API REST, una eina de línia d'ordres (`cli.py`) o un agent d'IA que segueixi [`docs/skill/SKILL.md`](docs/skill/SKILL.md).
- **Guions:** escrits per IA o propis, en molts idiomes. Funciona amb la majoria de proveïdors de LLM: OpenAI, Anthropic Claude, Gemini, DeepSeek, Qwen, Kimi/Moonshot, Azure OpenAI, Grok, Groq, MiniMax, OpenRouter, Ollama, LiteLLM, OneAPI i altres passarel·les compatibles amb OpenAI.
- **Material visual:** les teves pròpies imatges i vídeos, clips d'estoc gratuïts de Pexels i Pixabay, Coverr, o clips generats per IA (MiniMax H3, Seedance, WaveSpeed, OFox, MuAPI, Shengsuan Cloud, text a imatge).
- **Veu:** Edge TTS és gratuït i no necessita clau. També admet Azure, SiliconFlow, Gemini, MiniMax, ElevenLabs, Fish Audio, Kokoro, Chatterbox, VoxCPM i altres. Pots pujar el teu propi àudio o prescindir de la locució.
- **Subtítols i música:** el tipus de lletra, el color, la posició i el contorn dels subtítols són configurables. La música de fons pot ser aleatòria, local o generada per IA, amb el seu propi volum.
- **Sortida:** vertical 9:16, horitzontal 16:9 o quadrat 1:1. Pot generar variants per lots, desa un historial de tasques i publica directament a TikTok, Instagram i YouTube Shorts.
- **Idiomes de la interfície:** English, Español, Català, 简体中文 i més. Canvia l'idioma des de la configuració de la WebUI.

## Instal·lació

**Requisits:** Python 3.11+, com a mínim 4 nuclis de CPU i 4 GB de RAM (se'n recomanen 8 GB). No necessites GPU.

### Opció A: instal·lació local amb [uv](https://docs.astral.sh/uv/) (recomanada)

```shell
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
uv python install 3.11
uv sync --frozen
```

Si no fas servir uv, pip també funciona: `python3.11 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`.

### Opció B: Docker

```shell
cp config.example.toml config.toml
docker compose -f docker-compose.release.yml up
```

### Opció C: paquet d'un clic per a Windows

Descarrega el `.7z` des de [Releases](https://github.com/harry0703/MoneyPrinterTurbo/releases/latest) i descomprimeix-lo. Executa primer `update.bat` i després `start.bat`.

### Configuració

En el primer arrencament, es crea `config.toml` a partir de `config.example.toml`. Afegeix les teves claus al tauler **Configuració bàsica** de la WebUI o edita `config.toml` directament. Com a mínim necessites:

1. **Un proveïdor de LLM** i la seva clau d'API, per escriure el guió. Per a un model local, fes servir Ollama, que no necessita clau.
2. **Una clau de font de material**. Les claus de Pexels i Pixabay són gratuïtes. Pots ometre-la si fas servir els teus propis fitxers locals.

## Execució

| Mode | Ordre | Obrir |
| ---- | ----- | ----- |
| WebUI (macOS/Linux) | `sh webui.sh` | http://127.0.0.1:8501 |
| WebUI (Windows) | `.\webui.bat` | http://127.0.0.1:8501 |
| API | `uv run python main.py` | http://127.0.0.1:8080/docs |
| CLI | `uv run python cli.py --video-subject "Com la IA està canviant la vida quotidiana"` | — |
| Docker | `docker compose -f docker-compose.release.yml up` | :8501 (WebUI) i :8080 (API) |

- Per exposar la WebUI a la xarxa local, executa `MPT_WEBUI_HOST=0.0.0.0 sh webui.sh` (Windows: `set MPT_WEBUI_HOST=0.0.0.0`).
- Per veure totes les opcions de la CLI, incloses les execucions per lots des d'un manifest JSON (`--batch-file`), executa `uv run python cli.py --help`.
- Els vídeos generats es desen a `storage/tasks/<task-id>/`.

Per a opcions avançades, ajustos de veu i subtítols i resolució de problemes, consulta el [README](README-ca.md) complet.
