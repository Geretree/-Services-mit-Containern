# Services mit Containern

Dieses Repository dokumentiert die Einrichtung und Verwaltung von Services mit Docker-Containern.

## Inhaltsverzeichnis

- [Über das Projekt](#über-das-projekt)
- [Voraussetzungen](#voraussetzungen)
- [Installation](#installation)
- [Services](#services)
- [Verwendung](#verwendung)
- [Dokumentation](#dokumentation)

## Über das Projekt

Dieses Projekt dient zur Verwaltung und Dokumentation von containerisierten Services mit Docker.

## Voraussetzungen

- Ubuntu/Debian-basiertes System
- Sudo-Rechte
- Internetverbindung

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
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

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

Hier werden zukünftig die containerisierten Services dokumentiert.

_Noch keine Services konfiguriert._

## Verwendung

Detaillierte Anleitungen zur Verwendung der Services folgen nach der Konfiguration.

## Dokumentation

Weitere Dokumentation finden Sie im [`docs/`](./docs/) Verzeichnis:

- [Installation Details](./docs/INSTALLATION.md)
- [Services Übersicht](./docs/SERVICES.md)
- [Changelog](./docs/CHANGELOG.md)
