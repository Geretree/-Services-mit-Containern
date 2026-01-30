# Changelog

Alle wichtigen Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/).

## [Unreleased]

### Geplant
- Weitere Service-Konfigurationen
- Docker Compose Setup
- Monitoring Integration

## [1.1.0] - 2026-01-30

### Hinzugefügt
- Docker Anmeldung und Credential Management durchgeführt
- Erste praktische Docker-Übungen dokumentiert
- Hello-World Container erfolgreich getestet
- Ubuntu Images in verschiedenen Versionen (latest, 21.10) gepullt
- Nginx Webserver als Service eingerichtet (Port 8080:80)
- Nginx erfolgreich im Browser getestet

### Durchgeführte Docker-Befehle
- `docker pull hello-world` - Erstes Image heruntergeladen
- `docker run hello-world` - Verifizierung der Installation
- `docker pull ubuntu` und `docker pull ubuntu:21.10` - Verschiedene Ubuntu-Versionen
- `docker run -it ubuntu bash` - Interaktive Container-Sessions
- `docker images` - Übersicht aller Images
- `docker ps -a` - Alle Container anzeigen
- `docker pull nginx` - Nginx Webserver Image
- `docker run --name some-nginx -d --rm -p 8080:80 nginx` - Nginx Container starten
- `docker stop` und `docker rm` - Container-Management

### Getestet
- ✅ Docker Installation funktioniert korrekt
- ✅ Image Pull von Docker Hub erfolgreich
- ✅ Container können erstellt und gestartet werden
- ✅ Port-Mapping funktioniert (8080:80)
- ✅ Nginx Webserver läuft erfolgreich
- ✅ "Welcome to nginx!" Seite im Browser erreichbar

## [1.0.0] - 2026-01-30

### Hinzugefügt
- Initiale Projekt-Dokumentation
- README.md mit Übersicht und Installationsanleitung
- Docker Installation komplett dokumentiert
- INSTALLATION.md mit detaillierten Schritten
- SERVICES.md Template für Service-Dokumentation
- GitHub Actions Workflow für automatische Dokumentationsaktualisierung
- Docker Deinstallation und Neuinstallation durchgeführt
- Docker Repository und GPG Keys konfiguriert
- Docker Desktop installiert

### Durchgeführte Schritte
- Alte Docker-Versionen entfernt
- Zertifikate und Abhängigkeiten installiert (ca-certificates, curl, gnupg, lsb-release)
- Docker PGP Key hinzugefügt
- Docker Repository zur APT-Quellen-Liste hinzugefügt
- Docker Desktop Installation abgeschlossen

---

## Changelog-Kategorien

- **Hinzugefügt** für neue Features
- **Geändert** für Änderungen an bestehender Funktionalität
- **Veraltet** für Features, die bald entfernt werden
- **Entfernt** für entfernte Features
- **Behoben** für Bugfixes
- **Sicherheit** für Sicherheitsrelevante Änderungen