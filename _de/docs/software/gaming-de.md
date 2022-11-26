# Gaming & Emulation

## &Uuml;berblick

- [**OpenTyrian - Open-Source-Portierung des DOS-Spiels Tyrian**](#opentyrian)
- [**Cuberite - Schneller Minecraft-Server mit Webinterface**](#cuberite)
- [**MineOS - Mehrere Minecraft-Server mit Webinterface**](#mineos)
- [**Nukkit - Server f&uuml;r Minecraft Pocket Edition**](#nukkit)
- [**Amiberry - Amiga-Emulationssystem**](#amiberry)
- [**DXX-Rebirth - Descent 1 und 2 OpenGL-Port**](#dxx-rebirth)
- [**Steam - Steam-Client**](#steam)
- [**PaperMC - Schneller und optimierter Minecraft-Server**](#papermc)
- [**Box86 - i386 Userspace-Emulation f&uuml;r ARMv7**](#box86)
- [**Box64 - x86_64 Userspace-Emulation f&uuml;r ARMv8**](#box64)

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

## OpenTyrian

Tyrian ist ein vertikal scrollender Shooter im Arcade-Stil. Die Geschichte steht fest
in 20.031, wo Sie als Trent Hawkins spielen, ein erfahrener Kampfpilot, der angestellt ist
um gegen MicroSol zu k&auml;mpfen und die Galaxie zu retten.

![OpenTyrian-Screenshot](../assets/images/dietpi-software-games-opentyrian.jpg){: width="400" height="251" loading="lazy"}

=== "Starte das Spiel"

    - Konsole: Um OpenTyrian von der Konsole aus auszuf&uuml;hren, verwenden Sie den folgenden Befehl: `opentyrian`
    - Desktop: Um OpenTyrian vom Desktop aus auszuf&uuml;hren, wurden ein Desktop-Symbol und ein Startmen&uuml;eintrag hinzugef&uuml;gt.
    - Autostart: Um OpenTyrian automatisch beim Booten auszuf&uuml;hren, w&auml;hlen Sie es aus dem `dietpi-autostart`-Men&uuml; oder direkt &uuml;ber: `dietpi-autostart 4`

=== "Pers&ouml;nliche Notiz"

    Tyrian (OpenTyrian) ist zwar nicht das beste Spiel der Welt, aber das beste Top-Down-Shooter/Scroller-Spiel, das je entwickelt wurde.
    OpenTyrian l&auml;sst sich am besten mit einer Maus und der ++Enter++-Taste erleben, um den R&uuml;ckfeuermodus zu &auml;ndern.
    Es ist alt, retro und ein Klassiker usw., aber ich bezweifle, dass Sie ein &auml;hnliches aktuelles Spiel finden werden, das der Sucht nach OpenTyrian nahe kommt.

## Cuberit

Mit Cuberite k&ouml;nnen Sie einen einzigen, blitzschnellen Minecraft-Server erstellen, der die Leistungsvorteile von C++ (anstelle von Java) nutzt und &uuml;ber eine praktische Weboberfl&auml;che verf&uuml;gt.

![Ansicht der Cuberite-Weboberfl&auml;che](../assets/images/dietpi-software-games-cuberite.png){: width="400" height="198" loading="lazy"}

=== "Zugriff auf die Weboberfl&auml;che"

Das Webinterface ist &uuml;ber Port **1339** erreichbar:

    - URL = `http://<Ihre.IP>:1339`
    - Benutzername = `admin`
    - Passwort = `<globalSoftwarePassword>` (Standard: `dietpi`)

=== "Optimieren"

    Optimieren Sie die Servereinstellungen, indem Sie die folgenden Dateien &auml;ndern:

    - Allgemeine Servereinstellungen:

        ```
        /mnt/dietpi_userdata/cubrite/settings.ini
        ```

    - Einstellungen f&uuml;r die Webadministration:

        ```
        /mnt/dietpi_userdata/cubrite/webadmin.ini
        ```

    - Einstellungen f&uuml;r die Welt:

        ```
        /mnt/dietpi_userdata/cubrite/world/world.ini
        ```

=== "Dienst neu starten"

    Sie k&ouml;nnen den Dienst neu starten, indem Sie Folgendes ausf&uuml;hren:

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

Mit MineOS k&ouml;nnen Sie &uuml;ber eine einfache Weboberfl&auml;che problemlos mehrere Minecraft-Server erstellen.

![Ansicht der MineOS-Weboberfl&auml;che](../assets/images/dietpi-software-games-mineos.png){: width="400" height="208" loading="lazy"}

=== "Zugriff auf Webinterface"

    Das Webinterface ist &uuml;ber Port **8443** erreichbar:

    - URL: `https://<your.IP>:8443`
      Sie k&ouml;nnen die Zertifikats-"Warnung" getrost ignorieren, falls eine angezeigt wird.
    - Benutzername: `root`.
    - Passwort: Dasselbe wie Ihr Root-Login-Passwort. Standard ist `dietpi`.

=== "1st run setup"

Nach dem Einloggen in die Weboberfl&auml;che:

    1. Klicken Sie auf Profile auf der linken Seite des Bildschirms
    2. W&auml;hlen Sie eine Minecraft-Version, die Ihren Anforderungen entspricht, und klicken Sie dann auf Herunterladen
    3. Klicken Sie auf der linken Seite des Bildschirms auf Neuen Server erstellen
    4. Geben Sie einen Servernamen ein und klicken Sie dann unten auf Neuen Server erstellen
    5. Ihr Server wird nun am unteren Rand des Dashboard-Bildschirms angezeigt, w&auml;hlen Sie ihn aus
    6. W&auml;hlen Sie in den Dropdown-Feldern `Profil &auml;ndern in:` und `Ausf&uuml;hrbare JAR-Datei &auml;ndern in:` den Eintrag aus, der die Serverversionsnummer enth&auml;lt, die Sie in Profile heruntergeladen haben
    7. Klicken Sie auf EULA akzeptieren
    8. Klicken Sie erneut auf EULA akzeptieren
    9. Klicken Sie auf Starten

Ihr Server sollte jetzt auf dem Standardport 25565 laufen.

***

Offizielles Forum: <https://discourse.codeemo.com/>
Quellcode: <https://github.com/hexparrot/mineos-node>
Lizenz: [GPLv3](https://github.com/hexparrot/mineos-node/blob/master/LICENSE.md)

##Nukkit

Nukkit ist ein Java-basierter Server f&uuml;r Minecraft Pocket Edition.

![Nukkit-Screenshot](../assets/images/dietpi-software-games-nukkit.png){: width="400" height="225" loading="lazy"}

=== "Informationen"

    Nukkit betreibt standardm&auml;&szlig;ig einen einzelnen Server, der im LAN verf&uuml;gbar ist.

=== "Optimieren"

    Optimieren Sie die Servereinstellungen, indem Sie die folgende Datei &auml;ndern:

    ```
    /usr/local/bin/nukkit/server.properties
    ```

=== "Dienst neu starten"

    Sie k&ouml;nnen den Dienst neu starten, indem Sie Folgendes ausf&uuml;hren:

    ```sh
    systemctl restart nukkit
    ```

## Amibeere

Amiberry ist ein optimierter Amiga-Emulator f&uuml;r den Raspberry Pi und andere ARM-basierte SoCs, der Ihnen die leistungsst&auml;rkste Amiga-Emulation bietet. Ob klassischer A500, A1200, CD32 oder bis hin zu einem High-End-Modell, das mit einem 68040 und einer Grafikkarte ausgestattet ist, wir haben alles f&uuml;r Sie.

Diese Installation ist m&ouml;glich durch eine Zusammenarbeit mit Dimitris Panokostas (Amiberry) und Daniel Knight (DietPi).

- Tastatur + Maus wird dringend empfohlen.
- Wir bieten auch ein vollst&auml;ndig automatisiertes Installations-Image f&uuml;r Amiberry an. Siehe: <https://blitterstudio.com/amiberry/>.
- Direkter Download-Link: <https://dietpi.com/downloads/images/DietPi_RPi-ARMv6-Bullseye_Amiberry.7z>.

![Amiberry-Logo](../assets/images/dietpi-software-games-amiberry.jpg){: width="400" height="189" loading="lazy"}

=== "1st run setup"

    - **Kickstarts (Amiga BIOS/Bootsystem)**
      Amiga Kickstart ROM-Images sind erforderlich, um die Systeme auszuf&uuml;hren, die Sie emulieren m&ouml;chten. Diese k&ouml;nnen aufgrund von Urheberrechtsbeschr&auml;nkungen nicht geb&uuml;ndelt werden.
      Wenn Sie das Amiga Forever-Produkt besitzen, k&ouml;nnen Sie Kickstarts, f&uuml;r die Sie berechtigt sind, legal herunterladen und verwenden von: <https://www.amigaroms.com/>
      **Anmerkung:** *Kickstart 1.3 (A500-A2500-A3000-CDTV) wird dringend empfohlen, um mit den meisten Spielen zu funktionieren.*
      Kickstarts k&ouml;nnen in `/mnt/dietpi_userdata/amiberry/kickstarts` abgelegt werden.
    - **Disketten (Amiga `.adf`-Images)**
      Disketten-Images von Amiga haben die Dateierweiterung `.adf`.
      Sie ben&ouml;tigen mindestens ein ADF-Image, um Ihr Amiga-Erlebnis zu beginnen.
      Laden Sie Ihren ADF oder platzieren Sie ihn dort, wo Sie ihn haben m&ouml;chten, z. B. erstellen und verwenden Sie:
      `/mnt/dietpi_userdata/amiberry/floppy_images`
      Denken Sie daran, die erforderlichen Berechtigungen zu erteilen, um Uploads &uuml;ber Dateiserver zuzulassen, z.
      `chown dietpi:dietpi /mnt/dietpi_userdata/amiberry/floppy_images`

=== "Starten"

    - Amiberry kann gestartet werden durch Ausf&uuml;hren von: `systemctl start amiberry`
    - Optional k&ouml;nnen Sie den Amiberry-Autostart aktivieren, um so schnell wie m&ouml;glich direkt in die Amiga-Umgebung zu booten, mit der geringstm&ouml;glichen St&ouml;rung durch Linux.
      F&uuml;hren Sie `dietpi-autostart 6` von der Konsole oder `dietpi-autostart` aus und w&auml;hlen Sie *Amiberry fast boot* aus dem Men&uuml;, dann starten Sie Ihr System neu.
      Wenn Sie Probleme mit der Schnellstartoption haben oder andere Dienste zuerst starten m&uuml;ssen, verwenden Sie `dietpi-autostart 8` bzw. w&auml;hlen Sie *Amiberry-Standardstart*.

=== "Erstelle eine Amiga-Konfiguration"

    Sobald Amiberry l&auml;uft, m&uuml;ssen Sie den Emulator konfigurieren, um ihm mitzuteilen, welches Amiga-System emuliert werden soll.

    - W&auml;hlen Sie `Schnellstart` (im Men&uuml; auf der linken Seite)
    - Unter Amiga-Modell: W&auml;hlen Sie das Amiga-Modell aus, das Sie emulieren m&ouml;chten (Beispiel A500)
    - Unter Config: W&auml;hlen Sie die zus&auml;tzlichen Optionen f&uuml;r das Ziel-Amiga-Modell (falls erforderlich)
    - Klicken Sie auf die Schaltfl&auml;che Konfiguration festlegen, um die &Auml;nderungen zu &uuml;bernehmen.

Als n&auml;chstes m&uuml;ssen Sie den Emulator f&uuml;r das Kickstart- und Disketten-Image einrichten, das Sie verwenden m&ouml;chten:

    - Kickstart (ROM) ausw&auml;hlen:
    - W&auml;hlen Sie auf der linken Seite ROM aus.
    - Klicken Sie unter Haupt-ROM-Datei: auf die Schaltfl&auml;che zum Durchsuchen (3 Punkte) ...
    - Navigieren Sie zu Ihrem Kickstarts-Verzeichnis
      `/mnt/dietpi_userdata/amiberry/kickstarts`
      Anmerkung: Amiberry unterst&uuml;tzt derzeit keine symbolischen Links. Wenn Sie ein dediziertes USB-Laufwerk installiert haben, lautet der Speicherort:
      `/mnt/uuid-of-drive/amiberry/kickstarts`
    - W&auml;hlen Sie einen Kickstart (1.3 wird empfohlen)

    - W&auml;hlen Sie ein Disketten-Image (ADF):
    - W&auml;hlen Sie auf der linken Seite Diskettenlaufwerke.
    - W&auml;hlen Sie unter `DF0:` die Schaltfl&auml;che zum Durchsuchen auf der rechten Seite (3 Punkte) ...
    - Navigieren Sie zu Ihrem Disketten-Image-Verzeichnis, z
      `/mnt/dietpi_userdata/amiberry/floppy_images`
      Anmerkung: Amiberry unterst&uuml;tzt derzeit keine symbolischen Links. Wenn Sie ein dediziertes USB-Laufwerk installiert haben, lautet der Speicherort:
      `/mnt/uuid-of-drive/amiberry/floppy_images`
    - W&auml;hlen Sie das ROM aus, das Sie verwenden m&ouml;chten.

=== "Vollbildausgabe aktivieren"

    W&auml;hlen Sie auf der linken Seite **Anzeige** aus.
    Stellen Sie sicher, dass die Option **Vollbild** aktiviert ist.

=== "Optional: Stellen Sie die CPU-Geschwindigkeit auf die h&ouml;chste ein (empfohlen)"

    Dadurch wird der Amiga so schnell wie m&ouml;glich emuliert und sichergestellt, dass Sie die maximale FPS f&uuml;r Ihre SBC-Hardware erhalten.

    - W&auml;hlen Sie auf der linken Seite CPU und FPU aus.
    - W&auml;hlen Sie unter CPU-Geschwindigkeit die schnellste Option aus.
    - Wenn Sie feststellen, dass diese &Auml;nderung die Emulation verlangsamt, versuchen Sie es mit dem festen Wert von 25 MHz

=== "Optional: Konfiguration speichern (empfohlen)"

    Es wird empfohlen, Ihre Einstellungen zu speichern. Dadurch wird sichergestellt, dass die Einstellungen beim n&auml;chsten Start von Amiberry &uuml;bernommen werden.

    - W&auml;hlen Sie auf der linken Seite **Konfigurationen**.
    - Geben Sie den Namen ein, z. B. "autostart", und klicken Sie dann auf **Speichern**.

=== "H&auml;ufig gestellte Fragen"

    #### Wie kann ich Kickstarts & Floppy Images auf das Ger&auml;t &uuml;bertragen?

    Stellen Sie sicher, dass Sie einen der Dateiserver von DietPi installiert haben.

    - Floppy Disk Image (`.adf`) Verzeichnis wie zuvor gew&auml;hlt, zB `/amiberry/floppy_images`
    - Kickstarts (`.rom`) Verzeichnis = `/amiberry/kickstarts`

    #### Wie kann ich das Konfigurationsfenster &ouml;ffnen, nachdem der Emulator gestartet wurde?

    Der vordefinierte Schl&uuml;ssel daf&uuml;r ist ++f12++.

    #### Wie kann ich die Amiga-Emulationsumgebung neu starten (Amiga-Reset)?

    Verwenden Sie die Tasten ++ctrl+lwin+rwin++.
    Wenn Sie keine Taste ++rwin++ haben, versuchen Sie es stattdessen mit der Taste ++menu++.

    #### Was sind die Standardsteuerungen f&uuml;r den Joystick, wenn eine Tastatur verwendet wird?

    Bei Verwendung einer Tastatur sind die standardm&auml;&szlig;igen Joystick-Steuerelemente:

    - ++oben++/++unten++/++links++/++rechts++ = Oben/Unten/Links/Rechts
    - ++Bild-unten++ = Feuer/Taste 1
    - ++Bild-auf++ = Feuer/Taste 2

    #### Wie kann ich die Leistung (Bildrate) verbessern?

    Eine ***niedrigere Aufl&ouml;sung*** kann die Leistung bei den meisten Spielen verbessern. Aus dem Hauptmen&uuml; des Emulators:

    - W&auml;hlen Sie auf der linken Seite Anzeige
    - 640 x 256 ist eine hohe Aufl&ouml;sung
    - 320 x 256 ist eine niedrige Aufl&ouml;sung und sollte eine verbesserte Leistung bieten

    Durch ***&Uuml;bertakten*** Ihres Systems wird die Leistung verbessert. Die Stabilit&auml;t kann je nach Ger&auml;t variieren und &Uuml;bertaktung wird nicht offiziell unterst&uuml;tzt:

    - F&uuml;hren Sie von einem Terminal aus `dietpi-config` aus
    - W&auml;hlen Sie das Men&uuml; Leistungsoptionen
    - W&auml;hlen Sie &Uuml;bertaktungsprofile
    - W&auml;hlen Sie ein &Uuml;bertaktungsprofil und starten Sie das System neu

    #### Wie stelle ich die Geschwindigkeit des Diskettenlaufwerks f&uuml;r Kompatibilit&auml;t ein?

    Die Diskettenlaufwerk-Emulation ist standardm&auml;&szlig;ig auf "800 %" eingestellt. Dies reduziert die Ladezeiten um bis zu 8x.
    Sie k&ouml;nnen dies auf 100 % senken, was die Kompatibilit&auml;t erh&ouml;ht:

    - W&auml;hlen Sie auf der linken Seite Diskettenlaufwerke
    - &Auml;ndern Sie den Wert f&uuml;r die Emulationsgeschwindigkeit des Diskettenlaufwerks auf 100 %

    #### Einige Spiele sind nicht im Vollbildmodus

    Spiele laufen mit verschiedenen Aufl&ouml;sungen &uuml;ber das Hauptmen&uuml; des Emulators:

    - W&auml;hlen Sie auf der linken Seite Anzeige
    - &Auml;ndern Sie den H&ouml;henwert auf 200 oder 256
    - Dr&uuml;cken Sie die Fortsetzen- oder Start-Taste

    Wenn Sie diese Installation n&uuml;tzlich finden, spenden Sie bitte. Verwenden Sie den folgenden Link und w&auml;hlen Sie **Spenden f&uuml;r DietPi und Amiberry 50:50**, um es zwischen Dimitris Panokostas (Amiberry) und DietPi aufzuteilen.
    [PayPal spenden](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=6DVBECXRW3TAA)

**Gut zu GEHEN!**
Wenn Sie fertig sind, w&auml;hlen Sie **Start**, um den Emulator zu starten. Habe Spa&szlig;!

***

YouTube-Video-Tutorial #1: *Amiga auf dem Raspberry Pi mit DietPi und Amiberry: Ich habe den Pi 400 zum Laufen gebracht!*.

<iframe src="https://www.youtube-nocookie.com/embed/osBU7iVSQ78?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

YouTube-Video-Tutorial #2: [Amiga auf dem Raspberry Pi mit DietPi und Amiberry: Workbench und Autobooting](https://www.youtube.com/watch?v=LU-G0PRNffQ)

## DXX-Wiedergeburt

Abstieg 1 & 2. Ein Meisterwerk 3D FPS. Mit dem DXX-Rebirth-Projekt wieder zum Leben erweckt. Spielen Sie Descent originalgetreu mit OpenGLES-Rendering.

- DietPi installiert die Demo- und Shareware-Versionen von Descent. Bitte lesen Sie die FAQ unten, um das vollst&auml;ndige Spiel zu &uuml;bertragen.
- Tastatur + Maus wird dringend empfohlen
- Wir haben die neueste Version von DXX-Rebirth (0.58.1) mit Unterst&uuml;tzung f&uuml;r FB und RPi OpenGL kompiliert.

![DXX-Rebirth-Logo und Screenshot](../assets/images/dietpi-software-games-dxxrebirth.png){: width="400" height="156" loading="lazy"}

=== "Starte DXX-Rebirth"

    DXX-Rebirth kann durch Ausf&uuml;hren von `dxx-rebirth` gestartet werden.
    Um DXX-Rebirth beim Booten automatisch zu starten, f&uuml;hren Sie einfach `dietpi-autostart 7` von der Konsole oder `dietpi-autostart` aus und w&auml;hlen Sie `DXX-Rebith (Descent 1/2)` aus dem Men&uuml; und starten Sie Ihr System neu.

=== "Einen Piloten ausw&auml;hlen"

    Wir haben ein Pilotprojekt namens DietPi erstellt. Die Konfiguration wurde f&uuml;r das Spielen im WSAD-Stil eingerichtet und wird f&uuml;r FPS-Spieler empfohlen, die WSAD + Maus verwenden.

    - ++w++/++a++/++s++/++d++ = Vorw&auml;rts/R&uuml;ckw&auml;rts/Links/Rechts
    - ++q++/++z++ = Auf/Ab
    - ++e++/++r++ = Z-Achse (vorw&auml;rts) drehen
    - ++f++ = Flare starten
    - ++alt+f2++ = Spiel speichern

=== "H&auml;ufig gestellte Fragen"

    #### Wie &uuml;bertrage ich die vollst&auml;ndigen Originalspieldateien von Descent?

    Bevor Sie beginnen, ben&ouml;tigen Sie die Originalspieldateien einer legalen Kopie und Installation von Descent.
    Stellen Sie sicher, dass Sie einen der Dateiserver von DietPi installiert haben.

    - Kopieren Sie Ihre Descent 1-Spieldateien nach `/mnt/dietpi_userdata/dxx-rebirth/descent_1_game`
    - Kopieren Sie Ihre Descent 2-Spieldateien nach `/mnt/dietpi_userdata/dxx-rebirth/descent_2_game`

***

Offizielle Website: <https://www.dxx-rebirth.com/>

## Steam

![Steam auf Linux-Logo](../assets/images/dietpi-software-games-steam.jpg){: width="400" height="267" loading="lazy"}

Steam ist ein Gaming-Client und -Shop von Valve.

### Steam auf ARM

Steam ist f&uuml;r x86 gemacht, aber es und viele Steam-Spiele mit Linux-Versionen k&ouml;nnen mit Hilfe von [Box86](#box86) auf ARM ausgef&uuml;hrt werden. Beachten Sie, dass 2D-Spiele am besten zu spielen sind und komplexere Spiele m&ouml;glicherweise eine &Uuml;bertaktung Ihres Ger&auml;ts erfordern.

??? Warnung `Bekannte Probleme auf ARM`

    - Nur der kleine Modus (die Liste der Minispiele) wird unterst&uuml;tzt, da der interne Bibliotheksbrowser auf 64-Bit-Komponenten angewiesen ist.
    - Daher ist es nicht m&ouml;glich, Spiele vom Client aus zu suchen/hinzuzuf&uuml;gen, was &uuml;ber den Website-Store (funktioniert nicht f&uuml;r kostenlose Spiele) oder einen anderen Client erfolgen muss.
    - Das Beenden des Steam-Clients funktioniert nur durch Ausf&uuml;hren von `killall steam.sh` von einer Konsole aus. Wenn Sie die Schaltfl&auml;che `Beenden` aus dem Men&uuml; oder dem Bedienfeldsymbol verwenden, wird Steam h&auml;ngen bleiben.

## PaperMC

Ein hochoptimierter Minecraft-Server mit Plugins, geschrieben in Java.
PaperMC f&uuml;hrt standardm&auml;&szlig;ig einen einzelnen Server aus, der im LAN verf&uuml;gbar ist, aber &uuml;ber einen Port weitergeleitet werden kann, damit andere Personen eine Verbindung herstellen k&ouml;nnen.

![PaperMC-Logo](../assets/images/dietpi-software-games-papermc.jpg){: width="100" height="100" loading="lazy"}

![PaperMC-Screenshot](../assets/images/dietpi-software-papermc.jpg){: width="500" height="300" loading="lazy"}

=== "Standardserver/Abfrageport"

    - Der standardm&auml;&szlig;ige Server-/Abfrageport ist: **25565**

=== "Konsolenzugriff &uuml;ber rcon"

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

    Optimieren Sie die Servereinstellungen, indem Sie die folgende Datei oder eine beliebige Datei im Konfigurationsverzeichnis &auml;ndern, die auf `.yml` endet:
    `/mnt/dietpi_userdata/papermc/server.properties`

=== "Speicherverwaltung"

    Da PaperMC als Java-Anwendung l&auml;uft, h&auml;ngt der Systemspeicherbedarf stark von der Java-Heap-Gr&ouml;&szlig;e ab, die angepasst werden kann. Die absolute Mindestkopfgr&ouml;&szlig;e, die zum Ausf&uuml;hren von PaperMC erforderlich ist, betr&auml;gt 512 MiB, was zu ~850 MiB insgesamt verwendetem Systemspeicher f&uuml;hrt. Wir empfehlen, ihn f&uuml;r die Produktionsnutzung auf mindestens 1 GiB (~1,35 GiB Gesamtspeichernutzung) oder h&ouml;her zu erh&ouml;hen, je nach Anzahl der Benutzer und installierten Plugins.

    Gehen Sie wie folgt vor, um die Gr&ouml;&szlig;e des Java-Heapspeichers zu &auml;ndern:

    1. F&uuml;hren Sie `dietpi-services` von der Konsole aus.
    2. W&auml;hlen Sie `papermc`.
    3. W&auml;hlen Sie `Bearbeiten`.
    4. Entkommentieren Sie die Zeile, die mit `#ExecStart=` beginnt (entfernen Sie das f&uuml;hrende `#`) und f&uuml;gen Sie z. B. `-Xms1G -Xmx1G` direkt hinter dem `java`-Befehl hinzu, um eine Heap-Gr&ouml;&szlig;e von 1 GiB anzuwenden. Zus&auml;tzlich m&uuml;ssen Sie oben ein `ExecStart=` hinzuf&uuml;gen, um den Befehl des urspr&uuml;nglichen Dienstes zu deaktivieren, sodass es schlie&szlig;lich so aussieht:

        ```
        ExecStart=
        ExecStart=/usr/bin/java -Xms1G -Xmx1G -jar /opt/papermc/paperclip.jar --nogui --noconsole
        ```

    5. Verwenden Sie ++ctrl+o++ und ++enter++, um die Datei zu speichern, dann ++ctrl+x++, um zum Men&uuml; `dietpi-services` zur&uuml;ckzukehren. Beim Beenden werden Sie gefragt, ob Sie den Dienst neu starten m&ouml;chten, um die &Auml;nderungen zu &uuml;bernehmen.

    !!! Warnung "Bewahren Sie Ihre Auslagerungsdatei nicht auf einer SD-Karte auf!"
        Wenn der verwendete Systemspeicher den physischen Arbeitsspeicher Ihres SBC &uuml;bersteigt, empfehlen wir dringend, die Auslagerungsdatei **nicht** auf einer SD-Karte, sondern auf einem externen Laufwerk zu speichern, da SD-Karten normalerweise die regelm&auml;&szlig;ige Verwendung nicht &uuml;berleben Auslagerungsdatei schreibt lange, was im schlimmsten Fall zu Serverabst&uuml;rzen und Datenverlust f&uuml;hrt.

=== "Dienst neu starten"

    Sie k&ouml;nnen den Dienst neu starten, indem Sie Folgendes ausf&uuml;hren:

    ```sh
    systemctl restart papermc
    ```

=== "Auf neueste Version aktualisieren"

    ```sh
    dietpi-software reinstall 181
    ```

=== "H&auml;ufig gestellte Fragen"

    #### Wie greife ich auf die Konsole des Servers zu?

    Verwenden Sie das installierte Tool MCrcon: `mcrcon -p <globalSoftwarePassword>`

    #### Wie finde und installiere ich Plugins?

    <https://www.spigotmc.org/resources/categories/spigot.4/>

    Verschieben Sie einfach die heruntergeladene JAR-Datei in das Verzeichnis `/mnt/dietpi_userdata/papermc/plugins`.

    #### Auf welcher Version von Minecraft funktioniert das?

    PaperMC wurde entwickelt, um auf der Java-Edition ausgef&uuml;hrt zu werden, kann jedoch mit den optionalen Geyser- und Floodgate-Plug-ins auch auf der Bedrock-Edition ausgef&uuml;hrt werden.
    W&auml;hlen Sie einfach, sie am Anfang zu installieren.

***

Offizielle Website: <https://paper.readthedocs.io>
Quellcode: <https://github.com/PaperMC/Paper>

##Box86

Mit Box86 k&ouml;nnen Sie **i386** Linux-Programme (z. B. Spiele) auf **ARMv7**-Systemen ausf&uuml;hren. Dank [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc), das standardm&auml;&szlig;ig aktiviert ist, k&ouml;nnen Sie **i386**-Bin&auml;rdateien wie jede andere ausf&uuml;hrbare Datei ausf&uuml;hren und Box86 wird automatisch aufgerufen.

##Box64

Mit Box64 k&ouml;nnen Sie **x86_64** Linux-Programme (z. B. Spiele) auf **ARMv8**-Systemen ausf&uuml;hren. Dank [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc), das standardm&auml;&szlig;ig aktiviert ist, k&ouml;nnen Sie **x86_64**-Bin&auml;rdateien wie jede andere ausf&uuml;hrbare Datei ausf&uuml;hren und Box64 wird automatisch aufgerufen.

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
