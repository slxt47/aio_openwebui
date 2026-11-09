## Ollama auf dem Mac

Auf macOS läuft Ollama direkt auf dem Mac (nicht in Docker), damit es die GPU von Apple
Silicon nutzen kann. Open WebUI läuft im Container und spricht über
`host.docker.internal` mit Ollama.

```bash
brew install ollama          # oder die App von https://ollama.com/download
ollama serve &               # bzw. die App starten
ollama pull llama3.2         # ein erstes Modell laden
docker compose up -d         # Open WebUI → http://localhost:3000
```
