# Desktop-Umgebungen und Dienstprogramme

## Überblick

### Desktops

- [**LXDE - Hochoptimierter ultraleichter Desktop**](#lxde)
- [**LXQt - Glatter und optimierter leichter Desktop**](#lxqt)
- [**MATE - Beliebter Gnome 2-Desktop**](#mate)
- [**Xfce - Lightweight-Desktop**](#xfce)
- [**GNUstep - Alternativer/einzigartiger Desktop**](#gnustep)

### Desktop-Dienstprogramme

- [**Chromium - Webbrowser**](#chromium)
- [**Firefox - Webbrowser**](#firefox)
- [**GIMP - Bildbearbeitung**](#gimp)
- [**QuiteRSS - Reader für RSS- und Atom-Newsfeeds**](#quiterss)
- [**Xfce Power Manager - Energiemanager mit Helligkeitssteuerung**](#xfce-power-manager)

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

##LXDE

LXDE ist ein hochoptimierter und ultraleichter Desktop. Es funktioniert gut mit Computern am unteren Ende des Leistungsspektrums wie Netbooks und kleinen Computern der neuen Generation oder älteren Computern mit begrenzten Ressourcen.

![LXDE-Screenshot](../assets/images/dietpi-software-LXDE_desktop.jpg){: width="795" height="600" loading="lazy"}

=== "Schnellstart"
    Nach der Installation kann der Desktop durch Eingabe ausgeführt werden

    ```sh
    startx
    ```

=== "Autostart aktivieren"
    Um verschiedene Programme beim Booten des Systems zu starten, führen Sie von der Befehlszeile aus:

    ```sh
    dietpi-autostart
    ```

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

***

Website: <https://www.lxde.org>
Offizielle Dokumentation: <https://wiki.lxde.org/en/Main_Page>

##LXQt

Optimierter leichter Desktop ohne Bloatware. Glatte und flüssige GUI, jedoch ressourcenintensiver als LXDE.

![LXQt-Screenshot](../assets/images/dietpi-software-LXQt_desktop.png){: width="1280" height="720" loading="lazy"}

Quelle: [LXQt](https://lxqt.github.io/screenshots/), CC BY-SA 3.0, [wikimedia](https://commons.wikimedia.org/w/index.php?curid=52420839) .

=== "Schnellstart"
    Nach der Installation kann der Desktop durch Eingabe ausgeführt werden

    ```sh
    startx
    ```

=== "Autostart aktivieren"
    Um verschiedene Programme beim Booten des Systems zu starten, führen Sie von der Befehlszeile aus:

    ```sh
    dietpi-autostart
    ```

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

***

Offizielle Dokumentation: <https://wiki.debian.org/LXQt>

## MATE

Beliebte Gnome2-basierte Desktop-Umgebung.

![MATE-Screenshot](../assets/images/dietpi-software-mate-desktop.jpg){: width="1280" height="960" loading="lazy"}

=== "Schnellstart"
    Nach der Installation kann der Desktop durch Eingabe ausgeführt werden

    ```sh
    startx
    ```

=== "Autostart aktivieren"
    Um verschiedene Programme beim Booten des Systems zu starten, führen Sie von der Befehlszeile aus:

    ```sh
    dietpi-autostart
    ```

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

***

Website: <https://mate-desktop.org>

## Xfce

![Xfce-Screenshot](../assets/images/dietpi-software-xfce-desktop.jpg){: width="800" height="450" loading="lazy"}

=== "Schnellstart"
    Nach der Installation kann der Desktop durch Eingabe ausgeführt werden

    ```sh
    startx
    ```

=== "Autostart aktivieren"
    Um verschiedene Programme beim Booten des Systems zu starten, führen Sie von der Befehlszeile aus:

    ```sh
    dietpi-autostart
    ```

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

***

Webseite: <https://wiki.debian.org/Xfce>

## GNUstep

![GNUstep-Screenshot](../assets/images/dietpi-software-gnustep-desktop.jpg){: width="885" height="720" loading="lazy"}

=== "Schnellstart"
    Nach der Installation kann der Desktop durch Eingabe ausgeführt werden

    ```sh
    startx
    ```

=== "Autostart aktivieren"
    Um verschiedene Programme beim Booten des Systems zu starten, führen Sie von der Befehlszeile aus:

    ```sh
    dietpi-autostart
    ```

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

***

Website: <http://gnustep.org>

## Desktop-Dienstprogramme

### Chromium

#### Unterstützt mein Gerät GPU-Beschleunigung?

Nicht alle Geräte unterstützen die GPU-Beschleunigung mit Chromium.

- RPis unterstützt natives OpenGL und wird während der Installation konfiguriert.
- Odroids unterstützen OpenGLES und werden während der Installation konfiguriert.
- Andere Geräte werden höchstwahrscheinlich auf Software-Rendering beschränkt sein.

#### Wo kann ich den Status der GPU-Beschleunigung überprüfen?

Sobald Chromium läuft, gehen Sie einfach zu folgender Adresse: <chrome://gpu>

#### Unterstützung für Widevine DRM-geschützte Inhalte auf RPi aktivieren

- Manuell: [https://blog.vpetkov.net/2019/07/12/net ... -chromium/](https://blog.vpetkov.net/2019/07/12/netflix-and-spotify-on-a-raspberry-pi-4-with-latest-default-chromium/)
- mit Skripten: [[https://blog.vpetkov.net/2020/03/30/ras ... many-others/](https://blog.vpetkov.net/2020/03/30/raspberry-pi-netflix-one-line-easy-install-along-with-hulu-amazon-prime-disney-plus-hbo-spotify-pandora-and-many-others/)

![Chromium-Screenshot](../assets/images/dietpi-software-desktop-tools-chromium.jpg){: width="1376" height="858" loading="lazy"}

### Firefox

![Firefox-Logo](../assets/images/dietpi-software-firefox.png){: width="128" height="128" loading="lazy"}

Firefox Browser, auch einfach als Firefox bekannt, ist ein kostenloser Open-Source-Webbrowser, der von der Mozilla Foundation und ihrer Tochtergesellschaft, der Mozilla Corporation, entwickelt wurde.

Ähnlich wie [Chromium](#chromium) wurde Firefox zu einer separaten Installationsoption gemacht. Für Desktop-Installationen können Benutzer zwischen Chromium, Firefox oder keinem Webbrowser wählen.

![Firefox-Screenshot](../assets/images/dietpi-software-firefox-display.png){: width="1024" height="723" loading="lazy"}

### GIMP

MS Paint auf Steroiden. Wenn Sie Pixel mit einer Vielzahl von Werkzeugen bearbeiten müssen, ist GIMP das einzige Programm, das Sie benötigen.

![GIMP-Screenshot](../assets/images/dietpi-software-desktop-tools-gimp.jpg){: width="960" height="587" loading="lazy"}

***

Website: <https://www.gimp.org>

### QuiteRSS

QuiteRSS ist ein plattformübergreifender Open-Source-Reader für RSS-/Atom-Newsfeeds mit der Hauptidee, für den Endbenutzer schnell und komfortabel zu sein.

![QuiteRSS-Screenshot](../assets/images/dietpi-software-desktop-tools-quiterss.jpg){: width="760" height="564" loading="lazy"}

### Xfce Power Manager

Ermöglicht Laptop-Benutzern, ein Energieprofil für zwei verschiedene Modi „im Akkubetrieb“ und „im Netzbetrieb“ einzurichten, während es Desktop-Benutzern weiterhin ermöglicht wird, zumindest die DPMS-Einstellungen und die CPU-Frequenz über den Einstellungsdialog zu ändern.

![Screenshot von Xfce Power Manager](../assets/images/dietpi-software-desktop-tools-xfce4-power-manager.jpg){: width="799" height="569" loading="lazy"}

[Zurück zur **Liste der optimierten Software**](../../software/)
