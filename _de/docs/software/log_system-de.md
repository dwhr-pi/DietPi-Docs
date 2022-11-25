# Systemauswahl protokollieren

## �berblick

- [**DietPi-RAMlog - Leichte RAM-Protokollierung**](#dietpi-ramlog)
- [**Full - Vollst�ndiges Protokollierungssystem mit Rsyslog und Logrotate**](#full-logging)

Es k�nnen verschiedene Protokollierungsmethoden von leicht bis vollst�ndig ausgew�hlt werden. Wenn Sie keine Protokolldateien ben�tigen, erhalten Sie einen Leistungsschub. Wenn Sie vollst�ndige dauerhafte Systemprotokollierungsfunktionen ben�tigen, kann DietPi dies auch tun.

Das *Protokollsystem* kann jederzeit ge�ndert werden, indem Sie die �dietpi-software� ausf�hren und �Protokollsystem� aus dem Men� ausw�hlen.

![Auswahl des DietPi-Protokollsystems](../assets/images/dietpi-software-log-system.png){: width="256" height="128" loading="lazy"}

??? Information "Wie f�hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef�hrten **DietPi-optimierten Softwareelemente** zu installieren, f�hren Sie es �ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W�hlen Sie **Software durchsuchen** und w�hlen Sie einen oder mehrere Artikel aus. W�hlen Sie abschlie�end �Installieren�.
    DietPi f�hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men�-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

???+ siehe auch "Logging-Informationen pr�fen"
    Eine Beschreibung der grundlegenden Log-Informationsanzeige und Filteroption finden Sie im [HowTo-Abschnitt der DietPi-Dokumentation](../../usage/).

[Zur�ck zur **Liste der optimierten Software**](../../software/)

## DietPi-RAMlog

Leichtgewichtige tmpfs-basierte RAM-Protokollierungsl�sung, die die Festplatten-E/A reduziert und m�glicherweise die Anwendungsleistung erh�ht.

=== "DietPi-RAMlog #1 (Standard)"

    Diese Option ist ideal f�r Benutzer, die keine Protokolldateien ben�tigen.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erh�ht die Gesamtleistung des Systems
    \+ Erh�ht die Lebensdauer Ihrer SD-Karte durch Reduzierung der Dateisystem-IO (Lesen/Schreiben)
    - DietPi l�scht automatisch st�ndlich Protokolldateien in */var/log* (um Speicher freizugeben)
    - Protokolldateien werden NICHT auf der Festplatte gespeichert
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

Anmerkung: Wenn Rsyslog ben�tigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

=== "DietPi-RAMlog #2"

Diese Option ist ideal f�r Benutzer, die die M�glichkeit ben�tigen, Protokolldateien mit dem Vorteil einer verbesserten Leistung zu speichern.

    Pro- und Kontra:
    \+ Mountet */var/log* in RAM
    \+ Erh�ht die Gesamtleistung des Systems
    \+ DietPi speichert/aktualisiert die Protokolldateidaten automatisch st�ndlich auf der Festplatte */root/log_file_storage*
    \+ DietPi l�scht dann die Protokolldateien in */var/log* (um den von DietPi-RAMlog verwendeten Speicher freizugeben)
    - M�glicher Verlust von bis zu 1 Stunde Protokolldateidaten bei Stromunterbrechung
    - Wird die Schreibzyklen der SD-Karte st�ndlich erh�hen, um Protokolle zu speichern
    - Rsyslog wird nicht installiert, um Ressourcen zu sparen. Dies kann die Protokollierung einiger Programme verhindern, die auf Rsyslog angewiesen sind

    Anmerkung: Wenn Rsyslog ben�tigt wird, kann es manuell mit `apt install rsyslog` installiert werden.

    Anmerkung: Diese Option schreibt deutlich weniger als ein System mit konstanter Protokollierung, z. B. der *Full-Logging-Modus*.
    Siehe auch <https://www.raspberrypi.org/forums/viewtopic.php?t=11258>.

## Vollst�ndige Protokollierung

Diese Option ist ideal f�r Benutzer, die eine dauerhafte maximale Protokollierung ohne St�rung durch DietPi ben�tigen. Rsyslog und Logrotate werden ebenfalls installiert, um Kernsystemprotokolle als Textdateien in �/var/log� verf�gbar zu machen und gleichzeitig das Wachstum jeder einzelnen Protokolldatei zu begrenzen.

    Pro- und Kontra:
    - */var/log* bleibt auf Platte.
    - Verringert die Gesamtleistung des Systems
    - Reduziert die Lebensdauer Ihrer SD-Karte aufgrund erh�hter Dateisystem-I/O (Lesen/Schreiben)
    \+ Wird standardm��ig mit installiertem Rsyslog und Logrotate geliefert
    \+ Der "Standard" von Linux-Protokollierungssystemen, unerl�sslich, wenn Ihre Protokolldateidaten f�r den Systembetrieb und/oder die Wartung von entscheidender Bedeutung sind

[Zur�ck zur **Liste der optimierten Software**](../../software/)
