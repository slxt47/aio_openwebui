# aio_openwebui

Fertige `docker-compose.yml`-Dateien für **[Open WebUI](https://github.com/open-webui/open-webui)**
(ChatGPT-ähnliche Oberfläche) mit **[Ollama](https://ollama.com)** für lokale Modelle – für
jede Hardware eine passende Variante.

| Ordner | Für | Was läuft |
|---|---|---|
| [`linux_nvidia/`](linux_nvidia/docker-compose.yml) | Linux mit NVIDIA-GPU | Ollama (GPU) + Open WebUI |
| [`linux_radeon/`](linux_radeon/docker-compose.yml) | Linux mit AMD-GPU (ROCm) | Ollama `:rocm` + Open WebUI |
| [`linux_cpuonly/`](linux_cpuonly/docker-compose.yml) | Linux ohne GPU | Ollama (CPU) + Open WebUI |
| [`macos/`](macos/README.md) | Mac (Apple Silicon) | Ollama nativ, Open WebUI im Container |
| [`all_os_api/`](all_os_api/docker-compose.yml) | überall | nur Open WebUI, Modelle über eine API (OpenAI, Mistral …) |

## Starten

```bash
cd linux_nvidia            # passende Variante wählen
docker compose up -d
docker exec -it ollama ollama pull llama3.2     # erstes Modell laden
```

Dann **http://localhost:3000** öffnen; das erste Konto wird Admin.

Für `all_os_api/` vorher `cp .env.example .env` und den API-Schlüssel eintragen.

### Voraussetzungen

- **NVIDIA:** [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) installiert.
- **AMD:** ROCm-fähige Karte, Benutzer in den Gruppen `video` und `render`.
  Welche Karte drin ist, sagt [checkIfAMD](https://github.com/slxt47/checkIfAMD).

## Sicherheit

Ollama hat **kein Login**. Deshalb sind alle Ports nur auf `127.0.0.1` gebunden. Wer Open WebUI
im Netz braucht, ändert nur dessen Port auf `"3000:8080"` – Ollama bleibt lokal.

## Änderungen (Oktober 2026)

- Fehler behoben: In `all_os_api` fehlte der Port, Open WebUI war nicht erreichbar.
- Ports nur noch auf `127.0.0.1` (Ollama war ohne Passwort im ganzen Netz offen).
- Veraltetes `version: '3.8'` entfernt (Compose v2 warnt sonst).
- macOS-Anleitung korrigiert: Das `install.sh` ist für Linux, auf dem Mac `brew` oder die App.
- `.env` wird ignoriert, `.env.example` mit Beispielen für mehrere Anbieter.
