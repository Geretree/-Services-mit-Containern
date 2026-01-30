## Docker Desktop Anmeldung und Credential Management

Nach der Installation von Docker Desktop können Sie sich anmelden und die Credential-Verwaltung konfigurieren.

### Anmeldung bei Docker Desktop

Sie können sich auf verschiedene Arten anmelden:

1. **Über die Docker Desktop GUI**
   - Docker Desktop öffnen
   - Auf "Sign in" klicken
   - Mit Docker Hub Account anmelden

2. **Über die Kommandozeile**
   ```bash
   docker login
   ```

### Credentials Management für Linux

Docker Desktop für Linux unterstützt verschiedene Credential Helpers zur sicheren Speicherung Ihrer Anmeldedaten.

**Verfügbare Credential Helpers:**
- `pass` - Standard Linux Password Manager
- `secretservice` - GNOME Keyring oder KDE Wallet
- Systemspezifische Keychains

**Konfiguration:**

Die Credential-Verwaltung wird in der Docker-Konfigurationsdatei eingerichtet:

```bash
# Docker config bearbeiten
nano ~/.docker/config.json
```

Weitere Details finden Sie in der [offiziellen Docker Dokumentation](https://docs.docker.com/desktop/setup/sign-in/#credentials-management-for-linux-users).

### Vorteile der Anmeldung

- Zugriff auf private Repositories
- Höhere Pull-Rate Limits
- Zugriff auf Docker Hub Features
- Synchronisation von Einstellungen

