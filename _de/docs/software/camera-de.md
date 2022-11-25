# Kamera & �berwachung

## �berblick

- [**RPi Cam Control - Webinterface & Steuerelemente f�r Ihre RPi-Kamera**](#rpi-cam-control)
- [**MotionEye - Webinterface & �berwachung f�r Ihre Kamera**](#motioneye)
- [**mjpg-streamer - Einfaches Kamera-Streaming-Tool mit HTML-Plugin**](#mjpg-streamer)

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

## RPi-Kamerasteuerung

Das Paket *RPi Cam Control* kann in Kombination mit einem Raspberry Pi Kameramodul verwendet werden

- ein Bild machen
- ein Video aufnehmen
- Beobachten basierend auf Bewegungserkennung
- Nehmen Sie ein Video mit Zeitraffer auf

Es besteht aus der vollst�ndigen Steuerung der Kamera in einer webbasierten Schnittstelle.

![Screenshot der RPi Cam Control-Weboberfl�che](../assets/images/dietpi-software-camera-rpicamcontrol.png){: width="500" height="395" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    Das Webinterface ist erreichbar �ber:

    - URL = `http://<your.IP>/rpicam`

=== "Zugriff auf Aufzeichnungen (ohne Webinterface)"

    Um ohne das Webinterface aus der Ferne auf Ihre Aufzeichnungen zuzugreifen, m�chten Sie vielleicht einen der [Dateiserver von DietPi](../file_servers/) installiert haben.
    Von MotionEye verwendete Verzeichnisse:

    - Medienverzeichnis = `/mnt/dietpi_userdata/rpicam`
    - Zugriff vom Dateiserver = `/rpicam`

=== "Auf neueste Version aktualisieren"

    RPi Cam Control kann auf die neueste Version aktualisiert werden, indem es �ber neu installiert wird

    ```sh
    dietpi-software reinstall 59
    ```

=== "RPi-Kameramodul"

    Das RPi-Kameramodul wird w�hrend des Installationsvorgangs automatisch aktiviert. Es erfordert jedoch einen Neustart und/oder manchmal einen Power-Cycle, um wirksam zu werden.
    Die Kameraaktivierung kann �ber `dietpi-config` > `Display Options` > `RPi Camera` �berpr�ft werden, um `[On]` anzuzeigen. Zus�tzlich kann im selben Dialog �ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem �ndern der Kameraaktivierung m�ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/silvanmelchior/RPi_Cam_Web_Interface>
Wiki: <https://elinux.org/RPi-Cam-Web-Interface>
Lizenz: [MIT](https://github.com/silvanmelchior/RPi_Cam_Web_Interface/blob/master/LICENSE.txt)

## MotionEye

Das Paket *MotionEye* bietet �berwachung f�r Ihre Kamera.
Es konzentriert sich haupts�chlich auf die Verwendung der Bewegungserkennung. Es enth�lt ein Webinterface.

Die Software kann

- ein Bild machen
- ein Video aufnehmen
- Beobachten basierend auf Bewegungserkennung
- Nehmen Sie ein Video mit Zeitraffer auf

von jeder RPi-Kamera, USB-Kamera oder einem Netzwerkstream einer IP-Kamera.

![Screenshot der MotionEye-Weboberfl�che](../assets/images/dietpi-software-camera-motioneye.png){: width="500" height="246" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    Das Webinterface ist �ber Port **8765** erreichbar:

    - URL = `http://<Ihre.IP>:8765`
    - Benutzer = `admin`.
    - Passwort = nicht erforderlich

    Passw�rter k�nnen im Webinterface konfiguriert werden.

=== "Zugriff auf Aufzeichnungen (ohne Webinterface)"

    Um ohne das Webinterface aus der Ferne auf Ihre Aufzeichnungen zuzugreifen, m�chten Sie vielleicht einen der [Dateiserver von DietPi](../file_servers/) installiert haben.
    Von MotionEye verwendete Verzeichnisse:

    - Medienverzeichnis = `/mnt/dietpi_userdata/motioneye`
    - Zugriff �ber Dateiserver = `/motioneye`

=== "Auf neueste Version aktualisieren"

MotionEye kann auf die neueste Version aktualisiert werden �ber

    ```sh
    sudo pip2 install -U motioneye
    ```

=== "RPi-Kameramodul"

    Wenn Sie ein offizielles Raspberry Pi-Kameramodul haben, kann es �ber `dietpi-config` > `Display Options` > `RPi Camera` aktiviert werden, um `[On]` anzuzeigen.
    Zus�tzlich kann im selben Dialog �ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem �ndern der Kameraaktivierung m�ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/ccrisan/motioneye>
Wiki: <https://github.com/ccrisan/motioneye/wiki>
Tutorial: [MotionEye auf DietPi auf Raspberry Pi: alles im Blick behalten](https://mansfield-devine.com/speculatrix/2018/12/motioneye-on-dietpi-on-raspberry-pi/)
YouTube-Video-Tutorial: `DietPi & MotionEye - Vollautomatische Installation inkl. Wlan Konfiguration, Updates und Anwendung`.

<iframe src="https://www.youtube-nocookie.com/embed/vQxL3TfQK5E?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

Lizenz: [GPLv3](https://github.com/ccrisan/motioneye/blob/dev/LICENSE)

## mjpg-Streamer

Streamen Sie JPEG-Frames von verschiedenen Quellen zu verschiedenen m�glichen Ausg�ngen. Mit der Standardeinstellung wird ein angeh�ngtes Kamerabild mit dem enthaltenen HTTP-Plugin auf eine einfache Webseite gestreamt.

![mjpg-streamer HTML-Stream GIF](../assets/images/mjpg-streamer.gif){: width="500" height="400" loading="lazy"}

=== "Auf den HTTP-Stream zugreifen"

    Das Webinterface verwendet Port **8082**:

    - Stream: `http://<your.IP>:8082/?action=stream`
    - Snapshot: `http://<your.IP>:8082/?action=snapshot`
    - HTTP-Plugin-Dokumentation: <https://github.com/jacksonliam/mjpg-streamer/blob/master/mjpg-streamer-experimental/plugins/output_http/README.md>

=== "Setup f�r OctoPrint"

    Wenn [OctoPrint](../printing/#octprint) installiert wird, wird es automatisch so konfiguriert, dass es den mjpg-streamer-HTTP-Stream und Snapshots verwendet, da dies der Hauptanwendungsfall ist, f�r den dieser Softwaretitel angefordert wurde. Sie k�nnen die Einrichtung in den Einstellungen der OctoPrint-Weboberfl�che �berpr�fen und testen.

=== "HTML-Authentifizierung"

    Standardm��ig ist der HTTP-Stream auf Port **8082** ohne Authentifizierung zug�nglich. Dies ist erforderlich, wenn Sie es in [OctoPrint](../printing/#octprint) einbetten, da der Browser die Anfrage sendet und derzeit keine Anmeldeinformationen weitergeben kann. Wenn Sie den Stream jedoch anderweitig verwenden, insbesondere wenn Sie ihn dem World-Wide-Web zur Verf�gung stellen, empfehlen wir, ein Passwort einzurichten. Daf�r:

    1. F�hren Sie �dietpi-services� aus
    2. W�hlen Sie �mjpg-Streamer� aus
    3. W�hlen Sie �Bearbeiten�, um eine Service-Override-Konfiguration mit dem �nano�-Befehlszeileneditor zu �ffnen.
    4. Entkommentieren Sie im Abschnitt `[Service]` die Zeile `ExecStart=` und f�gen Sie ` -c username:password` zum letzten Block mit einfachen Anf�hrungszeichen `''` hinzu, mit Benutzername und Passwort Ihrer Wahl.
    5. Oberhalb dieser Zeile m�ssen Sie ein weiteres `ExecStart=` ohne Inhalt hinzuf�gen, das den urspr�nglichen Startbefehl entfernen soll, damit Ihr ihn effektiv ersetzt. Die Datei k�nnte schlie�lich so aussehen:

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

    6. Dr�cken Sie ++ctrl+o++, um die Datei zu speichern und ++ctrl+x++, um den Editor zu verlassen. Beim Beenden von `dietpi-services` wird der Dienst automatisch neu geladen und ist fortan passwortgesch�tzt.

=== "Auf neueste Version aktualisieren"

    mjpg-streamer kann auf die neueste Version aktualisiert werden, indem Sie ihn �ber neu installieren

    ```sh
    dietpi-software reinstall 137
    ```

=== "Protokollierung"

    Sie k�nnen die Dienstprotokolle �ber anzeigen

    ```sh
    journalctl -u mjpg-streamer
    ```

    und der Dienststatus �ber

    ```sh
    systemctl status mjpg-streamer
    ```

=== "RPi-Kameramodul"

    Wenn Sie ein offizielles Raspberry Pi-Kameramodul haben, kann es �ber `dietpi-config` > `Display Options` > `RPi Camera` aktiviert werden, um `[On]` anzuzeigen.
    Zus�tzlich kann im selben Dialog �ber `RPi Camera LED` das Verhalten der Kamera-LED eingestellt werden.

    Anmerkung: Nach dem �ndern der Kameraaktivierung m�ssen Sie den SBC inkl. Kamera.

    ![DietPi-Config Kameraaktivierung](../assets/images/dietpi-config_camera-activation.png){: width="500" height="290" loading="lazy"}

***

Github-Seite: <https://github.com/jacksonliam/mjpg-streamer>
Plugin-Dokumentation: <https://github.com/jacksonliam/mjpg-streamer/tree/master/mjpg-streamer-experimental>
Lizenz: [GPLv2](https://github.com/jacksonliam/mjpg-streamer#license)

[Zur�ck zur **Liste der optimierten Software**](../../software/)
