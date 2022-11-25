# Remotedesktopzugriff

Führen Sie eine **Desktop-Umgebung** auf Ihrem Gerät aus und greifen Sie remote über das Netzwerk darauf zu. Es ist eine großartige Option für Headless-SBC-Geräte.

## Überblick

### Remotedesktop

- [**TigerVNC Server - Desktop für Remoteverbindung**](#tigervnc-server)
- [**RealVNC Server - Desktop für Remote-Verbindung**](#realvnc-server)
- [**XRDP - Remotedesktopserver für Windows-Remotedesktopclient**](#xrdp)
- [**NoMachine - Remote-Desktop-Verbindung mit vielen Funktionen**](#nomachine)

### Fernzugriff

- [**Remot3.it - (Weaved) Greifen Sie über das Internet auf Ihr Gerät zu**](#remot3it)
- [**VirtualHere - Teilen Sie physisch angeschlossene USB-Geräte von Ihrem SBC über das Netzwerk**](#virtualhere)

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschließend „Installieren“.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

!!! info Desktop-Umgebung

    Wählen Sie aus der Liste **Browse Software** zusammen mit einer beliebigen Remote Desktop Software auch eine der [_Graphical Desktop Environment_](../desktop/) aus. DietPi installiert beide, sodass Sie Ihre Tastatur und Maus verwenden können, um mit einer grafischen Desktop-Umgebung auf Ihrem Gerät zu interagieren.

[Zurück zur **Liste der optimierten Software**](../../software/)

## TigerVNC-Server

![TigerVNC-Desktop-Screenshot](../assets/images/dietpi-software-remote-desktop-tigervnc.jpg){: width="600" height="482" loading="lazy"}

=== "Schnellstart"

    Sie können den VNC-Dienst überwachen mit:

    ```sh
    systemctl status vncserver
    ```

    Obwohl jeder VNC-Viewer funktionieren kann, kann der neueste offizielle TigerVNC-Viewer hier heruntergeladen werden: <https://sourceforge.net/projects/tigervnc/files/stable/>

    #### Verbindungsdetails

    - Verwenden Sie die IP-Adresse Ihres DietPi-Geräts, zB: „192.168.0.100“.
      Wenn Sie keine Verbindung herstellen können, versuchen Sie, eine Verbindung zu Bildschirm „1“ herzustellen, z. B.: „192.168.0.100:1“.
    - Verwenden Sie das Passwort, das Sie während der Installation eingegeben haben. Wenn Sie das Passwort ändern möchten, führen Sie es von der Konsole/dem Terminal aus, führen Sie `vncpasswd` aus.
    - Der Standardport ist **5901**.
      **Hinweis:** Um den Zugriff von außerhalb Ihres lokalen Netzwerks zu ermöglichen, muss dieser Port von Ihrem Router weitergeleitet werden.

=== "Konfigurationsoptionen"

    #### Freigegebener Desktop

    Der Modus *Shared Desktop* wird verwendet, um mehr als einen einzelnen VNC-Viewer mit derselben Desktop-Sitzung zu verbinden. Um diesen Modus zu aktivieren, bearbeiten Sie `/boot/dietpi.txt`, zB über `nano /boot/dietpi.txt`.
    Ändern Sie die folgende Zeile auf den Wert "1":

    ```sh
    SOFTWARE_VNCSERVER_SHARE_DESKTOP=1
    ```

    Für diesen Modus ist ein laufender Desktop erforderlich, aktivieren Sie daher den Desktop-Autostart über `dietpi-autostart 2` oder stellen Sie sicher, dass eine lokale Desktop-Sitzung aktiv ist, bevor Sie TigerVNC manuell starten.

    #### Auflösungseinstellungen

    Im Folgenden sehen Sie ein Beispiel, wie Sie den VNC-Server auf dem Bildschirm **:1** ausführen, indem Sie einen neuen Desktop mit einer Auflösung von 1280 x 720 erstellen, indem Sie „/boot/dietpi.txt“ bearbeiten:

    ```sh
    nano /boot/dietpi.txt
    ```

und ändern Sie die folgenden Einstellungen:

    ```sh
    SOFTWARE_VNCSERVER_WIDTH=1280
    SOFTWARE_VNCSERVER_HEIGHT=720
    SOFTWARE_VNCSERVER_DEPTH=32
    SOFTWARE_VNCSERVER_DISPLAY_INDEX=1
    ```

    Starten Sie zuletzt den Dienst neu, um die neuen Einstellungen zu aktivieren:

    ```sh
    systemctl restart vncserver
    ```

=== "Autostart"

    TigerVNC ist standardmäßig aktiviert, um beim Booten automatisch zu starten. Führen Sie „systemctl disable vncserver“ aus, um dieses Verhalten zu deaktivieren, und „systemctl start vncserver“, um es manuell von der Konsole aus zu starten.

    Um den Autostart von TigerVNC wieder zu aktivieren, führen Sie „systemctl enable vncserver“ aus, um ihn manuell zu stoppen, kann „systemctl stop vncserver“ verwendet werden.

***

Siehe auch <https://tigervnc.org>
Manpage: <https://tigervnc.org/doc/Xvnc.html>
Quellcode: <https://github.com/TigerVNC/tigervnc>

## RealVNC-Server

RealVNC besteht aus dem *VNC-Server* und der Anwendung *VNC Viewer*, um den Desktop freizugeben oder den Computer zu steuern, auf dem der VNC-Server läuft.

![RealVNC-Desktop-Screenshot](../assets/images/dietpi-software-remotedesktop-realvnc.png){: width="600" height="450" loading="lazy"}

=== "VNC-Server-Modi"

    #### Grundlagen

    Standardmäßig startet DietPi eine virtuelle VNC-Sitzung beim Booten auf Bildschirm **:1** für Benutzer **root**.
    Der Bildschirmindex kann über `SOFTWARE_VNCSERVER_DISPLAY_INDEX` in `/boot/dietpi.txt` geändert werden.
    Protokolle können über `journalctl -t Xvnc:1 -t vncserver` und in `/root/.vnc/` eingesehen werden.
    Wenn Sie sich abmelden (anstatt nur das VNC Viewer-Fenster zu schließen), wird die Sitzung beendet. Starten Sie es über `systemctl restart vncserver` neu.

    #### Freigegebener Desktop

    Wenn Sie `SOFTWARE_VNCSERVER_SHARE_DESKTOP=1` in `/boot/dietpi.txt` setzen oder die automatische Desktop-Anmeldung über `dietpi-autostart` (Index 2) auswählen, wird der RealVNC-Server beim Booten im Shared-Desktop-Modus gestartet und an den zuerst gefundenen angehängt lokale Desktop-Sitzung.
    Überprüfen Sie den Dienststatus über `systemctl status vncserver-x11-serviced`.
    Überprüfen Sie alle Protokolle über `journalctl -u vncserver-x11-serviced`.

    #### RealVNC-Unternehmensabonnement

    Wenn Sie ein Unternehmensabonnement für RealVNC haben, können Sie virtuelle VNC-Sitzungen automatisch bei Bedarf pro Clientverbindung starten und schließen, sobald der Client die Verbindung trennt. Auf diese Weise muss keine ressourcenintensive X11/Desktop-Sitzung dauerhaft auf dem Server aktiv sein, um VNC-Verbindungen zu ermöglichen.
    Um dies zu aktivieren, gehen Sie nach dem Hinzufügen Ihrer Enterprise-Abonnement-Anmeldeinformationen wie folgt vor:

    - `systemctl disable --now vncserver` deaktiviert die dauerhafte virtuelle VNC-Sitzung auf dem Bildschirm **:1**.
    - `systemctl enable --now vncserver-virtuald` aktiviert den On-Demand-VNC-Sitzungs-Daemon.

=== "VNC Viewer einrichten"

    Wählen Sie einfach einen VNC-Viewer für Ihr System aus und laden Sie ihn herunter: <https://www.realvnc.com/connect/download/viewer/>

    #### Verbindungsdetails

    - Um sich mit der permanenten VNC-Sitzung auf Bildschirm :1 zu verbinden, fügen Sie den Bildschirmindex zu Ihrer lokalen IP oder Ihrem Hostnamen hinzu, z. B. „192.168.0.100:1“.
    - Um eine Verbindung zu einer freigegebenen Desktopsitzung herzustellen, überspringen Sie den Bildschirmindex, z. B. „192.168.0.100“.
    - Benutzername = `root`
    - Passwort = `<root-Passwort>` (Standard: `dietpi`)

=== "Direkt gerenderte Apps ausführen"

    Dies kann zB der Fall sein, wenn Sie Minecraft remote ausführen möchten.

    - Shared-Desktop-Modus aktivieren:
        - Führen Sie „dietpi-autostart 2“ aus, um automatisch in eine Desktop-Sitzung zu starten und RealVNC automatisch daran anzuhängen.
        - Starten Sie dann das System neu, damit die Änderungen wirksam werden.
    - Befolgen Sie die Anweisungen im Abschnitt *Direkt gerenderte Apps wie Minecraft remote ausführen* in <https://help.realvnc.com/hc/en-us/articles/360002249917-VNC-Connect-and-Raspberry-Pi>.

## XRDP

XRDP ist eine Remote-Desktop-Anwendung, die den *Windows Remote Desktop Client* verwendet.

![XRDP-Desktop-Screenshot](../assets/images/dietpi-software-remotedesktop-xrdp.png){: width="648" height="507" loading="lazy"}

=== "Mit Ihrem Desktop verbinden"

    Um eine Verbindung zum Desktop herzustellen, öffnen Sie die Remote-Desktop-Anwendung in Windows (oder einem anderen XRDP-kompatiblen Client).
    Geben Sie die IP-Adresse Ihres DietPi-Geräts ein, zB „192.168.0.100“.
    Klicken Sie auf Verbinden und geben Sie die folgenden Details ein, sobald die Verbindung hergestellt ist:

    - Modul = `Xorg`
    - Benutzername = `root`
    - Passwort = `dietpi`

=== "Zugriff von außerhalb Ihres lokalen Netzwerks"

    XRDP verwendet standardmäßig Port **3389**, daher müssen Sie ihn von Ihrem Router zu DietPi öffnen/weiterleiten.

## NoMachine

    NoMachine ist ein Remote-Desktop-Server mit erweiterten Funktionen wie Bildschirmaufzeichnung. Der Client scannt auch nach allen verfügbaren NoMachine-Servern in Ihrem Netzwerk, was eine einfache Verbindung und Wartung Ihrer Remote-Desktops ermöglicht.

![NoMachine-Client- und Desktop-Screenshot](../assets/images/dietpi-software-remotedesktop-nomachine.png){: width="600" height="299" loading="lazy"}

=== "NoMachine-Client herunterladen"

    Laden Sie die *NoMachine*-Client-Software herunter von:

    - URL = <https://www.nomachine.com>

=== "Mit DietPi verbinden"

    Sobald der NoMachine-Client installiert ist und auf Ihrem System läuft, sollten Sie ein Gerät namens *DietPi* sehen. Führen Sie die folgenden Schritte aus:

    1. Doppelklicken Sie darauf.
    2. Wählen Sie „Ja“ für *Remote-Host-Identifikation hat sich geändert*.
    3. Wählen Sie „Ja“ für *Hostauthentizität prüfen*.
    4. Geben Sie den Benutzernamen „root“ und das Passwort „dietpi“ ein.
    5. Wählen Sie „Ja“ für *Möchten Sie, dass NoMachine eine neue Anzeige erstellt*.

    Sie werden nun mit Ihrem Gerät verbunden.

##Remot3.it

Remot3.it ermöglicht Ihnen den einfachen Zugriff auf Ihr DietPi-Gerät über das Internet.

![Screenshot der Remot3.it-Weboberfläche](../assets/images/dietpi-software-remotedesktop-remot3it.png){: width="400" height="140" loading="lazy"}

Remot3.it verbindet Sie mit einem bestimmten TCP-Port auf Ihrem Gerät, die alle während der Ersteinrichtung angepasst werden können.

Beispiele für TCP-Ports für Remot3.it:

- SSH-Port **22**. Öffnen Sie ein Remote-Terminal für Ihr Gerät.
- Übertragungsport **9091**. Überwachen Sie Ihre BitTorrent-Downloads.
- Webserver-Port **80**. Greifen Sie auf Ihre internen Websites zu.

=== "Erstlauf-Setup"

Bei interaktiven Installationen ruft `dietpi-software` das Setup-Skript auf, um Ihre Anwendungsverbindungen einzurichten und zu verwalten. Bei unbeaufsichtigten Installationen, z. B. über `dietpi.txt`, können Sie es manuell von der Konsole aus aufrufen:

    ```sh
    connectd_installer
    ```

    Sobald Ihr Konto erstellt und mit diesem System verknüpft ist, können Sie einen Port für Remot3.it auswählen, um den Fernzugriff zu ermöglichen.

=== "Greifen Sie auf Ihr Gerät zu"

    Melden Sie sich bei Ihrem Remot3.it-Konto an, um remote auf Ihre Geräte zuzugreifen:

    - URL = <https://remote.it/>

***

YouTube-Video-Tutorial: `Raspberry Pi einfach fernsteuern: Remote.It SSH ohne VPN von überall - Installation unter DietPi`.

<iframe src="https://www.youtube-nocookie.com/embed/V5MZXBo3hGw?rel?=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="faul "></iframe>

## VirtualHere

Das VirtualHere-Paket wird verwendet, um physisch angeschlossene USB-Geräte von Ihrem SBC über das Netzwerk für andere Systeme freizugeben.

![VirtualHere-Client-Screenshot](../assets/images/dietpi-software-remotedesktop-virtualhere.png){: width="400" height="252" loading="lazy"}

Laden Sie den Client für Ihren PC herunter von:

- <https://www.virtualhere.com/usb_client_software>

Nach der Installation werden verfügbare VirtualHere-Geräte in der Client-Benutzeroberfläche angezeigt und können auf dem Client-PC verwendet werden.

!!! Warnung „USB-Speicher WARNUNG“
    - Gemäß <https://github.com/MichaIng/DietPi/issues/852#issuecomment-292781475> wird dringend empfohlen, VirtualHere nicht zu installieren, wenn Ihre DietPi-Benutzerdaten auf einem USB-Laufwerk gespeichert sind.
    - VirtualHere berücksichtigt keine eingebundenen Laufwerke bei der Auswahl für die Remote-Nutzung. Dies ist potenziell gefährlich für alle bereitgestellten Laufwerke, die verwendet werden, und kann zu Datenverlust führen.
    - Verwenden Sie auf dem Client keine Laufwerke, die auf dem SBC gemountet sind.
      Unmounten Sie das Laufwerk vorher in `dietpi-drive_manager`.

[Zurück zur **Liste der optimierten Software**](../../software/)
