# rpa-llm4bits
Einfaches lokales Setup für RPA-Workflows mit LLM-Integration.

Verwendet folgende Softwarekomponenten:
- [ollama](https://ollama.com/) - Modell-Wrapper mit OpenAI-API Kompatibilität
- [n8n](https://n8n.io/) - Workflow Builder

## Voraussetzungen
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installiert
- (opt.) dedizierte GPU vorhanden

## Einrichtung
### Repository herunterladen und extrahieren
Zunächst muss dieses Repository ([rpa-llm4bits-main.zip](https://github.com/schreinerbayern/rpa-llm4bits/archive/refs/heads/main.zip)) heruntergeladen und entpackt werden.
Anschließend wird innerhalb des Ordners ein Recktsklick druchgeführt und die Option `In Terminal öffnen` ausgewählt. Es öffnet sich eine Kommandozeile in der die folgenden Befehle ausgeführt werden können.

> **Hinweis:**  
> Es ist wichtig, dass das Terminal bzw. die Kommandozeile innerhalb des Ordners geöffnet wurden. Andernfalls können die Befehle nicht richtig durchgeführt werden.

### Cluster starten
Die Services werden als Container-Cluster mit folgendem Befehl über die Kommandozeile gestartet:

```sh
# Start-Befehl
docker-compose up --remove-orphans -d
# Parameter: --remove-orphans (entfernt Container, die nicht mehr definiert sind)
# Parameter: -d (lässt Container im Hintergrund laufen)
```

Sobald der Start-Befehl eingegeben wird, werden die entsprechenden Container-Images heruntergeladen und die Container erstellt, konfiguriert und gestartet. Dieser Vorgang kann einige Minuten in anspruch nehmen. Sobald die Container laufen, werden sie in Docker Desktop grün dargestellt werden.

![grafik](https://github.com/schreinerbayern/rpa-llm4bits/assets/52781604/c798f5ef-bdc6-4477-80f0-ac4f039ca97c)


### Modelle herunterladen
Als nächstes müssen Modelle in **ollama** heruntergeladen werden.
Welche Modelle verfügbar sind ist auf der Webseite (https://ollama.com/library) ersichtlich.
```sh
# Kommando um ein Modell in ollama herunterzuladen
# MODEL_NAME mit Namen aus der ollama-Library ersetzen
docker exec -it ollama sh -c "ollama pull MODEL_NAME"

# z.B. Herunterladen von Llama 3 - leistungsstarke LLM von Meta (empfohlen)
docker exec -it ollama sh -c "ollama pull llama3"

# z.B. Herunterladen von nomic-embed-text - Modell zum Erstellen von Embeddings (empfohlen)
docker exec -it ollama sh -c "ollama pull nomic-embed-text"
```

### n8n Admin-Account einrichten
Beim ersten Aufruf der Web-UI von **n8n** über  [http://localhost](http://localhost) wird man aufgefordert einen Account zu erstellen.

![grafik](https://github.com/schreinerbayern/rpa-llm4bits/assets/52781604/5bfdc3bd-86e7-42a2-ac2e-4085580afa27)



### ollama mit n8n verknüpfen
Nachdem ein Admin-Account eingerichtet wurde, erreicht man die **n8n** Konsole. In der Linken Menüleiste ist ein Schlüssel-Symbol zu finden. Hier kann die Verbindung zu **ollama** hinterlegt werden.
1. Klich auf "Add credentials"
2. "Ollama" suchen und "continue" anklicken
3. `http://ollama:11434` als `Base URL` eintragen
4. "Save" anklicken
5. Hinweis erscheint: "Connection tested successfully"

Die  Einrichtung ist somit abgeschlossen und es können KI-Workflows gebaut werden.

## Bedienung
### n8n Web-UI
Nach dem Start des Clusters ist die Web-UI von **n8n** über folgende URL erreichbar.

**URL:** http://localhost

### Cluster starten
Nachdem die Einrichtung des Clusters durchgeführt wurde, kann das Cluster jederzeit wieder gestartet werden.
#### Über Kommandozeile
```sh
# Cluster starten
docker-compose up --remove-orphans -d
```

### Cluster herunterfahren
#### Über Kommandozeile
```sh
# Cluster stoppen
docker-compose down
```
#### (Alt.) Über Docker-Desktop
![grafik](https://github.com/schreinerbayern/rpa-llm4bits/assets/52781604/02035e41-abfc-4b5d-a8ba-e22fd12861a5)

