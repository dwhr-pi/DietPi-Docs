# DNS-Server

## Überblick

- [**Pi-hole - Netzwerkweite Werbeblockierung**](#pi-hole)
- [**Unbound - Ein validierender, rekursiver und zwischenspeichernder DNS-Resolver**](#unbound)
- [**AdGuard Home - Ein leistungsstarker netzwerkweiter Anzeigen- und Tracker-Blocker-DNS-Server**](#adguard-home)

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

##Pi-Loch

Pi-hole ist ein DNS-Sinkhole mit Webschnittstelle, das Anzeigen für jedes Gerät in Ihrem Netzwerk blockiert.

- Installiert auch: [Webserver-Stack](../webserver_stack/)

![Screenshot der Pi-Hole-Weboberfläche](../assets/images/dietpi-software-dnsserver-pihole.png){: width="500" height="410" loading="lazy"}

!!! Warnung "Webserver-Installation"
    DietPi-Software ruft den Pi-hole-Installer mit dem Flag „--disable-install-webserver“ auf, das die Lighttpd- und PHP-Installationsteile überspringt. Stattdessen werden Lighttpd, Nginx oder Apache separat installiert, je nach Wahl des Benutzers, und PHP als eigenständiger PHP-FPM-Server bzw. Modul für Apache. Dies ermöglicht auch flexiblere Webserver-Konfigurationen, einfaches HTTPS, andere Websites/Anwendungen auf demselben Server usw. Beim **Reparieren** und **Neukonfigurieren** von Pi-Hole (siehe Registerkarte „Pi-Hole reparieren“ unten), Es ist wichtig, Lighttpd NICHT zu installieren, wenn Sie dazu aufgefordert werden, da dies zu doppelten PHP- und Webserver-Installationen oder widersprüchlichen Webserver-Einstellungen führen würde.

=== "Zugriff auf die Weboberfläche"

    Auf die Weboberfläche von Pi-hole kann zugegriffen werden über:

    - URL = `http://<Ihre.IP>/admin`
    - Passwort = `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfiguration"

    Die Konfiguration enthält Einstellungsgeräte (z. B. Router), um Pi-hole für die DNS-Auflösung zu verwenden.

    <font size="+2">Option 1 - Einrichten einzelner Geräte zur Verwendung des Pi-hole-DNS-Servers</font>

    Ändern Sie einfach Ihre DNS-Einstellungen, um die IP-Adresse Ihres Pi-hole-Geräts zu verwenden. Dies muss für jedes Gerät durchgeführt werden, mit dem Pi-hole arbeiten soll.

    Beispiel:

    - Mein Pi-hole-Gerät hat die IP-Adresse 192.168.0.100
    - Auf meinem PC würde ich die DNS-Adresse auf 192.168.0.100 setzen
    - Tutorial [Der ultimative Leitfaden zum Ändern Ihrer DNS-Einstellungen] (https://www.howtogeek.com/167533/the-ultimate-guide-to-changing-your-dns-server/).

    <font size="+2">Option 2 – Richten Sie Ihren Router so ein, dass er den DNS-Server von Pi-hole verwendet</font>

    Diese Methode verweist automatisch jedes Gerät (das DHCP verwendet) in Ihrem Netzwerk auf Pi-hole.
    Auf der Webseite der Systemsteuerung Ihres Routers müssen Sie eine Option namens "DNS-Server" finden. Dies sollte sich unter den DHCP-Einstellungen befinden.

    Geben Sie einfach unter „DNS-Server“ die IP-Adresse Ihres Pi-hole-Geräts ein:

    ![DietPi DNS-Server-Software-Router-Setup](../assets/images/dietpi-software-dnsserver-router-setup.png){: width="400" height="240" loading="lazy"}

    Auf Ihrem Pi-hole-Gerät müssen Sie einen anderen DNS-Server einstellen.
    Abhängig von Ihrer Routerkonfiguration kann das Pi-hole-Gerät möglicherweise nicht auf das Internet zugreifen, wenn Sie diesen Schritt nicht ausführen. Es wird dringend empfohlen, dass das Gerät Pi-hole ausführt und auf einen DNS-Server außerhalb Ihres Netzwerks verweist.

    - Führen Sie den folgenden Befehl aus: `dietpi-config 8 1`
    - Wählen Sie: *Ethernet*
    - Wenn Sie im DHCP-Modus arbeiten, wählen Sie *Change Mode* und dann: *Copy Current address to Static*
    - Wählen Sie *Statisches DNS* aus der Liste und dann einen DNS-Server aus oder geben Sie manuell einen benutzerdefinierten Eintrag ein.
    - Wenn Sie fertig sind, wählen Sie *Übernehmen*, um die Änderungen zu speichern.

=== "DietPi-Unterschiede"

    Die DietPi Pi-Hole-Implementierung verwendet das offizielle Installationsskript, weist jedoch einige Unterschiede im Vergleich zum offiziellen Standard-Setup auf:

    1. Das `/var/log/pihole.log`-Nur-Text-DNS-Abfrageprotokoll ist standardmäßig deaktiviert. Es ist eine zweite Abfrageprotokollimplementierung, da `/etc/pihole/pihole-FTL.db` bereits als datenbankweise Protokollimplementierung verwendet wird, die von der Webschnittstelle verwendet wird, um Langzeitprotokolle zu durchsuchen. Wenn Sie jedoch den Befehl `pihole -t`/`pihole tail` verwenden möchten, um farbige Protokolle auf der Konsole auszugeben, müssen Sie die dateibasierte Protokollierung erneut aktivieren:

        ```sh
        pihole -l on
        ```

       Auch das DietPi [Protokollierungssystem](../../dietpi_tools/#quick-selections) muss geändert werden, um DietPi-RAMlog zu deaktivieren, da sonst `/var/log/pihole.log` stündlich geleert wird.
    2. Die Protokollierungsdauer für das datenbankbezogene DNS-Abfrageprotokoll in `/etc/pihole/pihole-FTL.db` wird von 365 Tagen auf 2 Tage reduziert. Eine interne Diskussion ergab, dass niemand von uns Protokolle verwendet, die älter als ein paar Stunden sind. Ein Jahr Protokolle führt zu Datenbankgrößen von Hunderten von MiB bis GiB. Wir belassen es bei 2 Tagen, damit die Dashboard-Grafiken/Diagramme der Webschnittstelle nach dem (Neu-)Start von Pi-Hole nicht leer sind. Sie können die Protokollierungsdauer einfach anpassen, indem Sie die Konfigurationsdatei „/etc/pihole/pihole-FTL.conf“ bearbeiten. Um beispielsweise die standardmäßigen 365-Tage-Protokolle wiederherzustellen:

        ```sh
        MAXDBDAYS=365
        ```

=== "Aktualisiere Pi-Hole"

    Pi-hole kann über den Shell-Befehl „pihole -up“ aktualisiert werden.

=== "Pi-Loch reparieren"

    Sie können `pihole -r` verwenden, um Ihre Pi-hole-Instanz zu reparieren oder neu zu konfigurieren.

    !!! Warnung "Wählen Sie **NICHT** Lighttpd zu installieren"
        Wählen Sie **NICHT** Lighttpd zu installieren, wenn Sie dazu aufgefordert werden, da dies zu doppelten PHP- und Webserver-Installationen oder widersprüchlichen Webserver-Einstellungen führen würde.

=== "Passwort setzen"

    Wenn Sie Ihr Login-Passwort für die Pi-hole-Admin-Webseite vergessen haben, können Sie es mit dem Shell-Befehl „pihole -a -p“ auf Ihrem Pi-hole-Gerät festlegen.

=== "Blocklisten und Whitelists"

    Es gibt viele Websites im Internet, die Sperrlisten und Whitelists für Pi-Hole anbieten. Sie können verwendet werden, wenn Sie mehr Blockierung wünschen, als die Standardinstallation Ihnen bietet. Hier sind einige Beispiele:

    - [Die große Blocklist-Sammlung von `WaLLy3K`](https://firebog.net/)
    - [Blockliste der Phishing-Armee](https://phishing.army/)
    - [Whitelist-Sammlung von `anudeepND`](https://github.com/anudeepND/whitelist)

=== "Zugriff über OpenVPN oder WireGuard"

    Um VPN-Clients (OpenVPN oder WireGuard) den Zugriff auf Ihre lokale Pi-hole-Instanz zu erlauben, müssen Sie DNS-Anfragen von allen Netzwerkschnittstellen zulassen: `pihole -a -i local`.

=== "Pi-Hole überwachen"

    [DietPi-CloudShell](../system_stats/#dietpi-cloudshell) enthält eine Pi-hole-Szene, mit der die wichtigsten DNS-Abfragen und Blockstatistiken überwacht werden können. Führen Sie einfach „dietpi-cloudshell“ aus, wählen Sie „Scenes“ und vergewissern Sie sich, dass „8 Pi-hole“ ausgewählt ist. Schalten Sie „Output Display“ um, um auszuwählen, ob die Ausgabe auf der aktuellen Konsole oder dem Hauptbildschirm gedruckt werden soll, und wählen Sie dann „Start / Restart“, um die Ausgabe zu starten.

***

Offizielle Website: <https://pi-hole.net/>
Offizielle Dokumentation: <https://docs.pi-hole.net/>
Wikipedia: <https://wikipedia.org/wiki/Pi-hole>
Quellcode: <https://github.com/pi-hole>

DietPi-Blog: [Pi-Hole & Unbound: So haben Sie in wenigen Minuten ein werbefreies und sichereres Internet](https://dietpi.com/blog/?p=564)

YouTube-Video-Tutorial Nr. 1: *Raspberry Pi / Pi-hole / Diet-Pi / Netzwerkweiter Werbeblocker !!!!*.

<iframe src="https://www.youtube-nocookie.com/embed/RO2_eZlVrj4?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

YouTube-Video-Tutorial Nr. 2: [Werbung überall blockieren mit Pi-hole und PiVPN auf DietPi](https://www.youtube.com/watch?v=qbLEHlKkGiE){:class="nospellcheck"}
YouTube Video Tutorial #3 (deutschsprachig): [Raspberry Pi & DietPi : Pi-hole der Werbeblocker für Netzwerke mit Anleitung für AVM FritzBox](https://www.youtube.com/watch?v=vXUvFWhXW6c&list=PLQIL7cyHMGboXtOzwAcX4hGPW6ECbVinp&index=6) {:class="nospellcheck"}
YouTube-Video-Tutorial #4: [Raspberry Pi Zero W mit Pi-hole - günstiger Werbeblocker & Schritt für Schritt Anleitung unter DietPi](https://www.youtube.com/watch?v=IxWuMHu9IYk&list=PLQIL7cyHMGboXtOzwAcX4hGPW6ECbVinp&index=2 ){:class="nospellcheck"}
Blogeintrag mit YouTube-Video #5 (deutschsprachig): [Unbound Installation für PiHole unter DietPi](https://blog.login.gmbh/unbound-installation-fuer-pihole-unter-dietpi/){:class="nospellcheck "}

## Unbound

Unbound ist ein validierender, rekursiver, zwischenspeichernder DNS-Resolver. Es kann Hostnamen auflösen, indem es die Root-Nameserver direkt abfragt und ISP/öffentliche DNS-Resolver ersetzt. Die Eliminierung eines Spielers, der an der Bearbeitung Ihrer DNS-Anfragen beteiligt ist, erhöht Ihre Privatsphäre im Internet. Zusätzlich kann Unbound so konfiguriert werden, dass es das verschlüsselte DoT-Protokoll verwendet, das wiederum einen öffentlichen DNS-Anbieter erfordert, aber stattdessen Anfragen für Ihren LAN-Betreiber und ISP maskiert. Weitere Informationen finden Sie unten auf der Registerkarte „Aktivieren von DNS über TLS (DoT)“.

![Unbound-Logo](../assets/images/dietpi-software-dnsserver-unbound.svg){: width="150" height="34" loading="lazy"}

![Unbound Monitor Screenshot](../assets/images/dietpi-software-unbound.jpg){: width="500" height="274" loading="lazy"}

=== "Standard-DNS-Ports"

    - Standard-DNS-Port: **53**
    - DNS-Port, wenn Pi-hole oder AdGuard Home installiert sind: **5335**

=== "Konfigurationsverzeichnis"

    Dort befindet sich das Konfigurationsverzeichnis: `/etc/unbound`

=== "Protokolle anzeigen"

    Sehen Sie sich die Protokolldateien an:

     ```sh
     journalctl -u unbound
     ```

=== "Aktualisierung ungebunden"

    Update auf neueste Version:

    ```sh
    apt update
    apt upgrade
    ```

=== "DNS über TLS (DoT) aktivieren"

    DoT sendet verschlüsselte DNS-Anfragen und maskiert sie vor Ihrem LAN-Betreiber und ISP. Dafür braucht es aber wieder einen öffentlichen DNS-Provider, um die Root-Nameserver abzufragen, was ansonsten dank Unbound nicht nötig ist. Root-Nameserver-Anfragen können nur unverschlüsselt sein, entweder direkt von Unbound (Standard) oder von einem öffentlichen Anbieter (bei Verwendung von DoT). Ob DoT (oder ein anderes verschlüsseltes DNS-Wrapper-Protokoll) vorzuziehen ist oder nicht, hängt von Ihrem Einzelfall und Ihren Bedürfnissen ab, dh ob Sie Ihrem LAN-Betreiber und ISP mehr vertrauen oder einem öffentlichen DNS-Anbieter. Sie können DoT aktivieren, indem Sie den folgenden Befehlsblock kopieren und ausführen:

    ```sh
    cat << '_EOF_' > /etc/unbound/unbound.conf.d/dietpi-dot.conf
    # Adding DNS-over-TLS support
    server:
    tls-cert-bundle: /etc/ssl/certs/ca-certificates.crt
    forward-zone:
    name: "."
    forward-tls-upstream: yes
    ## Cloudflare
    forward-addr: 1.1.1.1@853#cloudflare-dns.com
    forward-addr: 1.0.0.1@853#cloudflare-dns.com
    ## Quad9
    forward-addr: 9.9.9.9@853#dns.quad9.net
    forward-addr: 149.112.112.112@853#dns.quad9.net
    _EOF_
    ```

??? Hinweis "Die verwendeten DNS-Server sind nur Beispiele und können durch Ihren Favoriten ersetzt werden."
    Eine Liste öffentlicher DNS-Anbieter, ihrer IP-Adressen und ihrer gegebenenfalls enthaltenen Funktionen zum Blockieren von Anzeigen / Inhalten für Erwachsene ist auf Wikipedia verfügbar:

- <https://wikipedia.org/wiki/Public_recursive_name_server>

    Damit die Änderung wirksam wird, muss der Unbound-Dienst neu gestartet werden:

    ```sh
    systemctl restart unbound
    ```

***

Offizielle Website: <https://www.nlnetlabs.nl/projects/unbound/about/>
Offizielle Dokumentation: <https://nlnetlabs.nl/documentation/unbound/unbound>
Neue WIP-Dokumentation: <https://unbound.readthedocs.io/>
Wikipedia: <https://wikipedia.org/wiki/Unbound_(DNS_server)>
Quellcode: <https://github.com/NLnetLabs/unbound>

DietPi-Blog: [Pi-Hole & Unbound: So haben Sie in wenigen Minuten ein werbefreies und sichereres Internet](https://dietpi.com/blog/?p=564)

Blogeintrag mit YouTube-Video: [Unbound Installation für PiHole unter DietPi](https://blog.login.gmbh/unbound-installation-fuer-pihole-unter-dietpi/){:class="nospellcheck"}

## AdGuard-Startseite

AdGuard Home ist ein DNS-Sinkhole mit Webschnittstelle, das Anzeigen für jedes Gerät in Ihrem Netzwerk blockiert.

![Screenshot der AdGuard Home-Weboberfläche](../assets/images/dietpi-software-dnsserver-adguardhome.png){: width="500" height="410" loading="lazy"}

=== "Zugriff auf die Weboberfläche"

    Das Webinterface ist über Port **8083** erreichbar:

    - URL = `http://<Ihre.IP>:8083`
    - Benutzer = „admin“.
    - Passwort = `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfiguration"

    Die Konfiguration enthält Geräte (z. B. Router), die AdGuard Home für die DNS-Auflösung verwenden.

    <font size="+2">Option 1 – Einrichten einzelner Geräte zur Verwendung des AdGuard Home-DNS-Servers</font>

    Ändern Sie einfach Ihre DNS-Einstellungen, um die IP-Adresse Ihres AdGuard Home-Geräts zu verwenden. Dies muss für jedes Gerät durchgeführt werden, mit dem AdGuard Home funktionieren soll.

    Beispiel:

    - Mein AdGuard Home-Gerät hat die IP-Adresse 192.168.0.100
    - Auf meinem PC würde ich die DNS-Adresse auf 192.168.0.100 setzen
    - Tutorial [Der ultimative Leitfaden zum Ändern Ihrer DNS-Einstellungen] (https://www.howtogeek.com/167533/the-ultimate-guide-to-changing-your-dns-server/).

    <font size="+2">Option 2 – Richten Sie Ihren Router so ein, dass er den AdGuard Home-DNS-Server verwendet</font>

    Diese Methode verweist automatisch jedes Gerät (das DHCP verwendet) in Ihrem Netzwerk auf AdGuard Home.
    Auf der Webseite der Systemsteuerung Ihres Routers müssen Sie eine Option namens "DNS-Server" finden. Dies sollte sich unter den DHCP-Einstellungen befinden.

    Geben Sie einfach unter "DNS-Server" die IP-Adresse Ihres AdGuard Home-Geräts ein:

    ![DietPi DNS-Server-Software-Router-Setup](../assets/images/dietpi-software-dnsserver-router-setup.png){: width="400" height="240" loading="lazy"}

    Auf Ihrem AdGuard Home-Gerät müssen Sie einen anderen DNS-Server einstellen.
    Abhängig von Ihrer Routerkonfiguration kann das AdGuard Home-Gerät möglicherweise nicht auf das Internet zugreifen, wenn Sie diesen Schritt nicht ausführen. Es wird dringend empfohlen, auf dem Gerät AdGuard Home auszuführen, das auf einen DNS-Server außerhalb Ihres Netzwerks verweist.

    - Führen Sie den folgenden Befehl aus: `dietpi-config 8 1`
    - Wählen Sie: *Ethernet*
    - Wenn Sie im DHCP-Modus arbeiten, wählen Sie *Change Mode* und dann: *Copy Current address to Static*
    - Wählen Sie *Statisches DNS* aus der Liste und dann einen DNS-Server aus oder geben Sie manuell einen benutzerdefinierten Eintrag ein.
    - Wenn Sie fertig sind, wählen Sie *Übernehmen*, um die Änderungen zu speichern.

=== "Aktualisierung von AdGuard Home"

    Bitte verwenden Sie den internen Updater der Weboberfläche, um Ihr AdGuard Home zu aktualisieren. Sobald ein Update verfügbar ist, wird oben auf der Seite eine Benachrichtigung angezeigt.

    ![Update-Benachrichtigung für AdGuard Home](../assets/images/adguardhome-update-notification.png){: width="753" height="95" loading="lazy"}

=== "Passwort setzen"

    Wenn Sie Ihr Anmeldekennwort für die AdGuard Home-Administrationswebseite vergessen haben, können Sie es mit dem folgenden Shell-Befehl auf Ihrem AdGuard Home-Gerät festlegen.

    ```sh
    G_CONFIG_INJECT 'password:[[:blank:]]' "  password: $(htpasswd -bnBC 10 '' "<your_new_password>" | tr -d ':\n' | sed 's/\$2y/\$2a/')" /mnt/dietpi_userdata/adguardhome/AdGuardHome.yaml
    systemctl restart adguardhome
    ```

=== "Blocklisten und Whitelists"

    Es gibt viele Websites im Internet, die Blocklisten und Whitelists für AdGuard Home bereitstellen. Sie können verwendet werden, wenn Sie mehr Blockierung wünschen, als die Standardinstallation Ihnen bietet. Hier sind einige Beispiele:

    - [Die große Blocklist-Sammlung von `WaLLy3K`](https://firebog.net/)
    - [Blockliste der Phishing-Armee](https://phishing.army/)
    - [Whitelist-Sammlung von `anudeepND`](https://github.com/anudeepND/whitelist)

***

Offizielle Website: <https://adguard.com/en/adguard-home/overview.html>
Offizielle Dokumentation: <https://github.com/AdguardTeam/AdGuardHome/wiki>
Wikipedia: <https://en.wikipedia.org/wiki/AdGuard#AdGuard_Home>
Quellcode: <https://github.com/AdguardTeam/AdGuardHome>
Lizenz: [GPLv3](https://github.com/AdguardTeam/AdGuardHome/blob/master/LICENSE.txt)

[Zurück zur **Liste der optimierten Software**](../../software/)
