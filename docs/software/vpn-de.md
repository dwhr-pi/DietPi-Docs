# VPN

## Ü;berblick

- [**OpenVPN - Einfach zu verwendender VPN-Server mit minimalem Aufwand**](#openvpn)
- [**PiVPN - OpenVPN-Serverinstallations- und Verwaltungstool**](#pivpn)
- [**WireGuard - Ein extrem einfaches, aber schnelles und modernes VPN**](#wireguard)

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschlie&szlig;end `Installieren`.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## OpenVPN

Ein einfach zu bedienendes VPN-Server- und Client-System. Die DietPi-Installation von OpenVPN verwendet eine einzige Client-Datei, um Sie mit minimalem Aufwand zu verbinden.

![OpenVPN-Logo](../assets/images/dietpi-software-vpn-openvpn-logo.png){: width="200" height="58" loading="lazy"}

=== "Client-Verbindungsdatei"

    #### Generieren Sie eine Client-Verbindungsdatei für Ihr VPN-Client-System

    Als Voraussetzung muss eine Client-Verbindungsdatei (`DietPi_OpenVPN_Client.ovpn`) beschafft und auf Ihrem Zielsystem abgelegt werden, auf dem Ihr VPN-Client läuft.
    DietPi generiert während der Installation automatisch eindeutige 2048-Bit-Server- und Client-Schlüssel und platziert sie in einer einheitlichen Client-Konfigurationsdatei. Sie ben&ouml;tigen diese Datei, um sich von einem Client mit Ihrem OpenVPN-Server zu verbinden.

    Speicherort der Clientdatei:

    - DietPi generiert die Client-Konfigurationsdatei und legt sie hier ab:
      `/boot/DietPi_OpenVPN_Client.ovpn`.
      Schalten Sie einfach die SD-Karte aus und stecken Sie sie in Ihr Zielsystem, um die Datei von der FAT-Partition zu erhalten.
    - DietPi erstellt auch eine Kopie der Datei in
      `/mnt/dietpi_userdata/DietPi_OpenVPN_Client.ovpn`.
      Verwenden Sie einen der Dateiserver von DietPi, um auf diese Datei zuzugreifen.

    ???+ Warnung `Sicherheitsproblem`
        Bitte entfernen Sie aus Sicherheitsgründen diese Client-Verbindungsdateien, nachdem sie auf dem Client-System bereitgestellt wurden!

    #### Änderung der Zieladresse für die Mandantendatei

    Sie müssen die Datei `DietPi_OpenVPN_Client.ovpn` in einem Texteditor &ouml;ffnen, um die Zieldomäne/IP-Adresse zu ändern. Dies kann alles sein, von einer Website-Adresse, einem No-IP-Domänennamen oder einer IP-Adresse.
    Beispiele zum Ändern von `mywebsite.com`. z.B:

    - `remote MySuperDooperWebsite.com 1194`
    - `remote 81.252.0.1 1194`

=== "Router-Setup"

    Sie müssen Ihren Router einrichten, um den externen Zugriff zu erm&ouml;glichen.
    Der OpenVPN-Server verwendet die folgenden Ports:

    -TCP 443
    -TCP 943
    - UDP-1194

    Diese Ports müssen alle in der Portweiterleitung auf Ihrem Router aktiviert sein und auf die IP-Adresse Ihres DietPi-Systems zeigen.

=== "Windows-Client"

    Die Installation des Windows OpenVPN-Clientprogramms erfolgt mit den folgenden Schritten:

    1. Laden Sie die Software unter herunter
      URL = <https://openvpn.net/community-downloads/>
    2. Laden Sie das Installationsprogramm herunter und installieren Sie es, das zu Ihrer Windows-Version passt.

=== "Verbinden mit Ihrem OpenVPN-Server (Windows)"

    Methode 1 - Schnell:
    Klicken Sie einfach mit der rechten Maustaste auf die Datei `DietPi_OpenVPN_Client.ovpn` und wählen Sie `OpenVPN in dieser Konfigurationsdatei starten`.

    Methode 2 - GUI:
    Wenn Sie die OpenVPN-GUI verwenden m&ouml;chten, müssen Sie `DietPi_OpenVPN_Client.ovpn` in den OpenVPN-Konfigurationsspeicherort kopieren (z. B.: `C:\Programme\OpenVPN\config`).

=== "OpenVPN + Pi-Hole"

    Damit VPN-Clients auf Ihre lokale Pi-hole-Instanz zugreifen k&ouml;nnen, müssen Sie DNS-Anfragen von allen Netzwerkschnittstellen zulassen:
    `pihole -a -i lokal`

***

Webseite: <https://openvpn.net>
Wikipedia: <https://wikipedia.org/wiki/OpenVPN>
Installationsartikel: [PiVPN: Raspberry Pi mit OpenVPN – Raspberry Pi Teil3](https://www.kuketz-blog.de/pivpn-raspberry-pi-mit-openvpn-raspberry-pi-teil3/){ :class="nospellcheck"}

## PiVPN

PiVPN ist ein Installations- und Verwaltungstool für OpenVPN und WireGuard. Es hat auch einen Befehl "pivpn", der eine einfache Erstellung zusätzlicher Benutzerprofile und -konfigurationen erm&ouml;glicht.

![PiVPN-Logo](../assets/images/dietpi-software-vpn-pivpn-logo.png){: width="100" height="100" loading="lazy"}

=== `Mit PiVPN`

    Führen Sie den Befehl `pivpn` aus, um eine Liste der Optionen anzuzeigen.

=== "Neues Benutzerprofil erstellen"

    Führen Sie einfach den Befehl `pivpn -a` aus.

***

Website: <https://www.pivpn.io>

YouTube-Video-Tutorial: *VPN-Konfiguration mit Raspberry Pi und DietPi*.

<iframe src="https://www.youtube-nocookie.com/embed/aYPaDeqtMG8?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

YouTube-Video-Tutorial: *DietPi PiVPN-Server-Setup auf Raspberry Pi 3 B Plus*.

<iframe src="https://www.youtube-nocookie.com/embed/0t0bwskZJFw?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

## WireGuard

WireGuard ist ein extrem einfaches, aber schnelles und modernes VPN, das modernste Kryptografie verwendet. Es zielt darauf ab, schneller, einfacher, schlanker und nützlicher als IPsec zu sein und gleichzeitig die massiven Kopfschmerzen zu vermeiden.

![WireGuard-Logo](../assets/images/dietpi-software-vpn-wireguard.svg){: width="300" height="53" loading="lazy"}

Bei der Installation mit `dietpi-software` k&ouml;nnen Sie wählen, ob Sie WireGuard als VPN-Server oder Client installieren m&ouml;chten.

=== "Als VPN-Server installieren"

    #### Allgemein

    Sie werden aufgefordert, Ihre &ouml;ffentliche IP/Domäne und den Port einzugeben, auf dem der VPN-Server erreichbar sein soll. Denken Sie daran, den Port (UDP) über NAT auf Ihrem Router zu &ouml;ffnen/weiterzuleiten.
    Während der Installation wird automatisch auch eine Client-Konfigurationsdatei erstellt unter:
    `/etc/wireguard/wg0-client.conf`.

    Konfigurieren Sie die Client-Konfiguration nach Ihren Bedürfnissen, sie enthält einige informative Kommentare. Standardmä&szlig;ig wird der gesamte Client-Netzwerkverkehr durch den VPN-Tunnel geleitet, einschlie&szlig;lich DNS-Anforderungen, die vom DNS-Resolver des Servers aufgel&ouml;st werden.
    Wenn Sie beispielsweise die Server-Pi-Hole-Instanz nur auf dem Client verwenden m&ouml;chten, aber den gesamten anderen Datenverkehr au&szlig;erhalb des VPN-Tunnels halten m&ouml;chten, würden Sie die folgenden Werte bearbeiten:

    - `DNS = 192.168.0.100`.
    - `AllowedIPs = 192.168.0.100/32` (wobei die IP mit der lokalen IP Ihres DietPi-Servers übereinstimmen muss)

    Wenn Ihr Client ein anderer Linux-Computer ist, auf dem iptables installiert ist, k&ouml;nnen Sie die beiden Kill-Switch-Zeilen auskommentieren, damit der gesamte Netzwerkverkehr automatisch deaktiviert wird, wenn die VPN-Verbindung unterbrochen wird.
    Wenn Ihr Client ein Mobiltelefon mit installierter WireGuard-App ist, k&ouml;nnen Sie die Konfiguration einfach anwenden, indem Sie einen QR-Code auf das Serverterminal drucken über:
    `grep -v '^#' /etc/wireguard/wg0-client.conf | qrencode -t ansiutf8`.
    Damit VPN-Clients auf Ihre lokale Pi-hole-Instanz zugreifen k&ouml;nnen, müssen Sie DNS-Anfragen von allen Netzwerkschnittstellen zulassen: `pihole -a -i local`.

    #### Hinzufügen mehrerer Clients

    Navigieren Sie zum WireGuard-Konfigurationsverzeichnis des Servers: `cd /etc/wireguard`.

    Erstellen Sie ein zweites Client-Schlüsselpaar:

    ```sh
    umask 0077
    wg genkey > client2_private.key
    wg pubkey < client2_private.key > client2_public.key
    umask 0022
    ```

    Klonen und konfigurieren Sie die Client-Konfiguration:

    ```sh
    cp -a wg0-client.conf wg0-client2.conf
    G_CONFIG_INJECT 'Address = ' 'Address = 10.9.0.3/24' wg0-client2.conf
    G_CONFIG_INJECT 'PrivateKey = ' "PrivateKey = $(<client2_private.key)" wg0-client2.conf
    ```

    Konfigurieren Sie `wg0.conf` (Serverkonfiguration) so, dass die letzten Zeilen übereinstimmen:

    ```
    [Peer]
    PublicKey = <paste content of client2_public.key here>
    AllowedIPs = 10.9.0.3/32
    ```

    Starten Sie den VPN-Server neu (`systemctl restart wg-quick@wg0`) und wenden Sie `wg0-client2.conf` auf Ihren zweiten VPN-Client an, wie Sie es zuvor für den ersten getan haben.
    Wiederholen Sie ähnliches für den dritten, vierten, ... VPN-Client.

=== "Als VPN-Client installieren"

    Normalerweise hat der VPN-Anbieter Installationsanweisungen und versendet eine Konfigurationsdatei.
    Wenn Sie sich mit einem anderen DietPi-Rechner verbinden m&ouml;chten, verwenden Sie die generierte `/etc/wireguard/wg0-client.conf` wie oben erwähnt.
    Wenn keine WireGuard (Auto-)Startanleitung enthalten ist, Sie diese aber ben&ouml;tigen, gehen Sie bitte wie folgt vor:

    - Ü;berprüfen Sie die erstellte Konfigurationsdatei/den Schnittstellennamen: `ls -Al /etc/wireguard/`
    - Es hat eine `.conf` Dateiendung, nehmen wir an: `wg0-client.conf`
    - Führen Sie zum Starten der VPN-Schnittstelle Folgendes aus: `systemctl start wg-quick@wg0-client`
    - Um die VPN-Schnittstelle beim Booten automatisch zu starten, führen Sie Folgendes aus: `systemctl enable wg-quick@wg0-client`
    - Um den Autostart wieder zu deaktivieren, führen Sie Folgendes aus: `systemctl disable wg-quick@wg0-client`

    Anmerkung: Wenn die Client-Konfiguration den DNS-Server über die `DNS = ...`-Direktive einstellt, stellen Sie sicher, dass resolvconf installiert ist: `apt install resolvconf`.

=== "Protokolle anzeigen"

    Die Protokollierung kann angezeigt werden mit:

    ```sh
    journalctl -u wg-quick@wg0
    ```

    beziehungsweise

    ```sh
    journalctl -u wg-quick@<config_name>
    ```

???+ Information "Kernel-Update"

    Das WireGuard-Kernelmodul muss jedes Mal neu erstellt werden, wenn der Kernel aktualisiert wird. Auf den meisten Geräten geschieht dies automatisch, wenn der Kernel (+Header) über das APT-Paket aktualisiert wird, was dann normalerweise den Modulneuaufbau ausl&ouml;st.
    Wenn Sie den Kernel au&szlig;erhalb von APT über `source build` oder Befehle wie `rpi-update` aktualisieren, stellen Sie sicher, dass auch passende Kernel-Header installiert sind, und erstellen Sie das WireGuard-Modul neu über: `dpkg-reconfigure wireguard-dkms`.

***

Website: <https://www.wireguard.com>
Wikipedia: <https://wikipedia.org/wiki/WireGuard>

YouTube-Video-Tutorial: `Raspberry Pi & PiVPN mit WireGuard: Installation unter DietPi mit NoIP und AVM Fritzbox`.

<iframe src="https://www.youtube-nocookie.com/embed/yRkdzGmnvA4?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

[Zurück zur **Liste der optimierten Software**](../../software/)
