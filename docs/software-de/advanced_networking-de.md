# Erweitertes Netzwerk

## &Uuml;berblick

- [**WiFi HotSpot - Verwandeln Sie Ihr Ger&auml;t in einen drahtlosen Hotspot/Zugangspunkt**](#wifi-hotspot)
- [**Tor HotSpot - Optional: Leitet den gesamten WLAN-HotSpot-Verkehr durch das Tor-Netzwerk**](#tor-hotspot)
- [**HAProxy - Hochleistungs-TCP/HTTP-Load-Balancer**](#haproxy)
- [**frp - Reverse-Proxy**](#frp)

??? info "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
Um eines der unten aufgef&uuml;hrten **DietPi-optimierten Softwareelemente** zu installieren, f&uuml;hren Sie es &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software durchsuchen** und w&auml;hlen Sie einen oder mehrere Artikel aus. W&auml;hlen Sie abschlie&szlig;end `Installieren`.
    DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

## WLAN-HotSpot

Das WiFi-HotSpot-Paket verwandelt Ihr Ger&auml;t in einen drahtlosen Hotspot/Zugangspunkt. Dadurch k&ouml;nnen andere drahtlose Ger&auml;te eine Verbindung herstellen und die Internetverbindung teilen.

![DietPi WLAN-Hotspot WLAN](../assets/images/dietpi-software-advanced-networking-wifihotspot.png){: width="550" height="345" loading="lazy"}

=== "Anforderungen"

    Die Anforderungen sind:

    - 1x Ethernet-Verbindung
    - 1x unterst&uuml;tzter USB-WLAN-Adapter oder integriertes WLAN. Dies kann je nach Ger&auml;t und verf&uuml;gbaren WLAN-Treibern/Modulen variieren. G&auml;ngige Adapter (z. B. Atheros) sollten jedoch in Ordnung sein.

=== "Erste Verbindungsdaten"

    Verwenden Sie die folgenden Anmeldeinformationen, um Ger&auml;te anf&auml;nglich mit Ihrem Hotspot zu verbinden.

- SSID = `DietPi-HotSpot`
- Zugangsschl&uuml;ssel = `dietpihotspot`

=== "WLAN-HotSpot-Einstellungen &auml;ndern"

    Nach der Installation k&ouml;nnen Sie die WLAN-HotSpot-Einstellungen (SSID/Schl&uuml;ssel/Kanal) jederzeit &auml;ndern:

    1. F&uuml;hren Sie `dietpi-config` aus
    2. Navigieren Sie zu *Netzwerkoptionen: Adapter* und w&auml;hlen Sie dann *WiFi*
    3. Es wird dringend empfohlen, in diesem Men&uuml; den L&auml;ndercode auf Ihr Land einzustellen. Abh&auml;ngig von den Vorschriften Ihres Landes k&ouml;nnte dies die Kan&auml;le 12/13 und eine erh&ouml;hte Ausgangsleistung (Reichweite) f&uuml;r den Hotspot erm&ouml;glichen

***

YouTube-Video-Tutorial: `Raspberry Hotspot: Internet Sperren umgehen mit eigenem WiFi Hotspot unter DietPi (f&uuml;r alle Ger&auml;te)`.

<iframe src="https://www.youtube-nocookie.com/embed/3ZROq90tM_s?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

## Tor-HotSpot

Das Tor-HotSpot-Paket verwandelt Ihr Ger&auml;t in einen WLAN-HotSpot/Access Point mit Tor-Routing. Der gesamte WiFi-HotSpot-Datenverkehr f&uuml;r alle verbundenen WiFi-Ger&auml;te wird durch das Tor-Netzwerk geleitet.
Dies ist perfekt f&uuml;r Benutzer, die Anonymit&auml;t und Privatsph&auml;re ben&ouml;tigen.

Es installiert auch:

    - [WLAN-HotSpot](#wifi-hotspot_1)

![DietPi WLAN-Hotspot-Tor](../assets/images/dietpi-software-advanced-networking-torhotspot.png){: width="550" height="308" loading="lazy"}

=== "Anforderungen"

    Die Anforderungen sind:

    - 1x Ethernet-Verbindung
    - 1x unterst&uuml;tzter USB-WLAN-Adapter oder integriertes WLAN. Dies kann je nach Ger&auml;t und verf&uuml;gbaren WLAN-Treibern/Modulen variieren. G&auml;ngige Adapter (z. B. Atheros) sollten jedoch in Ordnung sein.

=== "Verbindungsdaten"

    Diese sind identisch mit den [WiFi-HotSpot-Anmeldedaten](#wifi-hotspot_1).

=== "Verifizierung"

    Um zu &uuml;berpr&uuml;fen, ob der Datenverkehr durch Tor geleitet wird, k&ouml;nnen Sie Folgendes &uuml;berpr&uuml;fen:
    Rufen Sie auf dem verbundenen WLAN-Ger&auml;t die folgende URL auf: <https://check.torproject.org>

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

HAProxy steht f&uuml;r High Availability Proxy und ist eine beliebte Open-Source-Software f&uuml;r TCP/HTTP Load Balancer und Proxy-L&ouml;sung. Seine h&auml;ufigste Verwendung besteht darin, die Leistung und Zuverl&auml;ssigkeit einer Serverumgebung zu verbessern, indem die Arbeitslast auf mehrere Server (z. B. Web, Anwendung, Datenbank) verteilt wird.

Es eignet sich am besten f&uuml;r stark frequentierte Websites und betreibt eine ganze Reihe der meistbesuchten der Welt: GitHub, Imgur, Instagram und Twitter. Es ist zum De-facto-Standard-Open-Source-Load-Balancer geworden und wird h&auml;ufig standardm&auml;&szlig;ig auf Cloud-Plattformen bereitgestellt.

![HAProxy-Statistik-Webseite](../assets/images/dietpi-software-advanced-networking-haproxy2.jpg){: width="1898" height="650" loading="lazy"}

!!! Warnung "Dieser Softwaretitel wird NUR f&uuml;r fortgeschrittene Benutzer empfohlen!"

=== "Schnellstart"

    Nach der Installation m&uuml;ssen Sie die `haproxy.cfg` manuell &auml;ndern, damit sie Ihren Netzwerkanforderungen am besten entspricht. &Uuml;berpr&uuml;fen Sie das Konfigurationshandbuch [hier](https://www.haproxy.org/#docs).

    ```sh
    systemctl stop haproxy
    nano /etc/haproxy/haproxy.cfg
    systemctl start haproxy    
    ```

    Das Statistik-Webinterface ist &uuml;ber Port **1338** erreichbar:

    - URL = `http://<Ihre.IP>:1338`
    - Benutzername = `admin`
    - Passwort = `dietpi`

    !!! Hinweis "Diese Installation wurde von Jerome Queneuder erm&ouml;glicht, der die Methoden zum Kompilieren und Installieren bereitstellte."

=== "Lastverteilung"

    Die einfachste M&ouml;glichkeit, den Netzwerkverkehr auf mehrere Server auszugleichen, ist die Verwendung von Layer 4 (Transport Layer) Load Balancing. Der Lastausgleich auf diese Weise leitet den Benutzerdatenverkehr basierend auf dem IP-Bereich und dem Port weiter.

    ![Layer-4-Load-Balancing-Piktogramm](../assets/images/dietpi-software-advanced-networking-layer4.jpg){: width="690" height="248" loading="lazy"}

    Der Benutzer greift auf den Load Balancer zu, der die Anfrage des Benutzers an die Web-Backend-Gruppe von Backend-Servern weiterleitet. Welcher Backend-Server auch immer ausgew&auml;hlt wird, antwortet direkt auf die Anfrage des Benutzers.

    Aus dem Tutorial extrahierter Hilfetext: [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)

=== "Hohe Verf&uuml;gbarkeit"

    Ein Hochverf&uuml;gbarkeits-Setup (HA) ist eine Infrastruktur ohne Single Point of Failure. Es verhindert, dass ein Ausfall eines einzelnen Servers zu einem Ausfallereignis wird, indem jeder Ebene Ihrer Architektur Redundanz hinzugef&uuml;gt wird. Ein Load Balancer erleichtert die Redundanz f&uuml;r die Backend-Schicht (Web-/App-Server), aber f&uuml;r eine echte Einrichtung mit hoher Verf&uuml;gbarkeit ben&ouml;tigen Sie auch redundante Load Balancer.

    Hier ist ein Diagramm einer grundlegenden Einrichtung f&uuml;r hohe Verf&uuml;gbarkeit:
    ![Animiertes Hochverf&uuml;gbarkeits-Setup-Diagramm](../assets/images/dietpi-software-advanced-networking-high-availability.gif){: width="1200" height="577" loading="lazy"}

    Aus dem Tutorial extrahierter Hilfetext: [An Introduction to HAProxy and Load Balancing Concepts](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)

***

Website: <https://www.haproxy.org/>
Offizielle Dokumentation: <https://www.haproxy.org/#docs>

## frp

Ein schneller Reverse-Proxy, der Ihnen hilft, einen lokalen Server hinter einem NAT oder einer Firewall dem Internet auszusetzen. Es unterst&uuml;tzt mehr Protokolle und nennt nur einige: TCP, UDP, HTTP(S) und auch den P2P-Verbindungsmodus.

=== "Zugriff auf Webdienste"

    Abgesehen von Proxys hat frp auch ein paar Dashboards, die Sie verwenden k&ouml;nnen, um es zu &uuml;berwachen.

    - Admin-UI (Client): `http://<your.IP>:7400`
    - Dashboard (Server): `http://<your.IP>:7500`
        - Benutzername: `admin`.
        - Passwort: `<yourGlobalSoftwarePassword>` (Standard: `dietpi`)

=== "Konfigurationsdateien"

    Je nachdem, ob Sie als Client, Server oder beides installiert haben, gibt es nur die Konfigurationsdateien f&uuml;r diese Komponente.

    - Client: `/etc/frp/frpc.ini`
    - Server: `/etc/frp/frps.ini`

    Hinweis: Sie ben&ouml;tigen Root-Zugriff, um diese Dateien zu bearbeiten. Sie k&ouml;nnen die _client_-Konfigurationsdatei auch &uuml;ber die Admin-Benutzeroberfl&auml;che bearbeiten.

***

Offizielle Dokumentation: <https://github.com/fatedier/frp/blob/dev/README.md>
Quellcode: <https://github.com/fatedier/frp>

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
