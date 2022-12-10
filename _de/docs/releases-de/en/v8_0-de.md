# Versionshinweise

## Januar 2022 (Version 8.0)

### Überblick

**Januar 2022 Release von DietPi** entfernt die Unterstützung für Debian Stretch und bringt eine inkrementelle Verbesserung der gesamten Plattform.

![Nahaufnahme verschneiter Tannenzweige](../assets/images/dietpi-version-80.jpg){: width="447" height="281" loading="lazy"}

!!! zitiere "_Foto von Alicja, Pixabay_"

### Debian-Stretch-Unterstützung

Die Unterstützung für Debian Stretch wurde ab Version 8.0 entfernt. Diese Änderung ermöglichte uns eine umfassende Codebereinigung und Migration zu einigen neueren Methoden in verschiedenen Bereichen, die nur auf Buster und höher verfügbar sind.

!!! Warnung ""

    Debian 9 „Stretch“ wurde 2017 veröffentlicht und wurde zunächst von Debian 10 „Buster“ und dann von Debian 11 „Bullseye“ abgelöst.

    DietPi v7.9 war die letzte Veröffentlichung mit Unterstützung für Debian Stretch. **DietPi v8.0** und höher erfordern Debian Buster oder neuer.

    Lesen Sie unseren Artikel [**Warum Sie Ihr Stretch-System jetzt aktualisieren sollten**] (https://dietpi.com/blog/?p=1001), um mehr über die Notwendigkeit dieses Upgrades zu erfahren und wie Sie dies ganz einfach tun können Debian Buster und noch weiter bis zur neuesten Version (**Debian Bullseye**).

### Verbesserungen

- **Netzwerk** :octicons-arrow-right-16: Für neue Bilder wird das standardmäßige DHCP-Timeout nicht mehr auf 10 Sekunden reduziert. Dies könnte zu kurz gewesen sein, in diesem Fall werden Netzwerkziele der Boot-Sequenz erreicht, bevor tatsächlich eine IP zugewiesen wurde. Insbesondere bei `AUTO_SETUP_AUTOMATED=1` konnte dies zu Verbindungstest-Timeouts und damit zum Abbruch des automatisierten Erstlaufaufbaus führen. Vielen Dank an @jpeg2600 für die Meldung eines solchen Falls: <https://github.com/MichaIng/DietPi/issues/5143>
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Beim Konfigurieren eines ersten WLAN-Slots über das Scannen nach SSIDs wird der WLAN-Adapter jetzt nicht über `ifup` aufgerufen, aber `ip l dev wlanX up`. Auf diese Weise werden keine DHCP- und WPA-Client-Starts ausgelöst, die zum Scheitern verurteilt sind, wenn der WLAN-Adapter noch mit keinem Access Point verbunden ist. Insbesondere bei dem standardmäßigen DHCP-Timeout von 60 Sekunden würde dies sonst zu einer unnötig langen Verzögerung führen.
- [**DietPi-Dashboard**](../../software/system_stats/#dietpi-dashboard) :octicons-arrow-right-16: Option hinzugefügt, um mehrere Dashboard-Knoten von einer Frontend-Weboberfläche aus anzuzeigen. In diesem Zusammenhang kann das Backend jetzt nur installiert werden, was die Speichernutzung reduziert und es unmöglich macht, außerhalb der Backend-API manuell auf den Knoten zuzugreifen.
- **DietPi-Print_large** :octicons-arrow-right-16: Dieses neue Skript wurde hinzugefügt, das ausgeführt oder von `/boot/dietpi/func/dietpi-print_large` bezogen werden kann, um die über das erste Argument übergebene Zeichenfolge zu drucken in großen Schriftarten im „Figlet“-Stil. Es unterstützt derzeit nur die Zeichen az, AZ, 0-9, Punkt und Bindestrich, also die üblicherweise in Hostnamen erlaubten.
- [**DietPi-Banner**](../../dietpi_tools/#dietpi-banner) :octicons-arrow-right-16: Es wurde eine Option hinzugefügt, um den Hostnamen des Systems in großen Schriftarten im `Figlet`-Stil zu drucken, rechts unter dem Banner-Header. Falls es ebenfalls aktiviert ist, wird die reguläre/kleine Hostname-Zeile dann übersprungen. Vielen Dank an @matelis für die Implementierung dieser Funktion: <https://github.com/MichaIng/DietPi/pull/5113>

    ![DietPi-Banner-Screenshot mit großem Hostnamen](../assets/images/dietpi-banner_large_hostname.png){: width="641" height="362" loading="lazy"}

- **DietPi-Software** | **Mono** :octicons-arrow-right-16: `mono-complete` wird nicht mehr installiert, sondern nur noch `mono-devel`. Dadurch wird der Webserverdienst „XSP4“ übersprungen, der standardmäßig auf Port 8084 lauscht, wo er mit dem Dateibrowser in Konflikt gerät. Dies betrifft nur Neuinstallationen. Sie können diese Änderung manuell anwenden, indem Sie den nächsten Befehl ausführen:

    ```sh
    apt-mark manual mono-devel && apt --autoremove purge mono-complete
    ```

    Vielen Dank an @jaguar489 für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5093>

- **DietPi-Software** | [**FuguHub**](../../software/cloud/#fuguhub) :octicons-arrow-right-16: Der veraltete offizielle Installer wurde durch ein vollautomatisiertes eigenes Setup ersetzt, das veraltete oder sogar schädliche entfernt interaktive Dialoge. Bei Neuinstallationen wird auch ein Administratorkonto „dietpi“ mit einem globalen Softwarepasswort erstellt.
- **DietPi-Software** | [**myMPD**](../../software/media/#mympd) :octicons-arrow-right-16: Die Installation erfolgt jetzt über das offizielle APT-Repository, was eine schnellere Installation im Vergleich zum Kompilieren aus dem Quellcode bedeutet, weniger Abhängigkeiten und einfachere Updates über `apt upgrade`: <https://github.com/MichaIng/DietPi/issues/5115>
- **DietPi-Software** | [**Airsonic**](../../software/media/#airsonic) :octicons-arrow-right-16: Da das Projekt von seinem Betreuer archiviert wurde und unter der kritischen [Log4Shell](https: //dietpi.com/blog/?p=1172) Sicherheitslücke sind wir auf den beworbenen Fork „Airsonic-Advanced“ umgezogen, der auch die Kompatibilität mit Java 17 und damit Debian Bullseye ermöglicht. Airsonic wird im Rahmen des DietPi-Updates neu installiert, um die Migration anzuwenden. Alle Daten und Einstellungen bleiben erhalten und werden automatisch migriert.
- **DietPi-Bilder** | [**Parallels Desktop (macOS)**](../../hardware/#parallels-desktop) :octicons-arrow-right-16: Neues Image der virtuellen Maschine für Parallels Desktop unter macOS.

    ![Parallels Desktop DietPi-Maschine](../assets/images/Parallels1.jpg){: width="640" height="360" loading="lazy"}

### Fehlerbehebung

- [**Raspberry Pi**](../../hardware/#raspberry-pi) :octicons-arrow-right-16: Behebung eines Problems, bei dem unbeabsichtigt der Turbo-Modus aktiviert wurde. Dies wurde auf v7.9, auf unsere bestehenden RPi-Images und per Live-Patch zurückportiert. Vielen Dank an @ayo-x und @whyisthisbroken für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5088>
- **DietPi-FS_partition_resize** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem in einigen Fällen die Bootpartition beim ersten Booten nicht gemountet werden konnte, da das System nach der Größenänderung der Partition in einigen Fällen nicht genügend Zeit dafür hatte Wenden Sie die Änderung vollständig an, bevor Sie mit dem Boot-Mount-Versuch fortfahren. Vielen Dank an @Mausy5043 und @sistemicorp für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5006>
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem auf Raspberry Pi, wenn der vollständige KMS-Anzeigetreiber verwendet wird, die Soundkartenauswahl könnte fälschlicherweise angewendet worden sein. Bei vollständig aktiviertem KMS erscheint für jeden HDMI-Anschluss eine zusätzliche HDMI-Soundkarte (anstelle des regulären Firmware-HDMI-Soundgeräts), selbst wenn kein HDMI-Gerät angeschlossen und das integrierte Audio deaktiviert ist. Dies führte zu einem Anstieg der externen Soundkarten-Indizes. Das Erscheinungsbild der KMS HDMI-Soundkarten ist nun an die Onboard-Firmware der HDMI-Soundkarten angeglichen, dh wenn nicht onboard „auto“ oder HDMI in „dietpi-config“ ausgewählt ist, werden jetzt auch die KMS-HDMI-Soundgeräte deaktiviert und verwenden des Overlay-Parameters "noaudio" des Gerätebaums.
- **DietPi-Software**
    – Es wurde ein Problem behoben, bei dem beim ersten Start Auswahl- und Einstellungsmenüauswahlen einen Fehler auslösten, da die Installationsstatusdatei noch nicht existierte. Vielen Dank an @bsheeres für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5080>
    - Es wurde ein Problem behoben, bei dem die veraltete Option "AUTO_SETUP_FILE_SERVER_INDEX" in der Datei "dietpi.txt" invertiert angewendet wurde. `-1` hätte [ProFTPD](../../software/file_servers/#proftpd) und `-2` Samba installieren sollen, während es umgekehrt gemacht wurde. Beachten Sie jedoch, dass diese Einstellung bei aktuellen Images nicht vorhanden und veraltet ist. Verwenden Sie stattdessen `AUTO_SETUP_INSTALL_SOFTWARE_ID`, um einen oder mehrere Dateiserver für die automatische Installation zu markieren. Vielen Dank an @bsheeres für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5081>
    - **Browser** - Auf den ARMv6-Raspberry-Pi-Modellen Raspberry Pi 1 und Zero (1) seit Bullseye, [Chromium](../../software/desktop/#chromium) und [Firefox](../. ./software/desktop/#firefox) können aufgrund von Hardware- und Build-Einschränkungen, die außerhalb unserer Kontrolle liegen, nicht gestartet werden. Da dies derzeit die einzigen beiden Browser sind, die von `dietpi-software` erhältlich sind, wurden sie zusammen mit dem Browser-Einstellungsmenü für diese Systeme deaktiviert, bis wir einen guten zusätzlichen kompatiblen Browser gefunden und implementiert haben. Weitere Informationen: <https://github.com/RPi-Distro/chromium-browser/issues/21>.
- **DietPi-Software** | [**Kodi**](../../software/media/#kodi) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem nachfolgende Kodi-Neuinstallationen Duplikate des „CMA“-Parameters für die KMS-Overlay-Einstellung erstellten in `config.txt`. Die Duplikate werden während des DietPi-Updates ausgepatcht.
- **DietPi-Software** | [**Docker**](../../software/programming/#docker) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation aufgrund einer falschen Prüfung auf fehlende Kernel-Module abgebrochen wurde. Vielen Dank an @dragonandy für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5061>
- **DietPi-Software** | [**Pi-hole**](../../software/dns_servers/#pi-hole) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Teleporter-Importprotokoll nicht angezeigt, aber vom X verweigert wurde -Frame-Options-Header: <https://discourse.pi-hole.net/t/unable-to-restore-teleporter-backup-fresh-install-no-funky-changes-made/51573>
- **DietPi-Software** | [**Blynk Server**](../../software/hardware_projects/#blynk-server) :octicons-arrow-right-16: Es wurde ein Problem bei ARMv6 RPi-Modellen behoben, bei dem die Installation als neueste Version von Blynk Server fehlschlug enthält keinen Java 8-Build. Da der ältere Java 8-Build keine native Log4Shell-Schwachstellenminderung enthält, wird er auf diesen Systemen serverweise hinzugefügt.
- **DietPi-Software** | [**Mycroft AI**](../../software/hardware_projects/#mycroft-ai) :octicons-arrow-right-16: Es wurde ein Problem auf Bullseye-Systemen (und höher) behoben, bei denen „mycroft-cli-client ` schlägt mit einem Berechtigungsproblem fehl, selbst als Root-Benutzer. Vielen Dank an @berndverhofstadt für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5100>
- **DietPi-Software** | [**Nukkit**](../../software/gaming/#nukkit) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation aufgrund einer geänderten Download-URL fehlschlug. Die Jenkins-Instanz ist nach `ci.opencollab.dev` umgezogen, wo auch die Geyser- und Floodgate-Projekte gehostet werden.
- **DietPi-Software** | [**FuguHub**](../../software/cloud/#fuguhub) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Deinstallation fehlschlug, da der Prozess nicht wie beabsichtigt gestoppt wurde. Vielen Dank an @kd9352 für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5058>
- **DietPi-Software** | [**myMPD**](../../software/media/#mympd) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation aufgrund einer aktualisierten Abhängigkeit fehlschlug. Vielen Dank an @supersexy für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5115>
- **DietPi-Software** | [**Python 3**](../../software/programming/#python-3) :octicons-arrow-right-16: Umgehung eines Problems, bei dem die Neuinstallation von `pip` fehlschlug. Vielen Dank an @hueppinr für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5117>
- **DietPi-Software** | [**Unbound**](../../software/dns_servers/#unbound) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der Dienst „unbound-resolvconf“ localhost automatisch als lokalen Nameserver anwendete, wenn das `resolvconf`-Paket wurde installiert. Da Unbound oft in Kombination mit Pi-hole oder AdGuard Home installiert wird und diese normalerweise nur von Netzwerkclients verwendet werden, nicht vom Server selbst, ist `unbound-resolvconf` jetzt bei Unbound-Installationen deaktiviert. Wenn Unbound auch als lokaler Resolver gewünscht wird, sollte es explizit konfiguriert werden, zB über die Netzwerkoptionen von dietpi-config. Vielen Dank an @Ianszh für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5133>
- **DietPi-Software** | [**Mosquitto**](../../software/hardware_projects/#mosquitto) :octicons-arrow-right-16: Wendete eine Problemumgehung auf ARMv6 an, wo die neuesten Mosquitto-Pakete aus dem offiziellen APT-Repository nicht ARMv6-kompatibel sind . Vielen Dank an @thomasmockridge für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5140>

Wie immer wurden viele kleinere Codeleistungs- und Stabilitätsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Codeänderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/issues/5137>

### Bekannte/ausstehende Probleme

- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Das Aktivieren von WLAN- und Ethernet-Adaptern, beide in unterschiedlichen Subnetzen, unterbricht in einigen Fällen die WLAN-Verbindung : <https://github.com/MichaIng/DietPi/issues/2103>

Für alle zusätzlichen Probleme, die nach der Veröffentlichung auftreten können, besuchen Sie bitte den folgenden Link für aktive Tickets: <https://github.com/MichaIng/DietPi/issues>
