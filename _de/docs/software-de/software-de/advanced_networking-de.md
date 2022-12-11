# Erweitertes Netzwerk

## Überblick

- [**WiFi HotSpot - Verwandeln Sie Ihr Gerät in einen drahtlosen Hotspot/Zugangspunkt**](#wifi-hotspot)
- [**Tor HotSpot - Optional: Leitet den gesamten WLAN-HotSpot-Verkehr durch das Tor-Netzwerk**](#tor-hotspot)
- [**HAProxy - Hochleistungs-TCP/HTTP-Load-Balancer**](#haproxy)
- [**frp - Reverse-Proxy**](#frp)

??? info "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschlie&szlig;end `Installieren`.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## WLAN-HotSpot

Das WiFi-HotSpot-Paket verwandelt Ihr Gerät in einen drahtlosen Hotspot/Zugangspunkt. Dadurch k&ouml;nnen andere drahtlose Geräte eine Verbindung herstellen und die Internetverbindung teilen.

![DietPi WLAN-Hotspot WLAN](../assets/images/dietpi-software-advanced-networking-wifihotspot.png){: width="550" height="345" loading="lazy"}

=== "Anforderungen"

    Die Anforderungen sind:

    - 1x Ethernet-Verbindung
    - 1x unterstützter USB-WLAN-Adapter oder integriertes WLAN. Dies kann je nach Gerät und verfügbaren WLAN-Treibern/Modulen variieren. Gängige Adapter (z. B. Atheros) sollten jedoch in Ordnung sein.

=== "Erste Verbindungsdaten"

    Verwenden Sie die folgenden Anmeldeinformationen, um Geräte anfänglich mit Ihrem Hotspot zu verbinden.

- SSID = `DietPi-HotSpot`
- Zugangsschlüssel = `dietpihotspot`

=== "WLAN-HotSpot-Einstellungen ändern"

    Nach der Installation k&ouml;nnen Sie die WLAN-HotSpot-Einstellungen (SSID/Schlüssel/Kanal) jederzeit ändern:

    1. Führen Sie `dietpi-config` aus
    2. Navigieren Sie zu *Netzwerkoptionen: Adapter* und wählen Sie dann *WiFi*
    3. Es wird dringend empfohlen, in diesem Menü den Ländercode auf Ihr Land einzustellen. Abhängig von den Vorschriften Ihres Landes k&ouml;nnte dies die Kanäle 12/13 und eine erh&ouml;hte Ausgangsleistung (Reichweite) für den Hotspot erm&ouml;glichen

***

YouTube-Video-Tutorial: `Raspberry Hotspot: Internet Sperren umgehen mit eigenem WiFi Hotspot unter DietPi (für alle Geräte)`.

<iframe src="https://www.youtube-nocookie.com/embed/3ZROq90tM_s?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

## Tor-HotSpot

Das Tor-HotSpot-Paket verwandelt Ihr Gerät in einen WLAN-HotSpot/Access Point mit Tor-Routing. Der gesamte WiFi-HotSpot-Datenverkehr für alle verbundenen WiFi-Geräte wird durch das Tor-Netzwerk geleitet.
Dies ist perfekt für Benutzer, die Anonymität und Privatsphäre ben&ouml;tigen.

Es installiert auch:

    - [WLAN-HotSpot](#wifi-hotspot_1)

![DietPi WLAN-Hotspot-Tor](../assets/images/dietpi-software-advanced-networking-torhotspot.png){: width="550" height="308" loading="lazy"}

=== "Anforderungen"

    Die Anforderungen sind:

    - 1x Ethernet-Verbindung
    - 1x unterstützter USB-WLAN-Adapter oder integriertes WLAN. Dies kann je nach Gerät und verfügbaren WLAN-Treibern/Modulen variieren. Gängige Adapter (z. B. Atheros) sollten jedoch in Ordnung sein.

=== "Verbindungsdaten"

    Diese sind identisch mit den [WiFi-HotSpot-Anmeldedaten](#wifi-hotspot_1).

=== "Verifizierung"

    Um zu überprüfen, ob der Datenverkehr durch Tor geleitet wird, k&ouml;nnen Sie Folgendes überprüfen:
    Rufen Sie auf dem verbundenen WLAN-Gerät die folgende URL auf: <https://check.torproject.org>

=== "Protokolle anzeigen"

    Tor-Dienstprotokolle k&ouml;nnen mit dem folgenden Befehl angezeigt werden:

    ```sh
    journalctl -t tor
    ```

***

Wikipedia: <https://wikipedia.org/wiki/Tor_(anonymity_network)>
YouTube-Video-Tutorial: *DietPi Tor Hotspot-Setup auf Raspberry Pi 3 B Plus*.

<iframe src="https://www.youtube-nocookie.com/embed/rik-ABzSoHM?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading=" faul"></iframe>

## HAProxy

HAProxy steht für High Availability Proxy und ist eine beliebte Open-Source-Software für TCP/HTTP Load Balancer und Proxy-L&ouml;sung. Seine häufigste Verwendung besteht darin, die Leistung und Zuverlässigkeit einer Serverumgebung zu verbessern, indem die Arbeitslast auf mehrere Server (z. B. Web, Anwendung, Datenbank) verteilt wird.

Es eignet sich am besten für stark frequentierte Websites und betreibt eine ganze Reihe der meistbesuchten der Welt: GitHub, Imgur, Instagram und Twitter. Es ist zum De-facto-Standard-Open-Source-Load-Balancer geworden und wird häufig standardmä&szlig;ig auf Cloud-Plattformen bereitgestellt.

![HAProxy-Statistik-Webseite](../assets/images/dietpi-software-advanced-networking-haproxy2.jpg){: width="1898" height="650" loading="lazy"}

!!! Warnung "Dieser Softwaretitel wird NUR für fortgeschrittene Benutzer empfohlen!"

=== "Schnellstart"

    Nach der Installation müssen Sie die `haproxy.cfg` manuell ändern, damit sie Ihren Netzwerkanforderungen am besten entspricht. Überprüfen Sie das Konfigurationshandbuch [hier](https://www.haproxy.org/#docs).

    ```sh
    systemctl stop haproxy
    nano /etc/haproxy/haproxy.cfg
    systemctl start haproxy    
    ```

    Das Statistik-Webinterface ist über Port **1338** erreichbar:

    - URL = `http://<Ihre.IP>:1338`
    - Benutzername = `admin`
    - Passwort = `dietpi`

    !!! Hinweis "Diese Installation wurde von Jerome Queneuder erm&ouml;glicht, der die Methoden zum Kompilieren und Installieren bereitstellte."

=== "Lastverteilung"

    Die einfachste M&ouml;glichkeit, den Netzwerkverkehr auf mehrere Server auszugleichen, ist die Verwendung von Layer 4 (Transport Layer) Load Balancing. Der Lastausgleich auf diese Weise leitet den Benutzerdatenverkehr basierend auf dem IP-Bereich und dem Port weiter.

    ![Layer-4-Load-Balancing-Piktogramm](../assets/images/dietpi-software-advanced-networking-layer4.jpg){: width="690" height="248" loading="lazy"}

    Der Benutzer greift auf den Load Balancer zu, der die Anfrage des Benutzers an die Web-Backend-Gruppe von Backend-Servern weiterleitet. Welcher Backend-Server auch immer ausgewählt wird, antwortet direkt auf die Anfrage des Benutzers.

    Aus dem Tutorial extrahierter Hilfetext: [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)

=== "Hohe Verfügbarkeit"

    Ein Hochverfügbarkeits-Setup (HA) ist eine Infrastruktur ohne Single Point of Failure. Es verhindert, dass ein Ausfall eines einzelnen Servers zu einem Ausfallereignis wird, indem jeder Ebene Ihrer Architektur Redundanz hinzugefügt wird. Ein Load Balancer erleichtert die Redundanz für die Backend-Schicht (Web-/App-Server), aber für eine echte Einrichtung mit hoher Verfügbarkeit ben&ouml;tigen Sie auch redundante Load Balancer.

    Hier ist ein Diagramm einer grundlegenden Einrichtung für hohe Verfügbarkeit:
    ![Animiertes Hochverfügbarkeits-Setup-Diagramm](../assets/images/dietpi-software-advanced-networking-high-availability.gif){: width="1200" height="577" loading="lazy"}

    Aus dem Tutorial extrahierter Hilfetext: [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)

***

Website: <https://www.haproxy.org/>
Offizielle Dokumentation: <https://www.haproxy.org/#docs>

## frp

Ein schneller Reverse-Proxy, der Ihnen hilft, einen lokalen Server hinter einem NAT oder einer Firewall dem Internet auszusetzen. Es unterstützt mehr Protokolle und nennt nur einige: TCP, UDP, HTTP(S) und auch den P2P-Verbindungsmodus.

=== "Zugriff auf Webdienste"

    Abgesehen von Proxys hat frp auch ein paar Dashboards, die Sie verwenden k&ouml;nnen, um es zu überwachen.

    - Admin-UI (Client): `http://<your.IP>:7400`
    - Dashboard (Server): `http://<your.IP>:7500`
        - Benutzername: `admin`.
        - Passwort: `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfigurationsdateien"

    Je nachdem, ob Sie als Client, Server oder beides installiert haben, gibt es nur die Konfigurationsdateien für diese Komponente.

    - Client: `/etc/frp/frpc.ini`
    - Server: `/etc/frp/frps.ini`

    Hinweis: Sie ben&ouml;tigen Root-Zugriff, um diese Dateien zu bearbeiten. Sie k&ouml;nnen die _client_-Konfigurationsdatei auch über die Admin-Benutzeroberfläche bearbeiten.

***

Offizielle Dokumentation: <https://github.com/fatedier/frp/blob/dev/README.md>
Quellcode: <https://github.com/fatedier/frp>

[Zurück zur **Liste der optimierten Software**](../../software/)
