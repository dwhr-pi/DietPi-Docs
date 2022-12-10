# Versionshinweise

## Juli 2021 (Version 7.4)

Willkommen zur **Veröffentlichung vom Juli 2021** :octicons-heart-16: von **DietPi**.

### Neue Softwaretitel {: #new-software-74 }

- [**Synapse**](../../software/social/#synapse)

    Synapse ist eine Referenz-Homeserver-Implementierung, die vom Kernteam von Matrix.org in Python/Twisted geschrieben wurde. Es ermöglicht die dezentrale Kommunikation, das Speichern aller persönlichen Benutzerinformationen, den Chatverlauf, das Erstellen des Raums für den eigenen Gebrauch und viele andere Optionen.

    Matrix Synapse ist eine großartige Alternative für Anwendungen wie Slack, Discord, Rocket.chat und andere.

    Jetzt verfügbar zur Installation mit [`dietpi-software`](../../dietpi_tools/#dietpi-software) oder direkt mit der Software-ID `125`.

- [**PostgreSQL**](../../software/databases/#postgresql)

    Ein persistenter erweiterter objektrelationaler Datenbankserver wurde hinzugefügt. Jetzt verfügbar zur Installation mit [`dietpi-software`](../../dietpi_tools/#dietpi-software) oder direkt mit der Software-ID `194`.

- [**youtube-dl**](../../software/bittorrent/#youtube-dl)

    Das berühmte Kommandozeilenprogramm zum Herunterladen von Videos von YouTube und anderen Videoplattformen wurde hinzugefügt.

    Jetzt verfügbar zur Installation mit [`dietpi-software`](../../dietpi_tools/#dietpi-software) oder direkt mit der Software-ID `195`.

### DietPi Tools (neue / bemerkenswerte Updates) {: #dietpi-tools-74 }

- [DietPi-Update](../../dietpi_tools/#dietpi-update) :octicons-arrow-right-16: Ein neues Live-Patching-System wurde implementiert. Dies ermöglicht es uns, kleine Fixes und Updates auszuliefern, die sicher mit einem einzeiligen Befehl angewendet werden können, bis die nächste DietPi-Version veröffentlicht wird. Live-Patches werden zusammen mit DietPi-Updates gesucht und eine Benachrichtigung wird auch im Login-Banner angezeigt, wenn neue Live-Patches gefunden wurden. Wenn verfügbar, kann jeder Patch einzeln angewendet oder verworfen werden und das Login-Banner wird Sie nicht mehr über Patches belästigen, die Sie bereits im dietpi-Update-Menü gesehen haben, unabhängig davon, ob Sie sie angewendet haben oder nicht.
- [DietPi-Globals | `G_AGUP`](../../dietpi_tools/#useful-dietpi-shell-functions) :octicons-arrow-right-16: Unser `apt-get update`-Wrapper wirft jetzt einen Fehler, wenn einige Indexdateien dies könnten nicht heruntergeladen werden, z. B. aufgrund eines DNS-Fehlers. Derzeit gibt `apt-get update` eine Warnung aus, gibt aber keinen Fehlercode zurück. Es ist besser, hier eine Fehlerbehandlungsaufforderung zu haben, wo wir eine zugehörige Befehlsausgabe haben, als später, wenn Paketinstallationen oder Upgrades aufgrund veralteter Informationen oder fehlender Listendateien fehlschlagen.
- **DietPi-Set_swapfile** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das erneute Mounten des `/tmp` tmpfs-Dateisystems fehlschlug, wenn ein anderer Dateisystemtyp unter `/tmp` gemountet wurde. Dies könnte insbesondere während der DietPi-PREP-Image-Erstellung der Fall sein. Vielen Dank an @timocapa für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4573#issuecomment-884993352>

### Debian-Betriebssystem- und Armbian-Betriebssystem-Updates {: #change-74-bullseye }

- **Armbian-basierte Stretch-Systeme** :octicons-arrow-right-16: [Armbian](https://www.armbian.com/) hat die Unterstützung für Debian 9 (Stretch) aus ihrem APT-Repository eingestellt. Infolgedessen werden die APT-Quellen von Armbian-basierten Stretch-Systemen angepasst, um Kernel-, Gerätebaum-, Bootloader- und Firmware-Pakete aus der Armbian Buster-Suite zu ziehen. Diese sind mit allen Debian-Versionen kompatibel und haben keine Abhängigkeiten, die Konflikte verursachen könnten.

- Kommende **Debian 11 (Bullseye)**-Veröffentlichung :octicons-arrow-right-16: Die DietPi-Installation und DietPi-Tools wurden gründlich getestet, um mit der kommenden Veröffentlichung – Debian 11 Bullseye – vollständig kompatibel zu sein. Lesen Sie mehr über diese Veröffentlichung [hier](https://www.debian.org/releases/bullseye/releasenotes).

### Verbesserungen {: #changes-74 }

- [DietPi-Software | **Home Assistant**](../../software/home_automation/#home-assistant) :octicons-arrow-right-16: Auf ARMv6/7 wird piwheels.org jetzt innerhalb von pyenv verwendet, das vorab ausgeliefert wird. kompilierte Räder für viele Python-Module und beschleunigt dadurch die Installation, den ersten Dienststart und die Installation neuer Integrationen.
- [DietPi-Software | **myMPD**](../../software/media/#mympd) :octicons-arrow-right-16: Aktualisierte Konfigurationsschritte, um mit dem neuen myMPD v8.0.0 zu funktionieren. Vielen Dank an @jcorporation für die Information über dieses wichtige Update und die Anpassung unserer Konfigurationsschritte: <https://github.com/MichaIng/DietPi/issues/4562>
- [DietPi-Software | **Komga**](../../software/media/#komga) :octicons-arrow-right-16: Veraltete Einträge wurden aus der Standardkonfiguration entfernt und Datei-Hashing wird bei Neuinstallationen deaktiviert. Vielen Dank an @quyentruong für den Beitrag zu dieser Änderung: <https://github.com/MichaIng/DietPi/pull/4570>

### Fehlerbehebungen {: #fixes-74 }

- [DietPi-Software](../../software/) | **X.Org X Server** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der X-Server auf PINE A64 fehlschlug, da die falschen `DDX`-Treiberpakete installiert waren. Vielen Dank an @exadeci für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4541>
- [DietPi-Software | **PaperMC**](../../software/gaming/#papermc) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation von Geyser- und Floodgate-Plugins fehlschlug, da sich der Download-Link geändert hatte.
- [DietPi-Software | **Home Assistant**](../../software/home_automation/#home-assistant) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation auf ARMv6/7 fehlschlug, wenn g++ nicht installiert war.
- [DietPi-Software | **Pi-hole**](../../software/dns_servers/#pi-hole) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der lokale/LAN-Zugriff über IPv6 blockiert wurde, wenn die Option dazu verfügbar war Öffentlichen Zugriff auf das Admin-Panel blockieren wurde ausgewählt. Dies funktioniert nicht, wenn globale Unicast-IPv6-Adressen (GUA) innerhalb des LAN verwendet werden, daher müssen eindeutige lokale Adressen (ULA) aktiviert und verwendet werden, um auf das Pi-hole-Admin-Panel zuzugreifen. Vielen Dank an @dunxd für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4575>

Wie immer wurden viele kleinere Codeleistungs- und Stabilitätsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Codeänderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4584>
