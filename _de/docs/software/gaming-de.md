# Gaming & Emulation

## �berblick

- [**OpenTyrian - Open-Source-Portierung des DOS-Spiels Tyrian**](#opentyrian)
- [**Cuberite - Schneller Minecraft-Server mit Webinterface**](#cuberite)
- [**MineOS - Mehrere Minecraft-Server mit Webinterface**](#mineos)
- [**Nukkit - Server f�r Minecraft Pocket Edition**](#nukkit)
- [**Amiberry - Amiga-Emulationssystem**](#amiberry)
- [**DXX-Rebirth - Descent 1 und 2 OpenGL-Port**](#dxx-rebirth)
- [**Steam - Steam-Client**](#steam)
- [**PaperMC - Schneller und optimierter Minecraft-Server**](#papermc)
- [**Box86 - i386 Userspace-Emulation f�r ARMv7**](#box86)
- [**Box64 - x86_64 Userspace-Emulation f�r ARMv8**](#box64)

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

## OpenTyrian

Tyrian ist ein vertikal scrollender Shooter im Arcade-Stil. Die Geschichte steht fest
in 20.031, wo Sie als Trent Hawkins spielen, ein erfahrener Kampfpilot, der angestellt ist
um gegen MicroSol zu k�mpfen und die Galaxie zu retten.

![OpenTyrian-Screenshot](../assets/images/dietpi-software-games-opentyrian.jpg){: width="400" height="251" loading="lazy"}

=== "Starte das Spiel"

    - Konsole: Um OpenTyrian von der Konsole aus auszuf�hren, verwenden Sie den folgenden Befehl: `opentyrian`
    - Desktop: Um OpenTyrian vom Desktop aus auszuf�hren, wurden ein Desktop-Symbol und ein Startmen�eintrag hinzugef�gt.
    - Autostart: Um OpenTyrian automatisch beim Booten auszuf�hren, w�hlen Sie es aus dem `dietpi-autostart`-Men� oder direkt �ber: `dietpi-autostart 4`

=== "Pers�nliche Notiz"

    Tyrian (OpenTyrian) ist zwar nicht das beste Spiel der Welt, aber das beste Top-Down-Shooter/Scroller-Spiel, das je entwickelt wurde.
    OpenTyrian l�sst sich am besten mit einer Maus und der ++Enter++-Taste erleben, um den R�ckfeuermodus zu �ndern.
    Es ist alt, retro und ein Klassiker usw., aber ich bezweifle, dass Sie ein �hnliches aktuelles Spiel finden werden, das der Sucht nach OpenTyrian nahe kommt.

## Cuberit

Mit Cuberite k�nnen Sie einen einzigen, blitzschnellen Minecraft-Server erstellen, der die Leistungsvorteile von C++ (anstelle von Java) nutzt und �ber eine praktische Weboberfl�che verf�gt.

![Ansicht der Cuberite-Weboberfl�che](../assets/images/dietpi-software-games-cuberite.png){: width="400" height="198" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

Das Webinterface ist �ber Port **1339** erreichbar:

    - URL = `http://<Ihre.IP>:1339`
    - Benutzername = `admin`
    - Passwort = `<globalSoftwarePassword>` (Standard: `dietpi`)

=== "Optimieren"

    Optimieren Sie die Servereinstellungen, indem Sie die folgenden Dateien �ndern:

    - Allgemeine Servereinstellungen:

        ```
        /mnt/dietpi_userdata/cubrite/settings.ini
        ```

    - Einstellungen f�r die Webadministration:

        ```
        /mnt/dietpi_userdata/cubrite/webadmin.ini
        ```

    - Einstellungen f�r die Welt:

        ```
        /mnt/dietpi_userdata/cubrite/world/world.ini
        ```

=== "Dienst neu starten"

    Sie k�nnen den Dienst neu starten, indem Sie Folgendes ausf�hren:

    ```sh
    systemctl restart cuberite
    ```

=== "Protokolle anzeigen"

    - Protokolldateien: `/mnt/dietpi_userdata/cubrite/logs/`
    - Dienstprotokolle: `journalctl -u cuberite`

=== "Aktualisieren"

    Update auf neuste Version:

    ```sh
    dietpi-software reinstall 52
    ```

##MineOS

Mit MineOS k�nnen Sie �ber eine einfache Weboberfl�che problemlos mehrere Minecraft-Server erstellen.

![Ansicht der MineOS-Weboberfl�che](../assets/images/dietpi-software-games-mineos.png){: width="400" height="208" loading="lazy"}

=== "Zugriff auf Webinterface"

    Das Webinterface ist �ber Port **8443** erreichbar:

    - URL: `https://<your.IP>:8443`
      Sie k�nnen die Zertifikats-"Warnung" getrost ignorieren, falls eine angezeigt wird.
    - Benutzername: �root�.
    - Passwort: Dasselbe wie Ihr Root-Login-Passwort. Standard ist �dietpi�.

=== "1st run setup"

Nach dem Einloggen in die Weboberfl�che:

    1. Klicken Sie auf Profile auf der linken Seite des Bildschirms
    2. W�hlen Sie eine Minecraft-Version, die Ihren Anforderungen entspricht, und klicken Sie dann auf Herunterladen
    3. Klicken Sie auf der linken Seite des Bildschirms auf Neuen Server erstellen
    4. Geben Sie einen Servernamen ein und klicken Sie dann unten auf Neuen Server erstellen
    5. Ihr Server wird nun am unteren Rand des Dashboard-Bildschirms angezeigt, w�hlen Sie ihn aus
    6. W�hlen Sie in den Dropdown-Feldern �Profil �ndern in:� und �Ausf�hrbare JAR-Datei �ndern in:� den Eintrag aus, der die Serverversionsnummer enth�lt, die Sie in Profile heruntergeladen haben
    7. Klicken Sie auf EULA akzeptieren
    8. Klicken Sie erneut auf EULA akzeptieren
    9. Klicken Sie auf Starten

Ihr Server sollte jetzt auf dem Standardport 25565 laufen.

***

Offizielles Forum: <https://discourse.codeemo.com/>
Quellcode: <https://github.com/hexparrot/mineos-node>
Lizenz: [GPLv3](https://github.com/hexparrot/mineos-node/blob/master/LICENSE.md)

##Nukkit

Nukkit ist ein Java-basierter Server f�r Minecraft Pocket Edition.

![Nukkit-Screenshot](../assets/images/dietpi-software-games-nukkit.png){: width="400" height="225" loading="lazy"}

=== "Informationen"

    Nukkit betreibt standardm��ig einen einzelnen Server, der im LAN verf�gbar ist.

=== "Optimieren"

    Optimieren Sie die Servereinstellungen, indem Sie die folgende Datei �ndern:

    ```
    /usr/local/bin/nukkit/server.properties
    ```

=== "Dienst neu starten"

    Sie k�nnen den Dienst neu starten, indem Sie Folgendes ausf�hren:

    ```sh
    systemctl restart nukkit
    ```

## Amibeere

Amiberry ist ein optimierter Amiga-Emulator f�r den Raspberry Pi und andere ARM-basierte SoCs, der Ihnen die leistungsst�rkste Amiga-Emulation bietet. Ob klassischer A500, A1200, CD32 oder bis hin zu einem High-End-Modell, das mit einem 68040 und einer Grafikkarte ausgestattet ist, wir haben alles f�r Sie.

Diese Installation ist m�glich durch eine Zusammenarbeit mit Dimitris Panokostas (Amiberry) und Daniel Knight (DietPi).

- Tastatur + Maus wird dringend empfohlen.
- Wir bieten auch ein vollst�ndig automatisiertes Installations-Image f�r Amiberry an. Siehe: <https://blitterstudio.com/amiberry/>.
- Direkter Download-Link: <https://dietpi.com/downloads/images/DietPi_RPi-ARMv6-Bullseye_Amiberry.7z>.

![Amiberry-Logo](../assets/images/dietpi-software-games-amiberry.jpg){: width="400" height="189" loading="lazy"}

=== "1st run setup"

    - **Kickstarts (Amiga BIOS/Bootsystem)**
      Amiga Kickstart ROM-Images sind erforderlich, um die Systeme auszuf�hren, die Sie emulieren m�chten. Diese k�nnen aufgrund von Urheberrechtsbeschr�nkungen nicht geb�ndelt werden.
      Wenn Sie das Amiga Forever-Produkt besitzen, k�nnen Sie Kickstarts, f�r die Sie berechtigt sind, legal herunterladen und verwenden von: <https://www.amigaroms.com/>
      **Anmerkung:** *Kickstart 1.3 (A500-A2500-A3000-CDTV) wird dringend empfohlen, um mit den meisten Spielen zu funktionieren.*
      Kickstarts k�nnen in `/mnt/dietpi_userdata/amiberry/kickstarts` abgelegt werden.
    - **Disketten (Amiga `.adf`-Images)**
      Disketten-Images von Amiga haben die Dateierweiterung `.adf`.
      Sie ben�tigen mindestens ein ADF-Image, um Ihr Amiga-Erlebnis zu beginnen.
      Laden Sie Ihren ADF oder platzieren Sie ihn dort, wo Sie ihn haben m�chten, z. B. erstellen und verwenden Sie:
      `/mnt/dietpi_userdata/amiberry/floppy_images`
      Denken Sie daran, die erforderlichen Berechtigungen zu erteilen, um Uploads �ber Dateiserver zuzulassen, z.
      `chown dietpi:dietpi /mnt/dietpi_userdata/amiberry/floppy_images`

=== "Starten"

    - Amiberry kann gestartet werden durch Ausf�hren von: `systemctl start amiberry`
    - Optional k�nnen Sie den Amiberry-Autostart aktivieren, um so schnell wie m�glich direkt in die Amiga-Umgebung zu booten, mit der geringstm�glichen St�rung durch Linux.
      F�hren Sie `dietpi-autostart 6` von der Konsole oder `dietpi-autostart` aus und w�hlen Sie *Amiberry fast boot* aus dem Men�, dann starten Sie Ihr System neu.
      Wenn Sie Probleme mit der Schnellstartoption haben oder andere Dienste zuerst starten m�ssen, verwenden Sie �dietpi-autostart 8� bzw. w�hlen Sie *Amiberry-Standardstart*.

=== "Erstelle eine Amiga-Konfiguration"

    Sobald Amiberry l�uft, m�ssen Sie den Emulator konfigurieren, um ihm mitzuteilen, welches Amiga-System emuliert werden soll.

    - W�hlen Sie �Schnellstart� (im Men� auf der linken Seite)
    - Unter Amiga-Modell: W�hlen Sie das Amiga-Modell aus, das Sie emulieren m�chten (Beispiel A500)
    - Unter Config: W�hlen Sie die zus�tzlichen Optionen f�r das Ziel-Amiga-Modell (falls erforderlich)
    - Klicken Sie auf die Schaltfl�che Konfiguration festlegen, um die �nderungen zu �bernehmen.

Als n�chstes m�ssen Sie den Emulator f�r das Kickstart- und Disketten-Image einrichten, das Sie verwenden m�chten:

    - Kickstart (ROM) ausw�hlen:
    - W�hlen Sie auf der linken Seite ROM aus.
    - Klicken Sie unter Haupt-ROM-Datei: auf die Schaltfl�che zum Durchsuchen (3 Punkte) ...
    - Navigieren Sie zu Ihrem Kickstarts-Verzeichnis
      `/mnt/dietpi_userdata/amiberry/kickstarts`
      Anmerkung: Amiberry unterst�tzt derzeit keine symbolischen Links. Wenn Sie ein dediziertes USB-Laufwerk installiert haben, lautet der Speicherort:
      `/mnt/uuid-of-drive/amiberry/kickstarts`
    - W�hlen Sie einen Kickstart (1.3 wird empfohlen)

    - W�hlen Sie ein Disketten-Image (ADF):
    - W�hlen Sie auf der linken Seite Diskettenlaufwerke.
    - W�hlen Sie unter `DF0:` die Schaltfl�che zum Durchsuchen auf der rechten Seite (3 Punkte) ...
    - Navigieren Sie zu Ihrem Disketten-Image-Verzeichnis, z
      `/mnt/dietpi_userdata/amiberry/floppy_images`
      Anmerkung: Amiberry unterst�tzt derzeit keine symbolischen Links. Wenn Sie ein dediziertes USB-Laufwerk installiert haben, lautet der Speicherort:
      `/mnt/uuid-of-drive/amiberry/floppy_images`
    - W�hlen Sie das ROM aus, das Sie verwenden m�chten.

=== "Vollbildausgabe aktivieren"

    W�hlen Sie auf der linken Seite **Anzeige** aus.
    Stellen Sie sicher, dass die Option **Vollbild** aktiviert ist.

=== "Optional: Stellen Sie die CPU-Geschwindigkeit auf die h�chste ein (empfohlen)"

    Dadurch wird der Amiga so schnell wie m�glich emuliert und sichergestellt, dass Sie die maximale FPS f�r Ihre SBC-Hardware erhalten.

    - W�hlen Sie auf der linken Seite CPU und FPU aus.
    - W�hlen Sie unter CPU-Geschwindigkeit die schnellste Option aus.
    - Wenn Sie feststellen, dass diese �nderung die Emulation verlangsamt, versuchen Sie es mit dem festen Wert von 25 MHz

=== "Optional: Konfiguration speichern (empfohlen)"

    Es wird empfohlen, Ihre Einstellungen zu speichern. Dadurch wird sichergestellt, dass die Einstellungen beim n�chsten Start von Amiberry �bernommen werden.

    - W�hlen Sie auf der linken Seite **Konfigurationen**.
    - Geben Sie den Namen ein, z. B. "autostart", und klicken Sie dann auf **Speichern**.

=== "H�ufig gestellte Fragen"

    #### Wie kann ich Kickstarts & Floppy Images auf das Ger�t �bertragen?

    Stellen Sie sicher, dass Sie einen der Dateiserver von DietPi installiert haben.

    - Floppy Disk Image (`.adf`) Verzeichnis wie zuvor gew�hlt, zB `/amiberry/floppy_images`
    - Kickstarts (`.rom`) Verzeichnis = `/amiberry/kickstarts`

    #### Wie kann ich das Konfigurationsfenster �ffnen, nachdem der Emulator gestartet wurde?

    Der vordefinierte Schl�ssel daf�r ist ++f12++.

    #### Wie kann ich die Amiga-Emulationsumgebung neu starten (Amiga-Reset)?

    Verwenden Sie die Tasten ++ctrl+lwin+rwin++.
    Wenn Sie keine Taste ++rwin++ haben, versuchen Sie es stattdessen mit der Taste ++menu++.

    #### Was sind die Standardsteuerungen f�r den Joystick, wenn eine Tastatur verwendet wird?

    Bei Verwendung einer Tastatur sind die standardm��igen Joystick-Steuerelemente:

    - ++oben++/++unten++/++links++/++rechts++ = Oben/Unten/Links/Rechts
    - ++Bild-unten++ = Feuer/Taste 1
    - ++Bild-auf++ = Feuer/Taste 2

    #### Wie kann ich die Leistung (Bildrate) verbessern?

    Eine ***niedrigere Aufl�sung*** kann die Leistung bei den meisten Spielen verbessern. Aus dem Hauptmen� des Emulators:

    - W�hlen Sie auf der linken Seite Anzeige
    - 640 x 256 ist eine hohe Aufl�sung
    - 320 x 256 ist eine niedrige Aufl�sung und sollte eine verbesserte Leistung bieten

    Durch ***�bertakten*** Ihres Systems wird die Leistung verbessert. Die Stabilit�t kann je nach Ger�t variieren und �bertaktung wird nicht offiziell unterst�tzt:

    - F�hren Sie von einem Terminal aus `dietpi-config` aus
    - W�hlen Sie das Men� Leistungsoptionen
    - W�hlen Sie �bertaktungsprofile
    - W�hlen Sie ein �bertaktungsprofil und starten Sie das System neu

    #### Wie stelle ich die Geschwindigkeit des Diskettenlaufwerks f�r Kompatibilit�t ein?

    Die Diskettenlaufwerk-Emulation ist standardm��ig auf "800 %" eingestellt. Dies reduziert die Ladezeiten um bis zu 8x.
    Sie k�nnen dies auf 100 % senken, was die Kompatibilit�t erh�ht:

    - W�hlen Sie auf der linken Seite Diskettenlaufwerke
    - �ndern Sie den Wert f�r die Emulationsgeschwindigkeit des Diskettenlaufwerks auf 100 %

    #### Einige Spiele sind nicht im Vollbildmodus

    Spiele laufen mit verschiedenen Aufl�sungen �ber das Hauptmen� des Emulators:

    - W�hlen Sie auf der linken Seite Anzeige
    - �ndern Sie den H�henwert auf 200 oder 256
    - Dr�cken Sie die Fortsetzen- oder Start-Taste

    Wenn Sie diese Installation n�tzlich finden, spenden Sie bitte. Verwenden Sie den folgenden Link und w�hlen Sie **Spenden f�r DietPi und Amiberry 50:50**, um es zwischen Dimitris Panokostas (Amiberry) und DietPi aufzuteilen.
    [PayPal spenden](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=6DVBECXRW3TAA)

**Gut zu GEHEN!**
Wenn Sie fertig sind, w�hlen Sie **Start**, um den Emulator zu starten. Habe Spa�!

***

YouTube-Video-Tutorial #1: *Amiga auf dem Raspberry Pi mit DietPi und Amiberry: Ich habe den Pi 400 zum Laufen gebracht!*.

<iframe src="https://www.youtube-nocookie.com/embed/osBU7iVSQ78?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

YouTube-Video-Tutorial #2: [Amiga auf dem Raspberry Pi mit DietPi und Amiberry: Workbench und Autobooting](https://www.youtube.com/watch?v=LU-G0PRNffQ)

## DXX-Wiedergeburt

Abstieg 1 & 2. Ein Meisterwerk 3D FPS. Mit dem DXX-Rebirth-Projekt wieder zum Leben erweckt. Spielen Sie Descent originalgetreu mit OpenGLES-Rendering.

- DietPi installiert die Demo- und Shareware-Versionen von Descent. Bitte lesen Sie die FAQ unten, um das vollst�ndige Spiel zu �bertragen.
- Tastatur + Maus wird dringend empfohlen
- Wir haben die neueste Version von DXX-Rebirth (0.58.1) mit Unterst�tzung f�r FB und RPi OpenGL kompiliert.

![DXX-Rebirth-Logo und Screenshot](../assets/images/dietpi-software-games-dxxrebirth.png){: width="400" height="156" loading="lazy"}

=== "Starte DXX-Rebirth"

    DXX-Rebirth kann durch Ausf�hren von `dxx-rebirth` gestartet werden.
    Um DXX-Rebirth beim Booten automatisch zu starten, f�hren Sie einfach �dietpi-autostart 7� von der Konsole oder �dietpi-autostart� aus und w�hlen Sie �DXX-Rebith (Descent 1/2)� aus dem Men� und starten Sie Ihr System neu.

=== "Einen Piloten ausw�hlen"

    Wir haben ein Pilotprojekt namens DietPi erstellt. Die Konfiguration wurde f�r das Spielen im WSAD-Stil eingerichtet und wird f�r FPS-Spieler empfohlen, die WSAD + Maus verwenden.

    - ++w++/++a++/++s++/++d++ = Vorw�rts/R�ckw�rts/Links/Rechts
    - ++q++/++z++ = Auf/Ab
    - ++e++/++r++ = Z-Achse (vorw�rts) drehen
    - ++f++ = Flare starten
    - ++alt+f2++ = Spiel speichern

=== "H�ufig gestellte Fragen"

    #### Wie �bertrage ich die vollst�ndigen Originalspieldateien von Descent?

    Bevor Sie beginnen, ben�tigen Sie die Originalspieldateien einer legalen Kopie und Installation von Descent.
    Stellen Sie sicher, dass Sie einen der Dateiserver von DietPi installiert haben.

    - Kopieren Sie Ihre Descent 1-Spieldateien nach `/mnt/dietpi_userdata/dxx-rebirth/descent_1_game`
    - Kopieren Sie Ihre Descent 2-Spieldateien nach `/mnt/dietpi_userdata/dxx-rebirth/descent_2_game`

***

Offizielle Website: <https://www.dxx-rebirth.com/>

## Steam

![Steam auf Linux-Logo](../assets/images/dietpi-software-games-steam.jpg){: width="400" height="267" loading="lazy"}

Steam ist ein Gaming-Client und -Shop von Valve.

### Steam auf ARM

Steam ist f�r x86 gemacht, aber es und viele Steam-Spiele mit Linux-Versionen k�nnen mit Hilfe von [Box86](#box86) auf ARM ausgef�hrt werden. Beachten Sie, dass 2D-Spiele am besten zu spielen sind und komplexere Spiele m�glicherweise eine �bertaktung Ihres Ger�ts erfordern.

??? Warnung �Bekannte Probleme auf ARM�

    - Nur der kleine Modus (die Liste der Minispiele) wird unterst�tzt, da der interne Bibliotheksbrowser auf 64-Bit-Komponenten angewiesen ist.
    - Daher ist es nicht m�glich, Spiele vom Client aus zu suchen/hinzuzuf�gen, was �ber den Website-Store (funktioniert nicht f�r kostenlose Spiele) oder einen anderen Client erfolgen muss.
    - Das Beenden des Steam-Clients funktioniert nur durch Ausf�hren von `killall steam.sh` von einer Konsole aus. Wenn Sie die Schaltfl�che �Beenden� aus dem Men� oder dem Bedienfeldsymbol verwenden, wird Steam h�ngen bleiben.

## PaperMC

Ein hochoptimierter Minecraft-Server mit Plugins, geschrieben in Java.
PaperMC f�hrt standardm��ig einen einzelnen Server aus, der im LAN verf�gbar ist, aber �ber einen Port weitergeleitet werden kann, damit andere Personen eine Verbindung herstellen k�nnen.

![PaperMC-Logo](../assets/images/dietpi-software-games-papermc.jpg){: width="100" height="100" loading="lazy"}

![PaperMC-Screenshot](../assets/images/dietpi-software-papermc.jpg){: width="500" height="300" loading="lazy"}

=== "Standardserver/Abfrageport"

    - Der standardm��ige Server-/Abfrageport ist: **25565**

=== "Konsolenzugriff �ber rcon"

    - Port: **25575**
    - Passwort: `<globalSoftwarePassword>` (Standard: `dietpi`)
    - Konsolenbefehl: `mcrcon -p <globalSoftwarePassword>`

=== "Verzeichnisse"

    - Launcher: `/opt/papermc`
    - Konfiguration und Daten: `/mnt/dietpi_userdata/papermc`
    - Protokolle: `/var/log/papermc`

=== "Protokolle anzeigen"

    - Dienst: `journalctl -u papermc`
    - Datei: `/var/log/papermc/latest.log`

=== "Optimieren"

    Optimieren Sie die Servereinstellungen, indem Sie die folgende Datei oder eine beliebige Datei im Konfigurationsverzeichnis �ndern, die auf �.yml� endet:
    `/mnt/dietpi_userdata/papermc/server.properties`

=== "Speicherverwaltung"

    Da PaperMC als Java-Anwendung l�uft, h�ngt der Systemspeicherbedarf stark von der Java-Heap-Gr��e ab, die angepasst werden kann. Die absolute Mindestkopfgr��e, die zum Ausf�hren von PaperMC erforderlich ist, betr�gt 512 MiB, was zu ~850 MiB insgesamt verwendetem Systemspeicher f�hrt. Wir empfehlen, ihn f�r die Produktionsnutzung auf mindestens 1 GiB (~1,35 GiB Gesamtspeichernutzung) oder h�her zu erh�hen, je nach Anzahl der Benutzer und installierten Plugins.

    Gehen Sie wie folgt vor, um die Gr��e des Java-Heapspeichers zu �ndern:

    1. F�hren Sie `dietpi-services` von der Konsole aus.
    2. W�hlen Sie `papermc`.
    3. W�hlen Sie `Bearbeiten`.
    4. Entkommentieren Sie die Zeile, die mit `#ExecStart=` beginnt (entfernen Sie das f�hrende `#`) und f�gen Sie z. B. `-Xms1G -Xmx1G` direkt hinter dem `java`-Befehl hinzu, um eine Heap-Gr��e von 1 GiB anzuwenden. Zus�tzlich m�ssen Sie oben ein `ExecStart=` hinzuf�gen, um den Befehl des urspr�nglichen Dienstes zu deaktivieren, sodass es schlie�lich so aussieht:

        ```
        ExecStart=
        ExecStart=/usr/bin/java -Xms1G -Xmx1G -jar /opt/papermc/paperclip.jar --nogui --noconsole
        ```

    5. Verwenden Sie ++ctrl+o++ und ++enter++, um die Datei zu speichern, dann ++ctrl+x++, um zum Men� �dietpi-services� zur�ckzukehren. Beim Beenden werden Sie gefragt, ob Sie den Dienst neu starten m�chten, um die �nderungen zu �bernehmen.

    !!! Warnung "Bewahren Sie Ihre Auslagerungsdatei nicht auf einer SD-Karte auf!"
        Wenn der verwendete Systemspeicher den physischen Arbeitsspeicher Ihres SBC �bersteigt, empfehlen wir dringend, die Auslagerungsdatei **nicht** auf einer SD-Karte, sondern auf einem externen Laufwerk zu speichern, da SD-Karten normalerweise die regelm��ige Verwendung nicht �berleben Auslagerungsdatei schreibt lange, was im schlimmsten Fall zu Serverabst�rzen und Datenverlust f�hrt.

=== "Dienst neu starten"

    Sie k�nnen den Dienst neu starten, indem Sie Folgendes ausf�hren:

    ```sh
    systemctl restart papermc
    ```

=== "Auf neueste Version aktualisieren"

    ```sh
    dietpi-software reinstall 181
    ```

=== "H�ufig gestellte Fragen"

    #### Wie greife ich auf die Konsole des Servers zu?

    Verwenden Sie das installierte Tool MCrcon: `mcrcon -p <globalSoftwarePassword>`

    #### Wie finde und installiere ich Plugins?

    <https://www.spigotmc.org/resources/categories/spigot.4/>

    Verschieben Sie einfach die heruntergeladene JAR-Datei in das Verzeichnis `/mnt/dietpi_userdata/papermc/plugins`.

    #### Auf welcher Version von Minecraft funktioniert das?

    PaperMC wurde entwickelt, um auf der Java-Edition ausgef�hrt zu werden, kann jedoch mit den optionalen Geyser- und Floodgate-Plug-ins auch auf der Bedrock-Edition ausgef�hrt werden.
    W�hlen Sie einfach, sie am Anfang zu installieren.

***

Offizielle Website: <https://paper.readthedocs.io>
Quellcode: <https://github.com/PaperMC/Paper>

##Box86

Mit Box86 k�nnen Sie **i386** Linux-Programme (z. B. Spiele) auf **ARMv7**-Systemen ausf�hren. Dank [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc), das standardm��ig aktiviert ist, k�nnen Sie **i386**-Bin�rdateien wie jede andere ausf�hrbare Datei ausf�hren und Box86 wird automatisch aufgerufen.

##Box64

Mit Box64 k�nnen Sie **x86_64** Linux-Programme (z. B. Spiele) auf **ARMv8**-Systemen ausf�hren. Dank [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc), das standardm��ig aktiviert ist, k�nnen Sie **x86_64**-Bin�rdateien wie jede andere ausf�hrbare Datei ausf�hren und Box64 wird automatisch aufgerufen.

[Zur�ck zur **Liste der optimierten Software**](../../software/)
