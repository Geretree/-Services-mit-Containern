# Docker Installation - Detaillierte Anleitung

## Übersicht

Diese Anleitung dokumentiert die vollständige Installation von Docker und Docker Desktop auf einem Ubuntu/Debian-System.

## Schritt-für-Schritt Anleitung

### Schritt 1: System vorbereiten

Zuerst müssen alle alten Docker-Installationen entfernt werden, um Konflikte zu vermeiden.

```bash
# Alte Docker-Versionen deinstallieren
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt remove docker-desktop

# Docker Desktop Dateien entfernen
rm -r $HOME/.docker/desktop
sudo rm /usr/local/bin/com.docker.cli
sudo apt purge docker-desktop
```

### Schritt 2: Abhängigkeiten installieren

```bash
# Zertifikate und Tools installieren
sudo apt install -y ca-certificates curl gnupg lsb-release
```

**Was wird installiert:**
- `ca-certificates`: SSL/TLS Zertifikate für sichere Verbindungen
- `curl`: Tool zum Herunterladen von Dateien
- `gnupg`: Verschlüsselungs- und Signatur-Tool
- `lsb-release`: Informationen über die Linux-Distribution

### Schritt 3: Docker GPG Key hinzufügen

```bash
# Verzeichnis für Schlüssel erstellen
sudo mkdir -p /etc/apt/keyrings

# Docker's offiziellen GPG Key herunterladen
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### Schritt 4: Docker Repository konfigurieren

```bash
# Docker Repository zur APT Quellen-Liste hinzufügen
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Paketliste aktualisieren
sudo apt update -y
```

### Schritt 5: Docker Desktop installieren

```bash
# Zum Downloads-Verzeichnis wechseln
cd Downloads

# System aktualisieren
sudo apt update

# Docker Desktop installieren (muss vorher heruntergeladen worden sein)
sudo apt install ./docker-desktop-amd64.deb
```

## Verifizierung

Nach der Installation können Sie Docker mit folgendem Befehl testen:

```bash
# Docker Version prüfen
docker --version

# Docker Compose Version prüfen
docker compose version

# Test-Container ausführen
docker run hello-world
```

## Häufige Probleme

### Fehlermeldungen beim Entfernen

Wenn beim Entfernen alter Versionen Fehlermeldungen auftreten, ist das normal wenn Docker noch nicht installiert war. Diese können ignoriert werden.

### Berechtigungsprobleme

Falls Sie Docker ohne `sudo` verwenden möchten:

```bash
# Benutzer zur docker Gruppe hinzufügen
sudo usermod -aG docker $USER

# Neu anmelden oder:
newgrp docker
```

## Nächste Schritte

Nach der erfolgreichen Installation können Sie:
- Docker Container erstellen
- Docker Compose verwenden
- Services konfigurieren

Siehe [Services Dokumentation](./SERVICES.md) für weitere Informationen.