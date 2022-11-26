# Kamera & &Uuml;berwachung

## &Uuml;berblick

- [**RPi Cam Control - Webinterface & Steuerelemente f&uuml;r Ihre RPi-Kamera**](#rpi-cam-control)
- [**MotionEye - Webinterface & &Uuml;berwachung f&uuml;r Ihre Kamera**](#motioneye)
- [**mjpg-streamer - Einfaches Kamera-Streaming-Tool mit HTML-Plugin**](#mjpg-streamer)

??? Information "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef&uuml;hrten **DietPi-optimierten Softwareelemente** zu installieren, f&uuml;hren Sie es &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software durchsuchen** und w&auml;hlen Sie einen oder mehrere Artikel aus. W&auml;hlen Sie abschlie&szlig;end `Installieren`.
    DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

## RPi-Kamerasteuerung

Das Paket *RPi Cam Control* kann in Kombination mit einem Raspberry Pi Kameramodul verwendet werden

- ein Bild machen
- ein Video aufnehmen
- Beobachten basierend auf Bewegungserkennung
- Nehmen Sie ein Video mit Zeitraffer auf

Es besteht aus der vollst&auml;ndigen Steuerung der Kamera in einer webbasierten Schnittstelle.

![Screenshot der RPi Cam Control-Weboberfl&auml;che](../assets/images/dietpi-software-camera-rpicamcontrol.png){: width="500" height="395" loading="lazy"}

=== "Zugriff auf die Weboberfl&auml;che"

    Das Webinterface ist erreichbar &uuml;ber:

    - URL = `http://<your.IP>/rpicam`

=== "Zugriff auf Aufzeichnungen (ohne Webinterface)"

    Um ohne das Webinterface aus der Ferne auf Ihre Aufzeichnungen zuzugreifen, m&ouml;chten Sie vielleicht einen der [Dateiserver von DietPi](../file_servers/) installiert haben.
    Von MotionEye verwendete Verzeichnisse:

    - Medienverzeichnis = `/mnt/dietpi_userdata/rpicam`
    - Zugriff vom Dateiserver = `/rpicam`

=== "Auf neueste Version aktualisieren"

    RPi Cam Control kann auf die neueste Version aktualisiert werden, indem es &uuml;ber neu installiert wird

    ```sh
    dietpi-software reinstall 59
    ```

=== "RPi-Kameramodul"

    Das RPi-Kameramodul wird w&auml;hrend des Installationsvorgangs automatisch aktiviert. Es erfordert jedoch einen Neustart und/oder manchmal einen Power-Cycle, um wirksam zu werden.
    Die Kameraaktivierung kann &uuml;ber `dietpi-config` > `Display Options` > `RPi Camera` &uuml;berpr&uuml;ft werden, um `[On]` anzuzeigen. Zus&auml;tzlich kann im selben Dialog &uuml;ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem &Auml;ndern der Kameraaktivierung m&uuml;ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/silvanmelchior/RPi_Cam_Web_Interface>
Wiki: <https://elinux.org/RPi-Cam-Web-Interface>
Lizenz: [MIT](https://github.com/silvanmelchior/RPi_Cam_Web_Interface/blob/master/LICENSE.txt)

## MotionEye

Das Paket *MotionEye* bietet &Uuml;berwachung f&uuml;r Ihre Kamera.
Es konzentriert sich haupts&auml;chlich auf die Verwendung der Bewegungserkennung. Es enth&auml;lt ein Webinterface.

Die Software kann

- ein Bild machen
- ein Video aufnehmen
- Beobachten basierend auf Bewegungserkennung
- Nehmen Sie ein Video mit Zeitraffer auf

von jeder RPi-Kamera, USB-Kamera oder einem Netzwerkstream einer IP-Kamera.

![Screenshot der MotionEye-Weboberfl&auml;che](../assets/images/dietpi-software-camera-motioneye.png){: width="500" height="246" loading="lazy"}

=== "Zugriff auf die Weboberfl&auml;che"

    Das Webinterface ist &uuml;ber Port **8765** erreichbar:

    - URL = `http://<Ihre.IP>:8765`
    - Benutzer = `admin`.
    - Passwort = nicht erforderlich

    Passw&ouml;rter k&ouml;nnen im Webinterface konfiguriert werden.

=== "Zugriff auf Aufzeichnungen (ohne Webinterface)"

    Um ohne das Webinterface aus der Ferne auf Ihre Aufzeichnungen zuzugreifen, m&ouml;chten Sie vielleicht einen der [Dateiserver von DietPi](../file_servers/) installiert haben.
    Von MotionEye verwendete Verzeichnisse:

    - Medienverzeichnis = `/mnt/dietpi_userdata/motioneye`
    - Zugriff &uuml;ber Dateiserver = `/motioneye`

=== "Auf neueste Version aktualisieren"

MotionEye kann auf die neueste Version aktualisiert werden &uuml;ber

    ```sh
    sudo pip2 install -U motioneye
    ```

=== "RPi-Kameramodul"

    Wenn Sie ein offizielles Raspberry Pi-Kameramodul haben, kann es &uuml;ber `dietpi-config` > `Display Options` > `RPi Camera` aktiviert werden, um `[On]` anzuzeigen.
    Zus&auml;tzlich kann im selben Dialog &uuml;ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem &Auml;ndern der Kameraaktivierung m&uuml;ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/ccrisan/motioneye>
Wiki: <https://github.com/ccrisan/motioneye/wiki>
Tutorial: [MotionEye auf DietPi auf Raspberry Pi: alles im Blick behalten](https://mansfield-devine.com/speculatrix/2018/12/motioneye-on-dietpi-on-raspberry-pi/)
YouTube-Video-Tutorial: `DietPi & MotionEye - Vollautomatische Installation inkl. Wlan Konfiguration, Updates und Anwendung`.

<iframe src="https://www.youtube-nocookie.com/embed/vQxL3TfQK5E?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

Lizenz: [GPLv3](https://github.com/ccrisan/motioneye/blob/dev/LICENSE)

## mjpg-Streamer

Streamen Sie JPEG-Frames von verschiedenen Quellen zu verschiedenen m&ouml;glichen Ausg&auml;ngen. Mit der Standardeinstellung wird ein angeh&auml;ngtes Kamerabild mit dem enthaltenen HTTP-Plugin auf eine einfache Webseite gestreamt.

![mjpg-streamer HTML-Stream GIF](../assets/images/mjpg-streamer.gif){: width="500" height="400" loading="lazy"}

=== "Auf den HTTP-Stream zugreifen"

    Das Webinterface verwendet Port **8082**:

    - Stream: `http://<your.IP>:8082/?action=stream`
    - Snapshot: `http://<your.IP>:8082/?action=snapshot`
    - HTTP-Plugin-Dokumentation: <https://github.com/jacksonliam/mjpg-streamer/blob/master/mjpg-streamer-experimental/plugins/output_http/README.md>

=== "Setup f&uuml;r OctoPrint"

    Wenn [OctoPrint](../printing/#octprint) installiert wird, wird es automatisch so konfiguriert, dass es den mjpg-streamer-HTTP-Stream und Snapshots verwendet, da dies der Hauptanwendungsfall ist, f&uuml;r den dieser Softwaretitel angefordert wurde. Sie k&ouml;nnen die Einrichtung in den Einstellungen der OctoPrint-Weboberfl&auml;che &uuml;berpr&uuml;fen und testen.

=== "HTML-Authentifizierung"

    Standardm&auml;&szlig;ig ist der HTTP-Stream auf Port **8082** ohne Authentifizierung zug&auml;nglich. Dies ist erforderlich, wenn Sie es in [OctoPrint](../printing/#octprint) einbetten, da der Browser die Anfrage sendet und derzeit keine Anmeldeinformationen weitergeben kann. Wenn Sie den Stream jedoch anderweitig verwenden, insbesondere wenn Sie ihn dem World-Wide-Web zur Verf&uuml;gung stellen, empfehlen wir, ein Passwort einzurichten. Daf&uuml;r:

    1. F&uuml;hren Sie `dietpi-services` aus
    2. W&auml;hlen Sie `mjpg-Streamer` aus
    3. W&auml;hlen Sie `Bearbeiten`, um eine Service-Override-Konfiguration mit dem `nano`-Befehlszeileneditor zu &ouml;ffnen.
    4. Entkommentieren Sie im Abschnitt `[Service]` die Zeile `ExecStart=` und f&uuml;gen Sie ` -c username:password` zum letzten Block mit einfachen Anf&uuml;hrungszeichen `''` hinzu, mit Benutzername und Passwort Ihrer Wahl.
    5. Oberhalb dieser Zeile m&uuml;ssen Sie ein weiteres `ExecStart=` ohne Inhalt hinzuf&uuml;gen, das den urspr&uuml;nglichen Startbefehl entfernen soll, damit Ihr ihn effektiv ersetzt. Die Datei k&ouml;nnte schlie&szlig;lich so aussehen:

        ```systemd
        [Unit]
        #Description=mjpg-streamer (DietPi)
        #Documentation=https://github.com/jacksonliam/mjpg-streamer/tree/master/mjpg-streamer-experimental
        #Wants=network-online.target
        #After=network-online.target dietpi-boot.service

        [Service]
        #User=mjpg-streamer
        #WorkingDirectory=/opt/mjpg-streamer
        ExecStart=
        ExecStart=/opt/mjpg-streamer/mjpg_streamer -i 'input_uvc.so -d /dev/video0' -o 'output_http.so -p 8082 -n -c micha:youNeverGuessThis!'

        # Hardening
        #ProtectSystem=strict
        #PrivateTmp=true
        #ProtectHome=true
        #ProtectKernelTunables=true
        #ProtectControlGroups=true

        [Install]
        #WantedBy=multi-user.target
        ```

    6. Dr&uuml;cken Sie ++ctrl+o++, um die Datei zu speichern und ++ctrl+x++, um den Editor zu verlassen. Beim Beenden von `dietpi-services` wird der Dienst automatisch neu geladen und ist fortan passwortgesch&uuml;tzt.

=== "Auf neueste Version aktualisieren"

    mjpg-streamer kann auf die neueste Version aktualisiert werden, indem Sie ihn &uuml;ber neu installieren

    ```sh
    dietpi-software reinstall 137
    ```

=== "Protokollierung"

    Sie k&ouml;nnen die Dienstprotokolle &uuml;ber anzeigen

    ```sh
    journalctl -u mjpg-streamer
    ```

    und der Dienststatus &uuml;ber

    ```sh
    systemctl status mjpg-streamer
    ```

=== "RPi-Kameramodul"

    Wenn Sie ein offizielles Raspberry Pi-Kameramodul haben, kann es &uuml;ber `dietpi-config` > `Display Options` > `RPi Camera` aktiviert werden, um `[On]` anzuzeigen.
    Zus&auml;tzlich kann im selben Dialog &uuml;ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem &Auml;ndern der Kameraaktivierung m&uuml;ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/jacksonliam/mjpg-streamer>
Plugin-Dokumentation: <https://github.com/jacksonliam/mjpg-streamer/tree/master/mjpg-streamer-experimental>
Lizenz: [GPLv2](https://github.com/jacksonliam/mjpg-streamer#license)

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
