# DNS-Server

## �berblick

- [**Pi-hole - Netzwerkweite Werbeblockierung**](#pi-hole)
- [**Unbound - Ein validierender, rekursiver und zwischenspeichernder DNS-Resolver**](#unbound)
- [**AdGuard Home - Ein leistungsstarker netzwerkweiter Anzeigen- und Tracker-Blocker-DNS-Server**](#adguard-home)

??? Information "Wie f�hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef�hrten **DietPi-optimierten Softwareelemente** zu installieren, f�hren Sie es �ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W�hlen Sie **Software durchsuchen** und w�hlen Sie einen oder mehrere Artikel aus. W�hlen Sie abschlie�end �Installieren�.
    DietPi f�hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men�-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur�ck zur **Liste der optimierten Software**](../../software/)

##Pi-Loch

Pi-hole ist ein DNS-Sinkhole mit Webschnittstelle, das Anzeigen f�r jedes Ger�t in Ihrem Netzwerk blockiert.

- Installiert auch: [Webserver-Stack](../webserver_stack/)

![Screenshot der Pi-Hole-Weboberfl�che](../assets/images/dietpi-software-dnsserver-pihole.png){: width="500" height="410" loading="lazy"}

!!! Warnung "Webserver-Installation"
    DietPi-Software ruft den Pi-hole-Installer mit dem Flag �--disable-install-webserver� auf, das die Lighttpd- und PHP-Installationsteile �berspringt. Stattdessen werden Lighttpd, Nginx oder Apache separat installiert, je nach Wahl des Benutzers, und PHP als eigenst�ndiger PHP-FPM-Server bzw. Modul f�r Apache. Dies erm�glicht auch flexiblere Webserver-Konfigurationen, einfaches HTTPS, andere Websites/Anwendungen auf demselben Server usw. Beim **Reparieren** und **Neukonfigurieren** von Pi-Hole (siehe Registerkarte �Pi-Hole reparieren� unten), Es ist wichtig, Lighttpd NICHT zu installieren, wenn Sie dazu aufgefordert werden, da dies zu doppelten PHP- und Webserver-Installationen oder widerspr�chlichen Webserver-Einstellungen f�hren w�rde.

=== "Zugriff auf die Weboberfl�che"

    Auf die Weboberfl�che von Pi-hole kann zugegriffen werden �ber:

    - URL = `http://<Ihre.IP>/admin`
    - Passwort = `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfiguration"

    Die Konfiguration enth�lt Einstellungsger�te (z. B. Router), um Pi-hole f�r die DNS-Aufl�sung zu verwenden.

    <font size="+2">Option 1 - Einrichten einzelner Ger�te zur Verwendung des Pi-hole-DNS-Servers</font>

    �ndern Sie einfach Ihre DNS-Einstellungen, um die IP-Adresse Ihres Pi-hole-Ger�ts zu verwenden. Dies muss f�r jedes Ger�t durchgef�hrt werden, mit dem Pi-hole arbeiten soll.

    Beispiel:

    - Mein Pi-hole-Ger�t hat die IP-Adresse 192.168.0.100
    - Auf meinem PC w�rde ich die DNS-Adresse auf 192.168.0.100 setzen
    - Tutorial [Der ultimative Leitfaden zum �ndern Ihrer DNS-Einstellungen] (https://www.howtogeek.com/167533/the-ultimate-guide-to-changing-your-dns-server/).

    <font size="+2">Option 2 � Richten Sie Ihren Router so ein, dass er den DNS-Server von Pi-hole verwendet</font>

    Diese Methode verweist automatisch jedes Ger�t (das DHCP verwendet) in Ihrem Netzwerk auf Pi-hole.
    Auf der Webseite der Systemsteuerung Ihres Routers m�ssen Sie eine Option namens "DNS-Server" finden. Dies sollte sich unter den DHCP-Einstellungen befinden.

    Geben Sie einfach unter �DNS-Server� die IP-Adresse Ihres Pi-hole-Ger�ts ein:

    ![DietPi DNS-Server-Software-Router-Setup](../assets/images/dietpi-software-dnsserver-router-setup.png){: width="400" height="240" loading="lazy"}

    Auf Ihrem Pi-hole-Ger�t m�ssen Sie einen anderen DNS-Server einstellen.
    Abh�ngig von Ihrer Routerkonfiguration kann das Pi-hole-Ger�t m�glicherweise nicht auf das Internet zugreifen, wenn Sie diesen Schritt nicht ausf�hren. Es wird dringend empfohlen, dass das Ger�t Pi-hole ausf�hrt und auf einen DNS-Server au�erhalb Ihres Netzwerks verweist.

    - F�hren Sie den folgenden Befehl aus: `dietpi-config 8 1`
    - W�hlen Sie: *Ethernet*
    - Wenn Sie im DHCP-Modus arbeiten, w�hlen Sie *Change Mode* und dann: *Copy Current address to Static*
    - W�hlen Sie *Statisches DNS* aus der Liste und dann einen DNS-Server aus oder geben Sie manuell einen benutzerdefinierten Eintrag ein.
    - Wenn Sie fertig sind, w�hlen Sie *�bernehmen*, um die �nderungen zu speichern.

=== "DietPi-Unterschiede"

    Die DietPi Pi-Hole-Implementierung verwendet das offizielle Installationsskript, weist jedoch einige Unterschiede im Vergleich zum offiziellen Standard-Setup auf:

    1. Das `/var/log/pihole.log`-Nur-Text-DNS-Abfrageprotokoll ist standardm��ig deaktiviert. Es ist eine zweite Abfrageprotokollimplementierung, da `/etc/pihole/pihole-FTL.db` bereits als datenbankweise Protokollimplementierung verwendet wird, die von der Webschnittstelle verwendet wird, um Langzeitprotokolle zu durchsuchen. Wenn Sie jedoch den Befehl `pihole -t`/`pihole tail` verwenden m�chten, um farbige Protokolle auf der Konsole auszugeben, m�ssen Sie die dateibasierte Protokollierung erneut aktivieren:

        ```sh
        pihole -l on
        ```

       Auch das DietPi [Protokollierungssystem](../../dietpi_tools/#quick-selections) muss ge�ndert werden, um DietPi-RAMlog zu deaktivieren, da sonst `/var/log/pihole.log` st�ndlich geleert wird.
    2. Die Protokollierungsdauer f�r das datenbankbezogene DNS-Abfrageprotokoll in `/etc/pihole/pihole-FTL.db` wird von 365 Tagen auf 2 Tage reduziert. Eine interne Diskussion ergab, dass niemand von uns Protokolle verwendet, die �lter als ein paar Stunden sind. Ein Jahr Protokolle f�hrt zu Datenbankgr��en von Hunderten von MiB bis GiB. Wir belassen es bei 2 Tagen, damit die Dashboard-Grafiken/Diagramme der Webschnittstelle nach dem (Neu-)Start von Pi-Hole nicht leer sind. Sie k�nnen die Protokollierungsdauer einfach anpassen, indem Sie die Konfigurationsdatei �/etc/pihole/pihole-FTL.conf� bearbeiten. Um beispielsweise die standardm��igen 365-Tage-Protokolle wiederherzustellen:

        ```sh
        MAXDBDAYS=365
        ```

=== "Aktualisiere Pi-Hole"

    Pi-hole kann �ber den Shell-Befehl �pihole -up� aktualisiert werden.

=== "Pi-Loch reparieren"

    Sie k�nnen `pihole -r` verwenden, um Ihre Pi-hole-Instanz zu reparieren oder neu zu konfigurieren.

    !!! Warnung "W�hlen Sie **NICHT** Lighttpd zu installieren"
        W�hlen Sie **NICHT** Lighttpd zu installieren, wenn Sie dazu aufgefordert werden, da dies zu doppelten PHP- und Webserver-Installationen oder widerspr�chlichen Webserver-Einstellungen f�hren w�rde.

=== "Passwort setzen"

    Wenn Sie Ihr Login-Passwort f�r die Pi-hole-Admin-Webseite vergessen haben, k�nnen Sie es mit dem Shell-Befehl �pihole -a -p� auf Ihrem Pi-hole-Ger�t festlegen.

=== "Blocklisten und Whitelists"

    Es gibt viele Websites im Internet, die Sperrlisten und Whitelists f�r Pi-Hole anbieten. Sie k�nnen verwendet werden, wenn Sie mehr Blockierung w�nschen, als die Standardinstallation Ihnen bietet. Hier sind einige Beispiele:

    - [Die gro�e Blocklist-Sammlung von `WaLLy3K`](https://firebog.net/)
    - [Blockliste der Phishing-Armee](https://phishing.army/)
    - [Whitelist-Sammlung von `anudeepND`](https://github.com/anudeepND/whitelist)

=== "Zugriff �ber OpenVPN oder WireGuard"

    Um VPN-Clients (OpenVPN oder WireGuard) den Zugriff auf Ihre lokale Pi-hole-Instanz zu erlauben, m�ssen Sie DNS-Anfragen von allen Netzwerkschnittstellen zulassen: `pihole -a -i local`.

=== "Pi-Hole �berwachen"

    [DietPi-CloudShell](../system_stats/#dietpi-cloudshell) enth�lt eine Pi-hole-Szene, mit der die wichtigsten DNS-Abfragen und Blockstatistiken �berwacht werden k�nnen. F�hren Sie einfach �dietpi-cloudshell� aus, w�hlen Sie �Scenes� und vergewissern Sie sich, dass �8 Pi-hole� ausgew�hlt ist. Schalten Sie �Output Display� um, um auszuw�hlen, ob die Ausgabe auf der aktuellen Konsole oder dem Hauptbildschirm gedruckt werden soll, und w�hlen Sie dann �Start / Restart�, um die Ausgabe zu starten.

***

Offizielle Website: <https://pi-hole.net/>
Offizielle Dokumentation: <https://docs.pi-hole.net/>
Wikipedia: <https://wikipedia.org/wiki/Pi-hole>
Quellcode: <https://github.com/pi-hole>

DietPi-Blog: [Pi-Hole & Unbound: So haben Sie in wenigen Minuten ein werbefreies und sichereres Internet](https://dietpi.com/blog/?p=564)

YouTube-Video-Tutorial Nr. 1: *Raspberry Pi / Pi-hole / Diet-Pi / Netzwerkweiter Werbeblocker !!!!*.

<iframe src="https://www.youtube-nocookie.com/embed/RO2_eZlVrj4?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

YouTube-Video-Tutorial Nr. 2: [Werbung �berall blockieren mit Pi-hole und PiVPN auf DietPi](https://www.youtube.com/watch?v=qbLEHlKkGiE){:class="nospellcheck"}
YouTube Video Tutorial #3 (deutschsprachig): [Raspberry Pi & DietPi : Pi-hole der Werbeblocker f�r Netzwerke mit Anleitung f�r AVM FritzBox](https://www.youtube.com/watch?v=vXUvFWhXW6c&list=PLQIL7cyHMGboXtOzwAcX4hGPW6ECbVinp&index=6) {:class="nospellcheck"}
YouTube-Video-Tutorial #4: [Raspberry Pi Zero W mit Pi-hole - g�nstiger Werbeblocker & Schritt f�r Schritt Anleitung unter DietPi](https://www.youtube.com/watch?v=IxWuMHu9IYk&list=PLQIL7cyHMGboXtOzwAcX4hGPW6ECbVinp&index=2 ){:class="nospellcheck"}
Blogeintrag mit YouTube-Video #5 (deutschsprachig): [Unbound Installation f�r PiHole unter DietPi](https://blog.login.gmbh/unbound-installation-fuer-pihole-unter-dietpi/){:class="nospellcheck "}

## Unbound

Unbound ist ein validierender, rekursiver, zwischenspeichernder DNS-Resolver. Es kann Hostnamen aufl�sen, indem es die Root-Nameserver direkt abfragt und ISP/�ffentliche DNS-Resolver ersetzt. Die Eliminierung eines Spielers, der an der Bearbeitung Ihrer DNS-Anfragen beteiligt ist, erh�ht Ihre Privatsph�re im Internet. Zus�tzlich kann Unbound so konfiguriert werden, dass es das verschl�sselte DoT-Protokoll verwendet, das wiederum einen �ffentlichen DNS-Anbieter erfordert, aber stattdessen Anfragen f�r Ihren LAN-Betreiber und ISP maskiert. Weitere Informationen finden Sie unten auf der Registerkarte �Aktivieren von DNS �ber TLS (DoT)�.

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

=== "DNS �ber TLS (DoT) aktivieren"

    DoT sendet verschl�sselte DNS-Anfragen und maskiert sie vor Ihrem LAN-Betreiber und ISP. Daf�r braucht es aber wieder einen �ffentlichen DNS-Provider, um die Root-Nameserver abzufragen, was ansonsten dank Unbound nicht n�tig ist. Root-Nameserver-Anfragen k�nnen nur unverschl�sselt sein, entweder direkt von Unbound (Standard) oder von einem �ffentlichen Anbieter (bei Verwendung von DoT). Ob DoT (oder ein anderes verschl�sseltes DNS-Wrapper-Protokoll) vorzuziehen ist oder nicht, h�ngt von Ihrem Einzelfall und Ihren Bed�rfnissen ab, dh ob Sie Ihrem LAN-Betreiber und ISP mehr vertrauen oder einem �ffentlichen DNS-Anbieter. Sie k�nnen DoT aktivieren, indem Sie den folgenden Befehlsblock kopieren und ausf�hren:

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

??? Hinweis "Die verwendeten DNS-Server sind nur Beispiele und k�nnen durch Ihren Favoriten ersetzt werden."
    Eine Liste �ffentlicher DNS-Anbieter, ihrer IP-Adressen und ihrer gegebenenfalls enthaltenen Funktionen zum Blockieren von Anzeigen / Inhalten f�r Erwachsene ist auf Wikipedia verf�gbar:

- <https://wikipedia.org/wiki/Public_recursive_name_server>

    Damit die �nderung wirksam wird, muss der Unbound-Dienst neu gestartet werden:

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

Blogeintrag mit YouTube-Video: [Unbound Installation f�r PiHole unter DietPi](https://blog.login.gmbh/unbound-installation-fuer-pihole-unter-dietpi/){:class="nospellcheck"}

## AdGuard-Startseite

AdGuard Home ist ein DNS-Sinkhole mit Webschnittstelle, das Anzeigen f�r jedes Ger�t in Ihrem Netzwerk blockiert.

![Screenshot der AdGuard Home-Weboberfl�che](../assets/images/dietpi-software-dnsserver-adguardhome.png){: width="500" height="410" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    Das Webinterface ist �ber Port **8083** erreichbar:

    - URL = `http://<Ihre.IP>:8083`
    - Benutzer = �admin�.
    - Passwort = `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfiguration"

    Die Konfiguration enth�lt Ger�te (z. B. Router), die AdGuard Home f�r die DNS-Aufl�sung verwenden.

    <font size="+2">Option 1 � Einrichten einzelner Ger�te zur Verwendung des AdGuard Home-DNS-Servers</font>

    �ndern Sie einfach Ihre DNS-Einstellungen, um die IP-Adresse Ihres AdGuard Home-Ger�ts zu verwenden. Dies muss f�r jedes Ger�t durchgef�hrt werden, mit dem AdGuard Home funktionieren soll.

    Beispiel:

    - Mein AdGuard Home-Ger�t hat die IP-Adresse 192.168.0.100
    - Auf meinem PC w�rde ich die DNS-Adresse auf 192.168.0.100 setzen
    - Tutorial [Der ultimative Leitfaden zum �ndern Ihrer DNS-Einstellungen] (https://www.howtogeek.com/167533/the-ultimate-guide-to-changing-your-dns-server/).

    <font size="+2">Option 2 � Richten Sie Ihren Router so ein, dass er den AdGuard Home-DNS-Server verwendet</font>

    Diese Methode verweist automatisch jedes Ger�t (das DHCP verwendet) in Ihrem Netzwerk auf AdGuard Home.
    Auf der Webseite der Systemsteuerung Ihres Routers m�ssen Sie eine Option namens "DNS-Server" finden. Dies sollte sich unter den DHCP-Einstellungen befinden.

    Geben Sie einfach unter "DNS-Server" die IP-Adresse Ihres AdGuard Home-Ger�ts ein:

    ![DietPi DNS-Server-Software-Router-Setup](../assets/images/dietpi-software-dnsserver-router-setup.png){: width="400" height="240" loading="lazy"}

    Auf Ihrem AdGuard Home-Ger�t m�ssen Sie einen anderen DNS-Server einstellen.
    Abh�ngig von Ihrer Routerkonfiguration kann das AdGuard Home-Ger�t m�glicherweise nicht auf das Internet zugreifen, wenn Sie diesen Schritt nicht ausf�hren. Es wird dringend empfohlen, auf dem Ger�t AdGuard Home auszuf�hren, das auf einen DNS-Server au�erhalb Ihres Netzwerks verweist.

    - F�hren Sie den folgenden Befehl aus: `dietpi-config 8 1`
    - W�hlen Sie: *Ethernet*
    - Wenn Sie im DHCP-Modus arbeiten, w�hlen Sie *Change Mode* und dann: *Copy Current address to Static*
    - W�hlen Sie *Statisches DNS* aus der Liste und dann einen DNS-Server aus oder geben Sie manuell einen benutzerdefinierten Eintrag ein.
    - Wenn Sie fertig sind, w�hlen Sie *�bernehmen*, um die �nderungen zu speichern.

=== "Aktualisierung von AdGuard Home"

    Bitte verwenden Sie den internen Updater der Weboberfl�che, um Ihr AdGuard Home zu aktualisieren. Sobald ein Update verf�gbar ist, wird oben auf der Seite eine Benachrichtigung angezeigt.

    ![Update-Benachrichtigung f�r AdGuard Home](../assets/images/adguardhome-update-notification.png){: width="753" height="95" loading="lazy"}

=== "Passwort setzen"

    Wenn Sie Ihr Anmeldekennwort f�r die AdGuard Home-Administrationswebseite vergessen haben, k�nnen Sie es mit dem folgenden Shell-Befehl auf Ihrem AdGuard Home-Ger�t festlegen.

    ```sh
    G_CONFIG_INJECT 'password:[[:blank:]]' "  password: $(htpasswd -bnBC 10 '' "<your_new_password>" | tr -d ':\n' | sed 's/\$2y/\$2a/')" /mnt/dietpi_userdata/adguardhome/AdGuardHome.yaml
    systemctl restart adguardhome
    ```

=== "Blocklisten und Whitelists"

    Es gibt viele Websites im Internet, die Blocklisten und Whitelists f�r AdGuard Home bereitstellen. Sie k�nnen verwendet werden, wenn Sie mehr Blockierung w�nschen, als die Standardinstallation Ihnen bietet. Hier sind einige Beispiele:

    - [Die gro�e Blocklist-Sammlung von `WaLLy3K`](https://firebog.net/)
    - [Blockliste der Phishing-Armee](https://phishing.army/)
    - [Whitelist-Sammlung von `anudeepND`](https://github.com/anudeepND/whitelist)

***

Offizielle Website: <https://adguard.com/en/adguard-home/overview.html>
Offizielle Dokumentation: <https://github.com/AdguardTeam/AdGuardHome/wiki>
Wikipedia: <https://en.wikipedia.org/wiki/AdGuard#AdGuard_Home>
Quellcode: <https://github.com/AdguardTeam/AdGuardHome>
Lizenz: [GPLv3](https://github.com/AdguardTeam/AdGuardHome/blob/master/LICENSE.txt)

[Zur�ck zur **Liste der optimierten Software**](../../software/)
