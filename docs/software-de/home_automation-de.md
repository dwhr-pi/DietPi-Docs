# Heimautomatisierung

## Überblick

- [**Home Assistant - Open-Source-Hausautomatisierungsplattform, die auf Python 3 läuft**](#home-assistant)
- [**Domoticz - Multi-Plattform-Hausautomationssystem**](#domoticz)
- [**TasmoAdmin - Verwaltungswebsite für Tasmota-Geräte**](#tasmoadmin)

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

## Home-Assistent

Home Assistant ist eine Open-Source-Hausautomatisierungsplattform, die auf Python 3 läuft. Verfolgen und steuern Sie alle Geräte zu Hause und automatisieren Sie die Steuerung. Perfekt für den Betrieb auf einem Raspberry Pi.

![Home Assistant-Piktogramm](../assets/images/dietpi-software-homeautomation-homeassistant.png){: width="500" height="184" loading="lazy"}

=== "Erstinstallation und Zugriff"

    Der Installationsvorgang auf langsameren SBC-Modellen kann sehr lange dauern, bis zu 2 Stunden, also trinken Sie einen Kaffee, suchen Sie nach einer anderen Aktivität und schauen Sie ab und zu wieder vorbei. Es wird sehr lange Installing Python-3.xx.. angezeigt.
    Wenn Sie Verarbeitungsdetails sehen m&ouml;chten, führen Sie `htop` auf einem dedizierten Terminal oder einer SSH-Sitzung aus, um den Python-Build-Prozess live zu sehen.

    Nachdem `dietpi-software` fertig ist und der Dienst das erste Mal startet, führen Sie bitte die folgenden Schritte manuell durch:

    - Führen Sie `htop` aus und warten Sie, bis die CPU-Auslastung der `homeassistant`-Prozesse auf nahezu Null gesunken ist.
    - Führen Sie `systemctl restart home-assistant` aus
    - Führen Sie `htop` aus und warten Sie, bis die CPU-Auslastung der `homeassistant`-Prozesse auf nahezu Null gesunken ist.
    - &Ouml;ffnen Sie die HA-Weboberfläche (siehe Registerkarte `Zugriff auf die Weboberfläche`). Beim ersten Zugriff werden wieder einige Python-Module installiert, was wiederum eine Weile dauern kann. Überprüfen Sie immer `htop`, wenn Sie sich nicht sicher sind, was einen aktuell laufenden Python/pip-Modul-Installationsprozess anzeigt.

=== "Zugriff auf die Weboberfläche"

    Das Webinterface ist über Port **8123** erreichbar:

    URL = `http://<Ihre.IP>:8123`

=== "Konfigurationsdateien"

    Die Konfigurationsdateien werden systemweit gespeichert in:
    `/mnt/dietpi_userdata/homeassistant`

    Bitte beachten Sie die Online-Dokumentation: <https://home-assistant.io/docs/>

=== "Python-Umgebung anpassen"

    Home Assistant wird in einer dedizierten Python-Umgebung installiert, betrieben von: <https://github.com/pyenv/pyenv>.
    Dadurch wird eine eigenständige Python-Instanz platziert, die v&ouml;llig unabhängig von anderen installierten Python-Instanzen oder -Modulen ausgeführt wird. Wenn Sie zusätzliche Python-Module in dieser pyenv-Umgebung installieren, Python selbst aktualisieren oder ähnliches müssen, müssen Sie eine Shell als Benutzer `homeassistant` &ouml;ffnen und die pyenv-Umgebung aktivieren:

    ```sh
    sudo -u homeassistant bash
    . /home/homeassistant/pyenv-activate.sh
    pip3 install <module> # Or whichever install/update you need to do
    ```

=== "Home Assistant auf aktuelle Version aktualisieren"

    Um Home Assistant schnell auf die aktuelle Version zu aktualisieren, führen Sie Folgendes aus:

    ```sh
    /home/homeassistant/homeassistant-update.sh
    ```

=== "Bekannte zusätzliche Abhängigkeiten für die Geräteintegration"

    IKEA TRÅDFRI: `apt install autoconf`

***

Offizielle Dokumentation: <https://home-assistant.io/docs>

## Domoticz

Domoticz ist ein Hausautomationssystem, mit dem Sie verschiedene Geräte wie Lampen, Schalter, verschiedene Sensoren/Messgeräte für Temperatur, Regen, Wind, UV-Strahlung, elektrische Felder, Gas, Wasser und vieles mehr überwachen und konfigurieren k&ouml;nnen. Benachrichtigungen/Warnungen k&ouml;nnen an jedes mobile Gerät gesendet werden.

![Screenshot der Domoticz-Weboberfläche](../assets/images/dietpi-software-homeautomation-domoticz.jpg){: width="600" height="226" loading="lazy"}

=== "Zugriff auf die Weboberfläche"

    Das Webinterface ist über Port **8124** bzw. **8424**:

    - HTTP: `http://<Ihre.IP>:8124`
    - HTTPS: `https://<your.IP>:8424`

=== "Protokolle anzeigen"

    ```sh
    journalctl -u domoticz
    ```

=== "Serviceabwicklung"

    Verwenden Sie die folgenden Befehle, um den Domoticz-Systemdienst zu steuern:

    ```sh
    systemctl status domoticz
    ```

    ```sh
    systemctl stop domoticz
    ```

    ```sh
    systemctl start domoticz
    ```

    ```sh
    systemctl restart domoticz
    ```

=== "Installationsverzeichnis"

    `/opt/domoticz`

=== "Datenverzeichnis"

    `/mnt/dietpi_userdata/domoticz`

***

Quellcode: <https://github.com/domoticz/domoticz>

## TasmoAdmin

TasmoAdmin ist eine Verwaltungswebsite für mit Tasmota geflashte Geräte, die für Smart-Home-Systeme verwendet werden sollen.

Installiert auch:

- Webserver (nach Ihren Vorlieben)
- PHP

![TasmoAdmin-Logo](../assets/images/dietpi-software-homeautomation-tasmoadmin.png){: width="302" height="184" loading="lazy"}

=== "Zugriff auf die Weboberfläche"

`http://<Ihre.IP>/tasmoadmin`

***

Quellcode: <https://github.com/reloxx13/TasmoAdmin>
Credits: Implementiert von @svh1985

[Zurück zur **Liste der optimierten Software**](../../software/)
