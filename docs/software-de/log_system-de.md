# Systemauswahl protokollieren

## &Uuml;berblick

- [**DietPi-RAMlog - Leichte RAM-Protokollierung**](#dietpi-ramlog)
- [**Full - Vollst&auml;ndiges Protokollierungssystem mit Rsyslog und Logrotate**](#full-logging)

Es k&ouml;nnen verschiedene Protokollierungsmethoden von leicht bis vollst&auml;ndig ausgew&auml;hlt werden. Wenn Sie keine Protokolldateien ben&ouml;tigen, erhalten Sie einen Leistungsschub. Wenn Sie vollst&auml;ndige dauerhafte Systemprotokollierungsfunktionen ben&ouml;tigen, kann DietPi dies auch tun.

Das *Protokollsystem* kann jederzeit ge&auml;ndert werden, indem Sie die `dietpi-software` ausf&uuml;hren und `Protokollsystem` aus dem Men&uuml; ausw&auml;hlen.

![Auswahl des DietPi-Protokollsystems](../assets/images/dietpi-software-log-system.png){: width="256" height="128" loading="lazy"}

??? Information "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef&uuml;hrten **DietPi-optimierten Softwareelemente** zu installieren, f&uuml;hren Sie es &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software durchsuchen** und w&auml;hlen Sie einen oder mehrere Artikel aus. W&auml;hlen Sie abschlie&szlig;end `Installieren`.
    DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

???+ siehe auch "Logging-Informationen pr&uuml;fen"
    Eine Beschreibung der grundlegenden Log-Informationsanzeige und Filteroption finden Sie im [HowTo-Abschnitt der DietPi-Dokumentation](../../usage/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

## DietPi-RAMlog

Leichtgewichtige tmpfs-basierte RAM-Protokollierungsl&ouml;sung, die die Festplatten-E/A reduziert und m&ouml;glicherweise die Anwendungsleistung erh&ouml;ht.

=== "DietPi-RAMlog #1 (Standard)"

    Diese Option ist ideal f&uuml;r Benutzer, die keine Protokolldateien ben&ouml;tigen.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erh&ouml;ht die Gesamtleistung des Systems
    \+ Erh&ouml;ht die Lebensdauer Ihrer SD-Karte durch Reduzierung der Dateisystem-IO (Lesen/Schreiben)
    - DietPi l&ouml;scht automatisch st&uuml;ndlich Protokolldateien in */var/log* (um Speicher freizugeben)
    - Protokolldateien werden NICHT auf der Festplatte gespeichert
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

Anmerkung: Wenn Rsyslog ben&ouml;tigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

=== "DietPi-RAMlog #2"

Diese Option ist ideal f&uuml;r Benutzer, die die M&ouml;glichkeit ben&ouml;tigen, Protokolldateien mit dem Vorteil einer verbesserten Leistung zu speichern.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erh&ouml;ht die Gesamtleistung des Systems
    \+ DietPi speichert/aktualisiert die Protokolldateidaten automatisch st&uuml;ndlich auf der Festplatte */root/log_file_storage*
    \+ DietPi l&ouml;scht dann die Protokolldateien in */var/log* (um den von DietPi-RAMlog verwendeten Speicher freizugeben)
    - M&ouml;glicher Verlust von bis zu 1 Stunde Protokolldateidaten bei Stromunterbrechung
    - Wird die Schreibzyklen der SD-Karte st&uuml;ndlich erh&ouml;hen, um Protokolle zu speichern
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

    Anmerkung: Wenn Rsyslog ben&ouml;tigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

    Anmerkung: Diese Option schreibt deutlich weniger als ein System mit konstanter Protokollierung, z. B. der *Full-Logging-Modus*.
    Siehe auch <https://www.raspberrypi.org/forums/viewtopic.php?t=11258>.

## Vollst&auml;ndige Protokollierung

Diese Option ist ideal f&uuml;r Benutzer, die eine dauerhafte maximale Protokollierung ohne St&ouml;rung durch DietPi ben&ouml;tigen. Rsyslog und Logrotate werden ebenfalls installiert, um Kernsystemprotokolle als Textdateien in `/var/log` verf&uuml;gbar zu machen und gleichzeitig das Wachstum jeder einzelnen Protokolldatei zu begrenzen.

    Pro- und Kontra:
    - */var/log* bleibt auf Platte.
    - Verringert die Gesamtleistung des Systems
    - Reduziert die Lebensdauer Ihrer SD-Karte aufgrund erh&ouml;hter Dateisystem-I/O (Lesen/Schreiben)
    \+ Wird standardm&auml;&szlig;ig mit installiertem Rsyslog und Logrotate geliefert
    \+ Der "Standard" von Linux-Protokollierungssystemen, unerl&auml;sslich, wenn Ihre Protokolldateidaten f&uuml;r den Systembetrieb und/oder die Wartung von entscheidender Bedeutung sind

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
