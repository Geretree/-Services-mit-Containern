# Services mit Containern

Dieses Repository dokumentiert die Einrichtung und Verwaltung von Services mit Docker-Containern.

## Inhaltsverzeichnis

- [Über das Projekt](#über-das-projekt)
- [Grundlagen](#grundlagen)
  - [Was sind Container?](#was-sind-container)
  - [Was ist DevOps?](#was-ist-devops)
  - [Virtualisierung vs. Containerisierung](#virtualisierung-vs-containerisierung)
  - [Image vs. Container](#image-vs-container)
- [Voraussetzungen](#voraussetzungen)
- [Installation](#installation)
- [Services](#services)
  - [Hello-World Service](#hello-world-service)
  - [To-Do App v1](#to-do-app-v1)
  - [To-Do App v2 mit Redis](#to-do-app-v2-mit-redis)
  - [ONLYOFFICE Document Server](#onlyoffice-document-server)
- [Docker Befehlsreferenz](#docker-befehlsreferenz)
- [Verwendung](#verwendung)
- [Dokumentation](#dokumentation)

## Über das Projekt

Dieses Projekt dient zur Verwaltung und Dokumentation von containerisierten Services mit Docker.

## Grundlagen

### Was sind Container?

Container sind eine leichtgewichtige Form der Virtualisierung, die es ermöglicht, Anwendungen zusammen mit allen ihren Abhängigkeiten in isolierten Umgebungen zu betreiben. Im Gegensatz zu traditionellen virtuellen Maschinen teilen sich Container den Kernel des Host-Betriebssystems, wodurch sie deutlich ressourcenschonender und schneller starten.

Container verpacken eine Anwendung mit allen benötigten Komponenten wie Bibliotheken, Konfigurationsdateien und Abhängigkeiten in eine standardisierte Einheit. Dies garantiert, dass die Anwendung in jeder Umgebung – sei es auf dem Entwicklungsrechner, im Test oder in der Produktion – konsistent läuft. Das löst das klassische "But it works on my machine"-Problem der Softwareentwicklung.

Container sind besonders nützlich in folgenden Szenarien:
- **Microservices-Architekturen**: Verschiedene Services können unabhängig voneinander entwickelt, deployt und skaliert werden
- **Kontinuierliche Integration/Deployment (CI/CD)**: Schnelle und zuverlässige Build- und Deployment-Pipelines
- **Entwicklungsumgebungen**: Konsistente Entwicklungsumgebungen für alle Teammitglieder ohne aufwendige lokale Konfiguration
- **Lastverteilung und Skalierung**: Einfaches horizontales Skalieren durch schnelles Starten mehrerer Container-Instanzen
- **Isolierung von Anwendungen**: Mehrere Anwendungen mit unterschiedlichen Abhängigkeiten können auf demselben Host laufen, ohne sich gegenseitig zu beeinflussen

### Was ist DevOps?

DevOps ist eine Kombination aus kulturellen Philosophien, Praktiken und Tools, die die Zusammenarbeit zwischen Softwareentwicklung (Development) und IT-Betrieb (Operations) verbessert. Das Hauptziel ist es, den Software-Entwicklungszyklus zu verkürzen und qualitativ hochwertige Software kontinuierlich bereitzustellen.

Traditionell arbeiteten Entwicklungs- und Operations-Teams in Silos, was oft zu Kommunikationsproblemen, längeren Deployment-Zeiten und Konflikten führte. DevOps bricht diese Silos auf und fördert eine Kultur der gemeinsamen Verantwortung über den gesamten Software-Lebenszyklus hinweg – von der Entwicklung über das Testen bis zum Deployment und Betrieb.

Kernprinzipien von DevOps umfassen:
- **Automatisierung**: Wiederholbare Prozesse wie Testing, Building und Deployment werden automatisiert
- **Kontinuierliche Integration und Deployment (CI/CD)**: Code-Änderungen werden regelmäßig integriert und automatisch getestet
- **Infrastructure as Code (IaC)**: Infrastruktur wird durch Code definiert und versioniert
- **Monitoring und Logging**: Kontinuierliche Überwachung der Systeme zur frühzeitigen Fehlererkennung
- **Feedback-Schleifen**: Schnelle Rückmeldungen aus dem Betrieb fließen zurück in die Entwicklung

Container-Technologien wie Docker sind ein wesentlicher Bestandteil moderner DevOps-Praktiken, da sie Konsistenz über verschiedene Umgebungen hinweg garantieren und Deployment-Prozesse erheblich vereinfachen.

### Virtualisierung vs. Containerisierung

Beide Technologien dienen der Isolation und effizienten Ressourcennutzung, unterscheiden sich jedoch grundlegend in ihrer Architektur:

#### Virtualisierung

Bei der Virtualisierung wird auf einem physischen Server ein Hypervisor installiert, der mehrere komplett isolierte virtuelle Maschinen (VMs) betreibt. Jede VM enthält:
- Ein komplettes Gast-Betriebssystem
- Virtuelle Hardware (CPU, RAM, Festplatte)
- Die Anwendung und ihre Abhängigkeiten

**Vorteile:**
- Vollständige Isolation zwischen VMs
- Verschiedene Betriebssysteme auf demselben Host
- Etablierte Technologie mit ausgereiften Management-Tools

**Nachteile:**
- Hoher Ressourcenverbrauch (jede VM benötigt ein komplettes OS)
- Längere Startzeiten (Minuten)
- Größerer Speicherbedarf (GB pro VM)

#### Containerisierung

Container nutzen dagegen den Kernel des Host-Betriebssystems und isolieren nur die Anwendungsebene. Jeder Container enthält:
- Nur die Anwendung und ihre spezifischen Abhängigkeiten
- Keine eigene OS-Kopie

**Vorteile:**
- Minimal-ressourcenschonend (MB statt GB)
- Sehr schnelle Startzeiten (Sekunden)
- Höhere Dichte: Mehr Container als VMs auf derselben Hardware
- Portabilität: "Build once, run anywhere"

**Nachteile:**
- Alle Container teilen sich den Host-Kernel
- Etwas schwächere Isolation als VMs
- Gleiche OS-Familie erforderlich (Linux-Container auf Linux-Host)

**Fazit:** Virtualisierung bietet stärkere Isolation und ist ideal für das Betreiben unterschiedlicher Betriebssysteme. Containerisierung ist effizienter, schneller und ideal für Microservices und Cloud-native Anwendungen. Oft werden beide Technologien kombiniert: Container laufen in VMs für zusätzliche Sicherheit.

### Image vs. Container

Diese beiden Begriffe werden oft verwechselt, beschreiben aber unterschiedliche Konzepte:

#### Docker Image

Ein Image ist eine **unveränderliche (immutable) Vorlage** oder Blaupause, die alles enthält, was zum Ausführen einer Anwendung benötigt wird:
- Betriebssystem-Basis (z.B. Alpine Linux, Ubuntu)
- Anwendungscode
- Laufzeitumgebung (z.B. Python, Node.js)
- Bibliotheken und Abhängigkeiten
- Konfigurationsdateien
- Umgebungsvariablen

Images werden in Schichten (Layers) aufgebaut und sind read-only. Sie dienen als Bauplan und können aus einem Dockerfile erstellt werden.

**Beispiel:**
```bash
docker build -t meine-app:v1 .    # Erstellt ein Image
docker images                      # Zeigt alle Images
```

#### Docker Container

Ein Container ist eine **laufende Instanz** eines Images – quasi das Image in Aktion. Wenn ein Image gestartet wird, entsteht ein Container:
- Container sind beschreibbar (writeable layer on top)
- Mehrere Container können vom selben Image erstellt werden
- Jeder Container läuft isoliert mit eigenen Prozessen, Netzwerk und Dateisystem
- Container können gestartet, gestoppt, gelöscht werden

**Beispiel:**
```bash
docker run -d meine-app:v1        # Startet einen Container aus dem Image
docker ps                          # Zeigt laufende Container
```

**Analogie:** Ein Image ist wie ein **Rezept** (Anleitung), ein Container ist das **fertige Gericht** (das Ergebnis). Aus einem Rezept können viele Gerichte gekocht werden, aber jedes Gericht ist eine eigenständige Instanz.

**Workflow:**
1. **Dockerfile** schreiben → Beschreibt wie das Image gebaut wird
2. **Image** bauen → `docker build`
3. **Container** starten → `docker run`
4. **Container** verwalten → `docker stop`, `docker start`, `docker rm`

## Voraussetzungen

- Ubuntu/Debian-basiertes System
- Sudo-Rechte
- Internetverbindung
- Docker Desktop installiert

## Installation

### Docker Installation

Die folgenden Schritte wurden bereits auf dem System ausgeführt:

#### 1. Alte Docker-Versionen entfernen

```bash
# Zuerst alles entfernen
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt remove docker-desktop

rm -r $HOME/.docker/desktop
sudo rm /usr/local/bin/com.docker.cli
sudo apt purge docker-desktop
```

#### 2. Zertifikatsschlüssel per SSH zulassen

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

#### 3. PGP Key von Docker hinzufügen

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

#### 4. Docker Repository hinzufügen

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list [...]

sudo apt update -y
```

#### 5. Docker Desktop installieren

```bash
sudo apt update
cd Downloads
sudo apt install ./docker-desktop-amd64.deb
```

**Hinweis:** Es können Fehlermeldungen auftreten, wenn noch kein Docker installiert war. Diese können ignoriert werden.

## Services

### Hello-World Service

Ein einfacher Test-Service zum Überprüfen der Docker-Installation.

**Quelle:** [cloudmodule/hello-world](https://git.gibb.ch/thomas.staub/cloudmodule/-/tree/main/hello-world)

#### Build und Ausführung

```bash
# Docker Image erstellen
docker build -t test:latest .

# Container starten
docker run -p 8000:8000 test:latest
```

Der Service ist dann unter `http://localhost:8000` erreichbar.

#### Beenden des Containers

```bash
# Laufende Container anzeigen
docker ps

# Container stoppen (ersetze <container-id> mit der tatsächlichen ID)
docker stop <container-id>
```

---

### To-Do App v1

Eine einfache To-Do Listen Anwendung basierend auf Alpine Linux.

**Quelle:** [cloudmodule/to-do-appv1](https://git.gibb.ch/thomas.staub/cloudmodule/-/tree/main/to-do-appv1)

#### Dockerfile

```dockerfile
FROM alpine:3.16.2
MAINTAINER Johannes M. Scheuermann <johannes.scheuermann@inovex.de>

COPY ./bin/todo-app /app/todo-app
COPY ./public /app/public
RUN chmod +x /app/todo-app
WORKDIR /app
CMD ["./todo-app"]
EXPOSE 3000
```

#### Struktur

Das Projekt benötigt folgende Verzeichnisstruktur:

```
to-do-appv1/
├── Dockerfile
├── bin/
│   └── todo-app          # Ausführbare Datei
└── public/               # Statische Dateien (HTML, CSS, JS)
```

#### Build und Ausführung

```bash
# Docker Image erstellen
docker image build -t todo-app:v1 .

# Container im Hintergrund starten mit Namen "frontend"
docker run --name frontend -d -p 3000:3000 todo-app:v1
```

**Parameter-Erklärung:**
- `--name frontend`: Gibt dem Container einen spezifischen Namen für einfachere Verwaltung
- `-d`: Detached mode – Container läuft im Hintergrund
- `-p 3000:3000`: Port-Mapping (Host-Port:Container-Port)
- `todo-app:v1`: Das zu verwendende Image mit Tag

Die Anwendung ist dann unter `http://localhost:3000` erreichbar.

#### Verwaltung

```bash
# Container-Status prüfen
docker ps | grep frontend

# Logs ansehen
docker logs frontend
docker logs -f frontend          # Logs in Echtzeit folgen

# Container stoppen
docker stop frontend

# Container starten
docker start frontend

# Container neu starten
docker restart frontend

# Container entfernen (muss zuerst gestoppt werden)
docker stop frontend
docker rm frontend

# Container zwangsweise entfernen (auch wenn er läuft)
docker rm -f frontend

# Image entfernen
docker rmi todo-app:v1
```

#### Alternative Startoptionen

```bash
# Ohne Namen (Docker vergibt zufälligen Namen)
docker run -d -p 3000:3000 todo-app:v1

# Mit automatischem Entfernen nach dem Stoppen
docker run --name frontend --rm -d -p 3000:3000 todo-app:v1

# Interaktiv mit Log-Ausgabe (nicht im Hintergrund)
docker run --name frontend -p 3000:3000 todo-app:v1

# Mit Umgebungsvariablen
docker run --name frontend -d -p 3000:3000 -e NODE_ENV=production todo-app:v1

# Mit Volume für persistente Daten
docker run --name frontend -d -p 3000:3000 -v /host/data:/app/data todo-app:v1
```

---

### To-Do App v2 mit Redis

Eine erweiterte To-Do Listen Anwendung mit Redis-Backend in Master-Slave Architektur für persistente Datenspeicherung und höhere Verfügbarkeit.

<img width="2089" height="465" alt="image" src="https://github.com/user-attachments/assets/287e8a41-31f3-49ee-8f4e-13c27a399204" />


#### Architektur-Übersicht

Diese Version besteht aus drei Komponenten:
- **Frontend**: Web-Interface für die To-Do-Verwaltung (Port 3000)
- **Redis Master**: Primäre Datenbank für Schreiboperationen (Port 6379)
- **Redis Slave**: Sekundäre Datenbank für Leseoperationen und Redundanz (Port 6380)

**Vorteile der Master-Slave Architektur:**
- **Persistenz**: Daten bleiben auch nach Container-Neustart erhalten
- **Hochverfügbarkeit**: Bei Ausfall des Masters kann Slave übernehmen
- **Lastverteilung**: Lesezugriffe können auf Slave verteilt werden
- **Backup**: Slave dient als Live-Backup des Masters

#### Build der Images

```bash
# Redis Master Image erstellen
docker build -t redis-master:v1 .

# Redis Slave Image erstellen
docker build -t redis-slave:v1 .

# Frontend Image erstellen
docker build -t todo-app:v2 .
```

#### Docker Network erstellen

Für die Kommunikation zwischen den Containern wird ein gemeinsames Netzwerk benötigt:

```bash
# Eigenes Netzwerk erstellen
docker network create todo-network

# Netzwerk überprüfen
docker network ls
docker network inspect todo-network
```

#### Container starten

**Wichtig:** Die Container müssen in der richtigen Reihenfolge gestartet werden!

```bash
# 1. Redis Master starten
docker run -d \
  --name redis-master \
  --network todo-network \
  -p 6379:6379 \
  redis-master:v1

# 2. Redis Slave starten (verbindet sich mit Master)
docker run -d \
  --name redis-slave \
  --network todo-network \
  -p 6380:6379 \
  redis-slave:v1

# 3. Frontend starten (nutzt Redis Master)
docker run -d \
  --name frontend \
  --network todo-network \
  -p 3000:3000 \
  -e REDIS_HOST=redis-master \
  -e REDIS_PORT=6379 \
  todo-app:v2
```

**Parameter-Erklärung:**
- `--network todo-network`: Verbindet Container mit dem erstellten Netzwerk
- `-p 6379:6379`: Port-Mapping für Redis Master
- `-p 6380:6379`: Slave läuft auf Host-Port 6380, intern auf 6379
- `-e REDIS_HOST=redis-master`: Umgebungsvariable für Redis-Verbindung
- `-e REDIS_PORT=6379`: Redis-Port als Umgebungsvariable

#### Zugriff

Nach dem Start sind folgende Services erreichbar:
- **To-Do App**: `http://localhost:3000`
- **Redis Master**: `localhost:6379`
- **Redis Slave**: `localhost:6380`

#### Funktionalität testen

```bash
# To-Do hinzufügen über die Web-UI: http://localhost:3000

# Daten im Redis Master prüfen
docker exec -it redis-master redis-cli
> KEYS *
> GET todo:1
> exit

# Replikation im Slave prüfen
docker exec -it redis-slave redis-cli
> KEYS *
> GET todo:1
> INFO replication
> exit
```

#### Verwaltung

```bash
# Status aller Container prüfen
docker ps --filter "network=todo-network"

# Logs der einzelnen Services
docker logs -f frontend
docker logs -f redis-master
docker logs -f redis-slave

# Alle Services stoppen
docker stop frontend redis-slave redis-master

# Alle Services starten
docker start redis-master redis-slave frontend

# Alle Services neu starten
docker restart redis-master redis-slave frontend

# Einzelnen Service neu starten
docker restart frontend
```

#### Daten-Persistenz

Um Daten auch nach Container-Neustart zu behalten, können Volumes verwendet werden:

```bash
# Volume für Redis Master erstellen
docker volume create redis-master-data

# Redis Master mit Volume starten
docker run -d \
  --name redis-master \
  --network todo-network \
  -p 6379:6379 \
  -v redis-master-data:/data \
  redis-master:v1

# Volume inspizieren
docker volume inspect redis-master-data
```

#### Troubleshooting

**Problem: Slave kann nicht mit Master verbinden**
```bash
# Netzwerk-Konnektivität prüfen
docker exec redis-slave ping redis-master

# Master-Logs prüfen
docker logs redis-master

# Slave-Logs prüfen
docker logs redis-slave

# Replikationsstatus prüfen
docker exec -it redis-master redis-cli INFO replication
```

**Problem: Frontend kann Redis nicht erreichen**
```bash
# Umgebungsvariablen prüfen
docker inspect frontend | grep -A 10 Env

# Redis-Verbindung vom Frontend testen
docker exec -it frontend ping redis-master

# Frontend-Logs prüfen
docker logs -f frontend
```

**Problem: Daten gehen verloren nach Neustart**
```bash
# Volumes prüfen
docker volume ls

# Container mit Volume neu erstellen (siehe Daten-Persistenz Sektion)
```

#### Aufräumen

```bash
# Alle Container stoppen und entfernen
docker stop frontend redis-slave redis-master
docker rm frontend redis-slave redis-master

# Images entfernen
docker rmi todo-app:v2 redis-slave:v1 redis-master:v1

# Netzwerk entfernen
docker network rm todo-network

# Volumes entfernen (ACHTUNG: Löscht alle Daten!)
docker volume rm redis-master-data
```

#### Docker Compose Alternative

Für einfacheres Management kann auch Docker Compose verwendet werden:

```yaml
version: '3.8'

services:
  redis-master:
    image: redis-master:v1
    container_name: redis-master
    ports:
      - "6379:6379"
    networks:
      - todo-network
    volumes:
      - redis-master-data:/data

  redis-slave:
    image: redis-slave:v1
    container_name: redis-slave
    ports:
      - "6380:6379"
    networks:
      - todo-network
    depends_on:
      - redis-master

  frontend:
    image: todo-app:v2
    container_name: frontend
    ports:
      - "3000:3000"
    environment:
      - REDIS_HOST=redis-master
      - REDIS_PORT=6379
    networks:
      - todo-network
    depends_on:
      - redis-master

networks:
  todo-network:
    driver: bridge

volumes:
  redis-master-data:
```

**Verwendung mit Docker Compose:**
```bash
# Alle Services starten
docker-compose up -d

# Logs ansehen
docker-compose logs -f

# Services stoppen
docker-compose down

# Services stoppen und Volumes löschen
docker-compose down -v
```

---

### ONLYOFFICE Document Server

ONLYOFFICE ist eine vollwertige Office-Suite für kollaboratives Arbeiten mit Dokumenten, Tabellen und Präsentationen direkt im Browser.

**Offizielle Dokumentation:** [ONLYOFFICE Docker](https://github.com/ONLYOFFICE/Docker-DocumentServer)

<img width="2115" height="1247" alt="Screenshot 2026-02-06 085105" src="https://github.com/user-attachments/assets/e2c456ae-921d-4aa1-9cf4-21001ce47258" />


#### Features

- **Dokumentenbearbeitung**: Textverarbeitung, Tabellenkalkulation, Präsentationen
- **Echtzeit-Kollaboration**: Mehrere Benutzer können gleichzeitig an Dokumenten arbeiten
- **Kompatibilität**: Unterstützt gängige Formate (DOCX, XLSX, PPTX, ODT, PDF, etc.)
- **Web-basiert**: Komplett im Browser nutzbar, keine Desktop-Software notwendig
- **Integration**: Kann mit Nextcloud, ownCloud, Seafile und anderen Plattformen integriert werden

#### Installation und Ausführung

```bash
# ONLYOFFICE Document Server Image herunterladen und starten
docker run -d \
  --name onlyoffice \
  -p 8000:80 \
  -p 8443:443 \
  -e JWT_ENABLED=false \
  -v /app/onlyoffice/DocumentServer/logs:/var/log/onlyoffice \
  -v /app/onlyoffice/DocumentServer/data:/var/www/onlyoffice/Data \
  -v /app/onlyoffice/DocumentServer/lib:/var/lib/onlyoffice \
  onlyoffice/documentserver
```

**Parameter-Erklärung:**
- `-d`: Startet Container im Hintergrund (detached mode)
- `--name onlyoffice`: Gibt dem Container den Namen "onlyoffice"
- `-p 8000:80`: HTTP-Port-Mapping (Host:Container)
- `-p 8443:443`: HTTPS-Port-Mapping
- `-e JWT_ENABLED=false`: Deaktiviert JWT-Authentifizierung für Tests (für Produktion aktivieren!)
- `-v`: Volume-Mappings für persistente Daten (Logs, Daten, Bibliotheken)

#### Zugriff

Nach dem Start ist ONLYOFFICE erreichbar unter:
- **HTTP**: `http://localhost:8000` oder `http://192.168.110.30:11012/example/editor`
- **HTTPS**: `https://localhost:8443`

#### Erste Schritte

1. Browser öffnen und zu `http://localhost:8000` navigieren
2. Willkommensseite wird angezeigt
3. Beispiel-Editor testen: `http://localhost:8000/example/editor`
4. Neue Dokumente erstellen oder bestehende hochladen

#### Verwaltung

```bash
# Container-Status prüfen
docker ps | grep onlyoffice

# Logs ansehen
docker logs -f onlyoffice

# Container stoppen
docker stop onlyoffice

# Container starten
docker start onlyoffice

# Container neu starten
docker restart onlyoffice

# In Container einsteigen (für Debugging)
docker exec -it onlyoffice /bin/bash

# Container und Volumes entfernen
docker stop onlyoffice
docker rm onlyoffice
# Volumes bleiben erhalten unter /app/onlyoffice/
```

#### Persistente Daten

Die wichtigen Daten werden in folgenden Verzeichnissen gespeichert:
- **Logs**: `/app/onlyoffice/DocumentServer/logs`
- **Daten**: `/app/onlyoffice/DocumentServer/data`
- **Bibliotheken**: `/app/onlyoffice/DocumentServer/lib`

Diese Verzeichnisse bleiben auch nach dem Löschen des Containers erhalten.

#### Sicherheitshinweise für Produktion

Für den produktiven Einsatz sollten folgende Anpassungen vorgenommen werden:

```bash
# JWT-Token aktivieren für sichere API-Kommunikation
docker run -d \
  --name onlyoffice \
  -p 8000:80 \
  -p 8443:443 \
  -e JWT_ENABLED=true \
  -e JWT_SECRET=IHR_SICHERES_GEHEIMNIS \
  -v /app/onlyoffice/DocumentServer/logs:/var/log/onlyoffice \
  -v /app/onlyoffice/DocumentServer/data:/var/www/onlyoffice/Data \
  -v /app/onlyoffice/DocumentServer/lib:/var/lib/onlyoffice \
  onlyoffice/documentserver
```

Zusätzlich empfohlen:
- **HTTPS verwenden**: SSL-Zertifikat einbinden
- **Reverse Proxy**: Nginx oder Traefik vorschalten
- **Firewall**: Nur notwendige Ports freigeben
- **Backup**: Regelmäßige Sicherung der Volume-Daten
- **Updates**: Container regelmäßig aktualisieren

#### Troubleshooting

**Problem: Container startet nicht**
```bash
# Logs prüfen
docker logs onlyoffice

# Port-Konflikte prüfen
sudo netstat -tulpn | grep -E '8000|8443'
```

**Problem: Dokumente werden nicht gespeichert**
```bash
# Volume-Berechtigungen prüfen
ls -la /app/onlyoffice/DocumentServer/

# Falls nötig, Berechtigungen anpassen
sudo chown -R 104:107 /app/onlyoffice/DocumentServer/
```

**Problem: Langsame Performance**
```bash
# Ressourcen-Limits erhöhen
docker update --memory 2g --memory-swap 2g onlyoffice

# Oder beim Start festlegen
docker run -d --name onlyoffice --memory 2g --memory-swap 2g ...
```

## Docker Befehlsreferenz

Diese Übersicht enthält die wichtigsten Docker-Befehle mit ihrer Funktion. Sie wird laufend ergänzt.

### Image-Verwaltung

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker build` | Erstellt ein Image aus einem Dockerfile | `docker build -t meine-app:v1 .` |
| `docker images` | Listet alle lokalen Images auf | `docker images` |
| `docker image ls` | Alternative zu `docker images` | `docker image ls` |
| `docker rmi <image>` | Löscht ein Image | `docker rmi meine-app:v1` |
| `docker image rm <image>` | Alternative zu `docker rmi` | `docker image rm meine-app:v1` |
| `docker pull <image>` | Lädt ein Image aus einer Registry (z.B. Docker Hub) | `docker pull nginx:latest` |
| `docker push <image>` | Lädt ein Image in eine Registry hoch | `docker push user/meine-app:v1` |
| `docker tag <source> <target>` | Erstellt einen neuen Tag für ein Image | `docker tag meine-app:v1 meine-app:latest` |
| `docker image prune` | Entfernt ungenutzte Images | `docker image prune -a` |
| `docker history <image>` | Zeigt die Layer-Historie eines Images | `docker history nginx` |

### Container-Verwaltung

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker run` | Erstellt und startet einen neuen Container | `docker run -d -p 8080:80 nginx` |
| `docker run -d` | Startet Container im Hintergrund (detached) | `docker run -d nginx` |
| `docker run -it` | Startet Container interaktiv mit Terminal | `docker run -it ubuntu /bin/bash` |
| `docker run --name <name>` | Gibt dem Container einen Namen | `docker run --name web-server nginx` |
| `docker run -p <host>:<container>` | Mapped Ports vom Host zum Container | `docker run -p 8080:80 nginx` |
| `docker run -v <host>:<container>` | Bindet ein Volume ein | `docker run -v /data:/app/data nginx` |
| `docker run --rm` | Entfernt Container automatisch nach dem Stoppen | `docker run --rm nginx` |
| `docker ps` | Zeigt laufende Container | `docker ps` |
| `docker ps -a` | Zeigt alle Container (auch gestoppte) | `docker ps -a` |
| `docker start <container>` | Startet einen gestoppten Container | `docker start mein-container` |
| `docker stop <container>` | Stoppt einen laufenden Container (graceful) | `docker stop mein-container` |
| `docker kill <container>` | Beendet einen Container sofort (forceful) | `docker kill mein-container` |
| `docker restart <container>` | Startet einen Container neu | `docker restart mein-container` |
| `docker rm <container>` | Löscht einen Container | `docker rm mein-container` |
| `docker rm -f <container>` | Löscht einen laufenden Container zwangsweise | `docker rm -f mein-container` |
| `docker container prune` | Entfernt alle gestoppten Container | `docker container prune` |

### Container-Informationen & Debugging

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker logs <container>` | Zeigt die Logs eines Containers | `docker logs mein-container` |
| `docker logs -f <container>` | Folgt den Logs in Echtzeit (follow) | `docker logs -f mein-container` |
| `docker logs --tail <n>` | Zeigt die letzten n Zeilen der Logs | `docker logs --tail 50 mein-container` |
| `docker exec <container> <command>` | Führt einen Befehl im laufenden Container aus | `docker exec mein-container ls /app` |
| `docker exec -it <container> <shell>` | Öffnet eine interaktive Shell im Container | `docker exec -it mein-container /bin/bash` |
| `docker inspect <container>` | Zeigt detaillierte Informationen zum Container | `docker inspect mein-container` |
| `docker stats` | Zeigt Ressourcennutzung aller Container in Echtzeit | `docker stats` |
| `docker stats <container>` | Zeigt Ressourcennutzung eines spezifischen Containers | `docker stats mein-container` |
| `docker top <container>` | Zeigt laufende Prozesse im Container | `docker top mein-container` |
| `docker port <container>` | Zeigt Port-Mappings eines Containers | `docker port mein-container` |

### Netzwerk-Verwaltung

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker network ls` | Listet alle Netzwerke auf | `docker network ls` |
| `docker network create <name>` | Erstellt ein neues Netzwerk | `docker network create mein-netzwerk` |
| `docker network connect <network> <container>` | Verbindet Container mit Netzwerk | `docker network connect mein-netzwerk web` |
| `docker network disconnect <network> <container>` | Trennt Container von Netzwerk | `docker network disconnect mein-netzwerk web` |
| `docker network inspect <network>` | Zeigt Details zu einem Netzwerk | `docker network inspect bridge` |
| `docker network rm <network>` | Löscht ein Netzwerk | `docker network rm mein-netzwerk` |

### Volume-Verwaltung

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker volume ls` | Listet alle Volumes auf | `docker volume ls` |
| `docker volume create <name>` | Erstellt ein neues Volume | `docker volume create mein-volume` |
| `docker volume inspect <volume>` | Zeigt Details zu einem Volume | `docker volume inspect mein-volume` |
| `docker volume rm <volume>` | Löscht ein Volume | `docker volume rm mein-volume` |
| `docker volume prune` | Entfernt ungenutzte Volumes | `docker volume prune` |

### System-Befehle

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker version` | Zeigt Docker-Version (Client & Server) | `docker version` |
| `docker info` | Zeigt System-weite Informationen | `docker info` |
| `docker system df` | Zeigt Speichernutzung von Docker | `docker system df` |
| `docker system prune` | Entfernt ungenutzte Daten (Container, Networks, Images) | `docker system prune` |
| `docker system prune -a` | Entfernt ALLE ungenutzten Images (nicht nur dangling) | `docker system prune -a` |
| `docker system prune --volumes` | Schließt auch Volumes in die Bereinigung ein | `docker system prune --volumes` |

### Docker Compose (wenn installiert)

| Befehl | Funktion | Beispiel |
|--------|----------|----------|
| `docker-compose up` | Startet alle Services aus docker-compose.yml | `docker-compose up` |
| `docker-compose up -d` | Startet Services im Hintergrund | `docker-compose up -d` |
| `docker-compose down` | Stoppt und entfernt alle Services | `docker-compose down` |
| `docker-compose ps` | Zeigt laufende Compose-Services | `docker-compose ps` |
| `docker-compose logs` | Zeigt Logs aller Services | `docker-compose logs -f` |
| `docker-compose build` | Baut alle Images neu | `docker-compose build` |
| `docker-compose restart` | Startet Services neu | `docker-compose restart` |

### Häufig verwendete Kombinationen

```bash
# Container im Hintergrund mit Name und Port-Mapping starten
docker run -d --name mein-web -p 8080:80 nginx

# In laufenden Container einsteigen (Alpine Linux)
docker exec -it mein-container /bin/sh

# In laufenden Container einsteigen (Ubuntu/Debian)
docker exec -it mein-container /bin/bash

# Container-Logs in Echtzeit folgen
docker logs -f --tail 100 mein-container

# Alle gestoppten Container und ungenutzten Images entfernen
docker container prune && docker image prune

# Komplette Reinigung (VORSICHT: Löscht alle ungenutzten Ressourcen!)
docker system prune -a --volumes
```

## Verwendung

### Docker Grundbefehle

```bash
# Images anzeigen
docker images

# Laufende Container anzeigen
docker ps

# Alle Container anzeigen (auch gestoppte)
docker ps -a

# Container Logs anzeigen
docker logs <container-id>

# Container entfernen
docker rm <container-id>

# Image entfernen
docker rmi <image-name>

# In laufenden Container einsteigen
docker exec -it <container-id> /bin/sh
```

### Nützliche Docker Befehle

```bash
# Alle gestoppten Container entfernen
docker container prune

# Alle unbenutzten Images entfernen
docker image prune

# Alles aufräumen (Container, Images, Networks, Cache)
docker system prune -a
```

## Dokumentation

Weitere Dokumentation finden Sie im [`docs/`](./docs/) Verzeichnis:

- [Installation Details](./docs/INSTALLATION.md)
- [Services Übersicht](./docs/SERVICES.md)
- [Changelog](./docs/CHANGELOG.md)
