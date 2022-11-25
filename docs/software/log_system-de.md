# Systemauswahl protokollieren

## Überblick

- [**DietPi-RAMlog - Leichte RAM-Protokollierung**](#dietpi-ramlog)
- [**Full - Vollständiges Protokollierungssystem mit Rsyslog und Logrotate**](#full-logging)

Es können verschiedene Protokollierungsmethoden von leicht bis vollständig ausgewählt werden. Wenn Sie keine Protokolldateien benötigen, erhalten Sie einen Leistungsschub. Wenn Sie vollständige dauerhafte Systemprotokollierungsfunktionen benötigen, kann DietPi dies auch tun.

Das *Protokollsystem* kann jederzeit geändert werden, indem Sie die „dietpi-software“ ausführen und „Protokollsystem“ aus dem Menü auswählen.

![Auswahl des DietPi-Protokollsystems](../assets/images/dietpi-software-log-system.png){: width="256" height="128" loading="lazy"}

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschließend „Installieren“.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

???+ siehe auch "Logging-Informationen prüfen"
    Eine Beschreibung der grundlegenden Log-Informationsanzeige und Filteroption finden Sie im [HowTo-Abschnitt der DietPi-Dokumentation](../../usage/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## DietPi-RAMlog

Leichtgewichtige tmpfs-basierte RAM-Protokollierungslösung, die die Festplatten-E/A reduziert und möglicherweise die Anwendungsleistung erhöht.

=== "DietPi-RAMlog #1 (Standard)"

    Diese Option ist ideal für Benutzer, die keine Protokolldateien benötigen.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erhöht die Gesamtleistung des Systems
    \+ Erhöht die Lebensdauer Ihrer SD-Karte durch Reduzierung der Dateisystem-IO (Lesen/Schreiben)
    - DietPi löscht automatisch stündlich Protokolldateien in */var/log* (um Speicher freizugeben)
    - Protokolldateien werden NICHT auf der Festplatte gespeichert
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

Anmerkung: Wenn Rsyslog benötigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

=== "DietPi-RAMlog #2"

Diese Option ist ideal für Benutzer, die die Möglichkeit benötigen, Protokolldateien mit dem Vorteil einer verbesserten Leistung zu speichern.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erhöht die Gesamtleistung des Systems
    \+ DietPi speichert/aktualisiert die Protokolldateidaten automatisch stündlich auf der Festplatte */root/log_file_storage*
    \+ DietPi löscht dann die Protokolldateien in */var/log* (um den von DietPi-RAMlog verwendeten Speicher freizugeben)
    - Möglicher Verlust von bis zu 1 Stunde Protokolldateidaten bei Stromunterbrechung
    - Wird die Schreibzyklen der SD-Karte stündlich erhöhen, um Protokolle zu speichern
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

    Anmerkung: Wenn Rsyslog benötigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

    Anmerkung: Diese Option schreibt deutlich weniger als ein System mit konstanter Protokollierung, z. B. der *Full-Logging-Modus*.
    Siehe auch <https://www.raspberrypi.org/forums/viewtopic.php?t=11258>.

## Vollständige Protokollierung

Diese Option ist ideal für Benutzer, die eine dauerhafte maximale Protokollierung ohne Störung durch DietPi benötigen. Rsyslog und Logrotate werden ebenfalls installiert, um Kernsystemprotokolle als Textdateien in „/var/log“ verfügbar zu machen und gleichzeitig das Wachstum jeder einzelnen Protokolldatei zu begrenzen.

    Pro- und Kontra:
    - */var/log* bleibt auf Platte.
    - Verringert die Gesamtleistung des Systems
    - Reduziert die Lebensdauer Ihrer SD-Karte aufgrund erhöhter Dateisystem-I/O (Lesen/Schreiben)
    \+ Wird standardmäßig mit installiertem Rsyslog und Logrotate geliefert
    \+ Der "Standard" von Linux-Protokollierungssystemen, unerlässlich, wenn Ihre Protokolldateidaten für den Systembetrieb und/oder die Wartung von entscheidender Bedeutung sind

[Zurück zur **Liste der optimierten Software**](../../software/)
