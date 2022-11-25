# Systemstatistiken und -verwaltung

## Überblick

- [**DietPi-Dashboard - Offizielles, leichtes, eigenständiges DietPi-Webinterface**](#dietpi-dashboard)
- [**DietPi-CloudShell - Leichtgewichtige Systemstatistiken für Ihr LCD-Display oder Ihren Monitor**](#dietpi-cloudshell)
- [**Linux Dash - Systemstatistik der Webschnittstelle**](#linux-dash)
- [**phpSysInfo - Systemstatistik der Webschnittstelle**](#phpsysinfo)
- [**RPi-Monitor - Systemstatistiken der Webschnittstelle**](#rpi-monitor)
- [**Netdata - Systemstatistiken der Webschnittstelle**](#netdata)
- [**Webmin - Remote-Systemverwaltung mit Weboberfläche**](#webmin)
- [**K3s – Lightweight Kubernetes**](#k3s)

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschließend „Installieren“.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## DietPi-Dashboard

Das DietPi-Dashboard ist eine sehr leichte und eigenständige Weboberfläche zur Überwachung und Verwaltung Ihres DietPi-Systems mit Ihrem bevorzugten Webbrowser. Es ist in Rust geschrieben. Einen Überblick über seine Funktionen gibt unser Artikel [hier](https://dietpi.com/blog/?p=1137).

![DietPi-Dashboard-Screenshot](../assets/images/dietpi-dashboard.jpg){: width="700" height="346" loading="lazy"}

!!! Warnung "DietPi-Dashboard befindet sich noch in der Beta!"

    Wir empfehlen daher noch nicht, es aktiv auf sensiblen Produktivsystemen einzusetzen.

=== "Webinterface"

    DietPi-Dashboard ist standardmäßig über den TCP-Port **5252** erreichbar:

    - URL: `http://<Ihre.IP>:5252`
    - Passwort: `<Ihr Software-Passwort>` (Standard: `dietpi`)

=== "Verzeichnisse"

    Die ausführbare DietPi-Dashboard-Datei und ihre Konfigurationsdatei finden Sie unter:

    ```
    /opt/dietpi-dashboard
    ```

=== "Konfiguration"

    Die Konfigurationsdatei befindet sich unter:

    ```
    /opt/dietpi-dashboard/config.toml
    ```

    Wenn Sie Änderungen vornehmen, müssen Sie den Dienst anschließend neu starten:

    ```sh
    systemctl restart dietpi-dashboard
    ```

=== "Passwortschutz"

Der Passwortschutz ist ab DietPi v7.9 standardmäßig aktiviert. Wenn Sie es zuvor installiert haben, müssen Sie es über die Konfigurationsdatei aktivieren. Erstellen Sie dazu einen SHA512-Hash des „PASSWORTS“, das Sie für die Anmeldung bei der Webschnittstelle verwenden möchten, und ein zufälliges 64-stelliges Geheimnis, das zum Generieren eines Tokens zum sicheren Übertragen und Speichern in Ihrem Browser verwendet wird. Wenden Sie diese auf die Konfigurationsdatei an und starten Sie den Dienst neu, damit die Änderungen wirksam werden:

    ```sh
    hash=$(echo -n 'PASSWORD' | sha512sum | mawk '{print $1}')
    secret=$(openssl rand -hex 32)
    G_CONFIG_INJECT 'pass[[:blank:]]' 'pass = true' /opt/dietpi-dashboard/config.toml
    GCI_PASSWORD=1 G_CONFIG_INJECT 'hash[[:blank:]]' "hash = \"$hash\"" /opt/dietpi-dashboard/config.toml
    GCI_PASSWORD=1 G_CONFIG_INJECT 'secret[[:blank:]]' "secret = \"$secret\"" /opt/dietpi-dashboard/config.toml
    unset -v hash secret
    systemctl restart dietpi-dashboard
    ```

    Um das Passwort zu ändern, ersetzen Sie einfach den Hash in der Konfigurationsdatei und starten Sie den Dienst neu.

    Wenn Sie eine Abmeldung von allen Browsern erzwingen möchten, ohne das Passwort zu ändern, können Sie stattdessen das Geheimnis ändern. Generieren und wenden Sie ein neues Geheimnis auf die Konfigurationsdatei an und starten Sie den Dienst neu. Jeder Client und Browser muss sich dann erneut anmelden, um das DietPi-Dashboard weiter nutzen zu können, da das gespeicherte Token, das auf Passwort und Geheimnis basiert, ungültig gemacht wurde.

=== "Mehrere Knoten"

    Ab DietPi v8.0 können Sie das DietPi-Dashboard als reinen Backend-Knoten installieren, der kein eigenes Webinterface enthält. Auf solche Nur-Backend-Knoten kann dann von einem anderen vollständigen DietPi-Dashboard Frontend/Webinterface aus zugegriffen werden. Zusätzliche Knoten müssten manuell zur Konfigurationsdatei hinzugefügt werden, die sich unter befindet:

    ```
    /opt/dietpi-dashboard/config.toml
    ```  
    
Wenn Sie Änderungen vornehmen, müssen Sie den Dienst anschließend neu starten:

    ```sh
    systemctl restart dietpi-dashboard
    ```

    !!! Hinweis "Vollständige DietPi-Dashboard-Knoten mit integriertem Frontend können derzeit nicht von anderen Frontends aus aufgerufen werden."

=== "Dienststeuerung"

    Das DietPi-Dashboard wird standardmäßig als systemd-Dienst gestartet und kann daher mit den folgenden Befehlen gesteuert werden:

    ```sh
    systemctl status dietpi-dashboard
    ```

    ```sh
    systemctl stop dietpi-dashboard
    ```

    ```sh
    systemctl start dietpi-dashboard
    ```

    ```sh
    systemctl restart dietpi-dashboard
    ```

=== "Protokolle"

    Dienstprotokolle können mit dem folgenden Befehl überprüft werden:

    ```sh
    journalctl -u dietpi-dashboard
    ```

=== "Aktualisieren"

Sie können DastPi-Dashboard einfach aktualisieren, indem Sie es neu installieren:

    ```sh
    dietpi-software reinstall 200
    ```

***

Quellcode: <https://github.com/ravenclaw900/DietPi-Dashboard>
Lizenz: [GPLv3](https://github.com/ravenclaw900/DietPi-Dashboard/blob/main/LICENSE)

## DietPi-CloudShell

DietPi-CloudShell verwandelt Ihre Konsole oder Ihren LCD-Bildschirm in eine leichtgewichtige Systemstatistikanzeige.

### Beispiel-Screenshots

Die folgenden Screenshots sollen einen Überblick über die Anzeigefunktionen von *DietPi-CloudShell* geben.

=== "CPU-Auslastung"

    ![DietPi-CloudShell-CPU-Auslastungsdialog](../assets/images/dietpi-software-systemstat-cloudshare-cpuusage.jpg){: width="400" height="305" loading="lazy"}

=== "Speicherauslastung"

    ![DietPi-CloudShell-Speichernutzungsdialog](../assets/images/dietpi-software-systemstat-cloudshare-memoryusage.jpg){: width="400" height="293" loading="lazy"}

=== "Speicherdetails"

    ![DietPi-CloudShell-Speicherdetails-Dialog](../assets/images/dietpi-software-systemstat-cloudshare-storagedetails.png){: width="400" height="292" loading="lazy"}

=== "Netzwerkdetails"

    ![DietPi-CloudShell-Netzwerkdetails-Dialog](../assets/images/dietpi-software-systemstat-cloudshare-networkstats.jpg){: width="400" height="303" loading="lazy"}

=== "Pi-Hole-Statistiken"

    ![DietPi-CloudShell-Pi-Hole-Dialog](../assets/images/dietpi-software-systemstat-cloudshare-piholestats.jpg){: width="400" height="305" loading="lazy"}

***

YouTube-Video-Tutorial: *DietPi CloudShell (RPi / Odroid XU4)*

<iframe src="https://www.youtube-nocookie.com/embed/O-W8Z33as_U?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading=" faul"></iframe>

### Aufbau

=== "Konfiguration"

    Starten Sie das DietPi-CloudShell Control Panel:

    ```sh
    dietpi-cloudshell
    ```

![DietPi-CloudShell-Hauptmenü](../assets/images/dietpi-software-systemstat-cloudshare-configuration.png){: width="600" height="298" loading="lazy"}

=== "Szenen"

    DietPi-CloudShell bietet Szenen mit vordefinierten Anzeigeausgaben bzw. Grundrisse.
    Szenen werden im Dialog *Scenes* innerhalb von `dietpi-cloudshell` konfiguriert.

![DietPi-CloudShell-Szenenmenü](../assets/images/dietpi-software-systemstat-cloudshare-scenes.png){: width="600" height="283" loading="lazy"}

=== "Energiesparen"

    Mit dieser Funktion können Sie den Bildschirm automatisch ausschalten und die DietPi-CloudShell-Verarbeitung während einer bestimmten Zeit deaktivieren.
    Bitte beachten Sie, dass diese Funktion erfordert, dass DietPi-CloudShell mit `dietpi-autostart` gestartet wird oder `dietpi-cloudshell` vom Hauptbildschirm aus (`tty1`) ausführt.
    Wenn Sie Änderungen an DietPi-CloudShell über SSH vornehmen, starten Sie nach dem Speichern bitte das System neu, um sicherzustellen, dass diese Funktion aktiviert wird.

Energieeinsparung: `Auto screen off`

### Touchscreen-Unterstützung

=== "Waveshare32"

    Siehe <https://www.waveshare.com/3.2inch-rpi-lcd-b.htm>.
    Diese ist für alle Versionen von Raspberry Pi und Odroid verfügbar. DietPi konfiguriert Ihr System automatisch für das Gerät.
    Führen Sie einfach „dietpi-config“ aus, wählen Sie „Anzeigeoptionen“ und dann „waveshare32“.
    Nach einem Neustart wird Ihr *Waveshare32* aktiv.

![DietPi-CloudShell auf Waveshare32-Touchscreen-Foto](../assets/images/dietpi-software-systemstat-cloudshell-wavesharesupport.png){: width="400" height="258" loading="lazy"}

=== "Odroid 3.5 LCD-Schild"

    Siehe <https://www.hardkernel.com/shop/c1-3-2inch-tfttouchscreen-shield/>.
    Dies ist für alle Odroid-Versionen verfügbar. DietPi konfiguriert Ihr System automatisch für das Gerät.
    Führen Sie einfach „dietpi-config“ aus, wählen Sie „Anzeigeoptionen“ und dann „odroid-lcd35“.
    Nach einem Neustart wird Ihr *Odroid 3.5 LCD* aktiv.

    ![DietPi-CloudShell auf Odroid 3.5 LCD-Foto](../assets/images/dietpi-software-systemstat-cloudshell-touchscreensupport.jpg){: width="400" height="224" loading="lazy"}

=== "Andere Touchscreens"

Die Anzeigefunktion von *DietPi-CloudShell* funktioniert grundsätzlich mit jedem LCD-Display oder Monitor mit einer Auflösung von mindestens 320x240 Pixel.

## Linux-Dash

Mit Linux Dash können Sie Ihre Systemstatistiken von einer Webseite aus überwachen.

- Installiert auch: [LASP-Webserver-Stack](../webserver_stack/)

![Screenshot der Linux Dash-Weboberfläche](../assets/images/dietpi-software-systemstat-linuxdash.png){: width="500" height="270" loading="lazy"}

=== "Zugriff auf Linux Dash"

    Auf die Weboberfläche von *Linux Dash* kann zugegriffen werden über:

    - URL = `http://<your.IP>/linuxdash/app`

***

Offizielle Dokumentation: <https://github.com/afaqurk/linux-dash/wiki>

## phpSysInfo

Ermöglicht es Ihnen, Ihre Systemstatistiken von einer Webseite aus zu überwachen. Die Displayausgabe kann über eine `.ini`-Datei angepasst werden.

- Installiert auch: [LASP-Webserver-Stack](../webserver_stack/)

![Screenshot der phpSysInfo-Weboberfläche](../assets/images/dietpi-software-systemstat-phpsysinfo.png){: width="500" height="268" loading="lazy"}

=== "Zugriff auf phpSysInfo"

    Das Webinterface von *phpSysInfo* erreichen Sie über:

    - URL = `http://<your.IP>/phpsysinfo`

=== "Anpassung"

    Dies geschieht über die Datei `phpsysinfo.ini` die sich im Hauptverzeichnis von phpSysInfo befindet (typisch `/var/www/phpsysinfo`). Eine Beispieldatei `phpsysinfo.ini.new` ist vorhanden und gibt Inline-Informationen über alle Konfigurationsoptionen. Gehen Sie einfach durch diese Datei und entdecken Sie all diese Schnickschnack.

***

Offizielle Website: <https://phpsysinfo.github.io/phpsysinfo>

## RPi-Monitor

RPi-Monitor ist ein schicker, leichter Systemstatistik-Monitor mit Web-Interface.

![Screenshot der RPi-Monitor-Weboberfläche](../assets/images/dietpi-software-systemstat-rpimonitor.png){: width="500" height="364" loading="lazy"}

=== "Hauptmerkmale"

    Die Hauptfunktionen von *RPi-Monitor* sind:

    - Sammeln, Speichern und Präsentieren von Metriken
    - Es ist flexibel konfigurierbar
    - Es ist vom Benutzer erweiterbar
    - Das Teilen von Metriken kann über eine JSON-Datei oder über SNMP erfolgen
    - Alarmoption

=== "Zugriff auf RPi-Monitor"

    Das Webinterface ist über Port **8888** erreichbar:

    - URL = `http://<Ihre.IP>:8888`

=== "Konfiguration"

    Die Konfiguration ist dort beschrieben: <https://xavierberger.github.io/RPi-Monitor-docs/20_index.html>

***

Offizielle Website: <https://github.com/XavierBerger/RPi-Monitor>.

## Nettodaten

Netdata ist ein raffinierter und funktionsreicher Systemstatistikmonitor mit Webschnittstelle.

![Screenshot der Netdata-Weboberfläche](../assets/images/dietpi-software-systemstat-netdata.png){: width="500" height="260" loading="lazy"}

=== "Zugriff auf Netzdaten"

    Das Webinterface ist über Port **19999** erreichbar:

    - URL = `http://<Ihre.IP>:19999`

=== "Fehlerbehebung"

    Abhängig von Ihrem System ist Netdata standardmäßig möglicherweise nicht über Remote-Browser zugänglich. Öffnen Sie in diesem Fall die Konfigurationsdatei
    `/etc/netdata/netdata.conf`
    und die Zeile ändern
    `bind socket to IP = 127.0.0.1`
    um je nach Bedarf entweder die lokale Netzwerk-IP oder die statische öffentliche IP Ihres DietPi-Servers abzugleichen.
    Alternativ kommentieren Sie es zB, wenn Ihr Server keine statische öffentliche IP hat, Sie aber einen Fernzugriff benötigen. Beachten Sie jedoch, dass eine ungeschützte öffentlich zugängliche Netdata-Weboberfläche ein potenzielles Sicherheitsrisiko darstellt. Gehen Sie zur Registerkarte „Sicherheitshärtung“, um mehr darüber zu erfahren, wie Sie den Zugriff auf Netdata einschränken können.

    Nach dem Speichern müssen Sie den Dienst neu starten, um die Änderungen zu implementieren, indem Sie Folgendes in das Terminal eingeben:

    ```sh
    systemctl restart netdata
    ```

=== "Sicherheitshärtung"

    Beachten Sie, dass der Zugriff auf Netdata für jeden potenziellen Angreifer eine Menge nützlicher Informationen gibt, wo sie mit dem Hacken beginnen können.
    Um zu erfahren, wie Sie den Zugriff auf Netdata einschränken können, lesen Sie bitte deren Dokumentation bezüglich [der Konfiguration von Zugriffslisten] (https://learn.netdata.cloud/docs/agent/web/server/#access-lists).

***

Offizielle Dokumentation: <https://learn.netdata.cloud/docs/overview/what-is-netdata>
Wikipedia: <https://wikipedia.org/wiki/Netdata>

##Webmin

Webmin ist ein webbasiertes, funktionsreiches Remote-Systemverwaltungstool. Viele Systemeinstellungen können einfach über die Dialoge der Weboberfläche vorgenommen werden.

![Screenshot der Webmin-Oberfläche](../assets/images/dietpi-software-systemstat-webmin.png){: width="500" height="276" loading="lazy"}

=== "Zugriff auf Webmin"

    Das Webinterface ist über Port **10000** erreichbar:

    - URL = `https://<Ihre.IP>:10000`
    - Benutzername = `root`
    - Passwort = `<Ihr Software-Passwort>` (Standard: `dietpi`)

    ???+ Hinweis "HTTPS verwenden"

    Bitte stellen Sie sicher, dass die URL "https://" eingegeben wird, "http://" funktioniert nicht!

=== "Systemprotokollierung"
    
    Das Webmin-Systemprotokollierungspanel hängt immer noch von einem klassischen Dateilogger wie Rsyslog ab. DietPi wird diesen Protokollierungsaufwand jedoch standardmäßig nicht auf Systemen auferlegen. Wenn Sie Systemprotokolle über das *Webmin-Online-Panel* anzeigen müssen, können Sie entweder einen benutzerdefinierten *syslog*-Daemon konfigurieren oder *Rsyslog* manuell installieren:

    ```sh
    apt install rsyslog
    ```

    DietPi kommt mit *systemd* und dem dazugehörigen *journald* Systemlogger, der über den Befehl `journalctl` aufgerufen werden kann.

***

Offizielle Website: <https://webmin.com/>
<!--Offizielle Dokumentation: <https://doxfer.webmin.com/Webmin/Main_Page> -->
Wikipedia: <https://wikipedia.org/wiki/Webmin>

## K3s

Lightweight Kubernetes – Die zertifizierte Kubernetes-Distribution, die für IoT- und Edge-Computing entwickelt wurde

![K3s-Logo](../assets/images/logo-k3s.svg){: width="300" height="116" loading="lazy"}

=== "Vor der Installation"

    Die Standardinstallation von K3s erstellt einen Single-Node-Cluster.
    Wenn Sie ein Multi-Node-Setup haben möchten, müssen Sie die Nodes so konfigurieren, dass sie mit den anderen sprechen.

    Bearbeiten Sie in `/boot/dietpi.txt` den Parameter `SOFTWARE_K3S_EXEC`, um den Befehl (`server` oder `agent`) festzulegen.
    Sie können nach dem Befehl weitere Befehlszeilenparameter hinzufügen.

    Beispiel:

    ```
    SOFTWARE_K3S_EXEC=server --disable=local-storage
    ```

    Wenn Sie viele Befehlszeilenparameter hinzufügen müssen, wird empfohlen, sie stattdessen in einer Datei abzulegen.
    nur den Befehl (`server` oder `agent`) in `/boot/dietpi.txt` behalten.
    Wenn „/boot/dietpi-k3s.yaml“ vorhanden ist, wird sie während der Installation nach „/etc/rancher/k3s/config.yaml“ kopiert und von K3s verwendet.
    Das Format dieser Datei ist in den [K3s-Dokumenten](https://rancher.com/docs/k3s/latest/en/installation/install-options/#configuration-file) dokumentiert.

=== "Verbinden mit Ihrem Cluster"

    Bei Ausführung im `Server`-Modus generiert K3s eine `kubeconfig`-Datei unter `/etc/rancher/k3s/k3s.yaml`.
    Kopieren Sie diese auf Ihren Client-Rechner und bearbeiten Sie die Einstellung „Server“, um auf den Hostnamen des Servers zu verweisen.

    Platzieren Sie die Datei am Standardspeicherort (`~/.kube/config`) oder zeigen Sie mit der Umgebungsvariable "KUBECONFIG" darauf.

    Sie sollten jetzt mit „kubectl“ mit Ihrem Kubernetes-Cluster interagieren können:

    ```sh
    kubectl get nodes
    kubectl get pods -A
    ```

=== "Protokolle anzeigen"

    - Service: `journalctl -u k3s`

***

Offizielle Website: <https://k3s.io>
Offizielle Dokumentation: <https://rancher.com/docs/k3s/latest/en/>
Quellcode: <https://github.com/k3s-io/k3s>
Lizenz: [Apache 2.0](https://github.com/k3s-io/k3s/blob/master/LICENSE)

[Zurück zur **Liste der optimierten Software**](../../software/)
