# Services Dokumentation

## Übersicht

Hier werden alle containerisierten Services dokumentiert, die in diesem Projekt verwendet werden.

## Geplante Services

_Noch keine Services konfiguriert. Diese Dokumentation wird automatisch aktualisiert, sobald Services hinzugefügt werden._

## Service-Template

Für jeden neuen Service sollte folgende Struktur verwendet werden:

### Service Name

**Beschreibung:** Kurze Beschreibung des Services

**Image:** `image:tag`

**Ports:**
- `host:container` - Beschreibung

**Volumes:**
- `./local/path:/container/path` - Beschreibung

**Umgebungsvariablen:**
- `VARIABLE_NAME` - Beschreibung

**Abhängigkeiten:**
- Liste anderer Services

**Docker Compose Beispiel:**

```yaml
services:
  service-name:
    image: image:tag
    container_name: service-name
    ports:
      - "8080:80"
    volumes:
      - ./data:/data
    environment:
      - ENV_VAR=value
    restart: unless-stopped
```

**Verwendung:**

```bash
# Service starten
docker compose up -d service-name

# Logs anzeigen
docker compose logs -f service-name

# Service stoppen
docker compose stop service-name
```

## Docker Compose Struktur

Alle Services sollten in einer `docker-compose.yml` Datei im Hauptverzeichnis definiert werden:

```yaml
version: '3.8'

services:
  # Hier kommen die Services  
  
networks:
  # Netzwerk-Konfiguration  
  
volumes:
  # Persistente Volumes
```

## Best Practices

1. **Container Namen:** Verwenden Sie aussagekräftige Namen
2. **Restart Policy:** Verwenden Sie `unless-stopped` für Produktions-Services
3. **Volumes:** Nutzen Sie benannte Volumes für persistente Daten
4. **Netzwerke:** Isolieren Sie Services in eigenen Netzwerken
5. **Umgebungsvariablen:** Verwenden Sie `.env` Dateien für sensitive Daten
6. **Health Checks:** Definieren Sie Health Checks für kritische Services

## Nützliche Befehle

```bash
# Alle Services starten
docker compose up -d

# Alle Services stoppen
docker compose down

# Services neu bauen
docker compose build

# Status aller Services
docker compose ps

# Logs aller Services
docker compose logs -f

# Ressourcen aufräumen
docker system prune -a
```

## Monitoring

_Monitoring-Lösungen werden hier dokumentiert, sobald sie konfiguriert sind._