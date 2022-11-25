# Heimautomatisierung

## �berblick

- [**Home Assistant - Open-Source-Hausautomatisierungsplattform, die auf Python 3 l�uft**](#home-assistant)
- [**Domoticz - Multi-Plattform-Hausautomationssystem**](#domoticz)
- [**TasmoAdmin - Verwaltungswebsite f�r Tasmota-Ger�te**](#tasmoadmin)

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

## Home-Assistent

Home Assistant ist eine Open-Source-Hausautomatisierungsplattform, die auf Python 3 l�uft. Verfolgen und steuern Sie alle Ger�te zu Hause und automatisieren Sie die Steuerung. Perfekt f�r den Betrieb auf einem Raspberry Pi.

![Home Assistant-Piktogramm](../assets/images/dietpi-software-homeautomation-homeassistant.png){: width="500" height="184" loading="lazy"}

=== "Erstinstallation und Zugriff"

    Der Installationsvorgang auf langsameren SBC-Modellen kann sehr lange dauern, bis zu 2 Stunden, also trinken Sie einen Kaffee, suchen Sie nach einer anderen Aktivit�t und schauen Sie ab und zu wieder vorbei. Es wird sehr lange Installing Python-3.xx.. angezeigt.
    Wenn Sie Verarbeitungsdetails sehen m�chten, f�hren Sie �htop� auf einem dedizierten Terminal oder einer SSH-Sitzung aus, um den Python-Build-Prozess live zu sehen.

    Nachdem `dietpi-software` fertig ist und der Dienst das erste Mal startet, f�hren Sie bitte die folgenden Schritte manuell durch:

    - F�hren Sie `htop` aus und warten Sie, bis die CPU-Auslastung der `homeassistant`-Prozesse auf nahezu Null gesunken ist.
    - F�hren Sie `systemctl restart home-assistant` aus
    - F�hren Sie `htop` aus und warten Sie, bis die CPU-Auslastung der `homeassistant`-Prozesse auf nahezu Null gesunken ist.
    - �ffnen Sie die HA-Weboberfl�che (siehe Registerkarte �Zugriff auf die Weboberfl�che�). Beim ersten Zugriff werden wieder einige Python-Module installiert, was wiederum eine Weile dauern kann. �berpr�fen Sie immer `htop`, wenn Sie sich nicht sicher sind, was einen aktuell laufenden Python/pip-Modul-Installationsprozess anzeigt.

=== "Zugriff auf die Weboberfl�che"

    Das Webinterface ist �ber Port **8123** erreichbar:

    URL = `http://<Ihre.IP>:8123`

=== "Konfigurationsdateien"

    Die Konfigurationsdateien werden systemweit gespeichert in:
    `/mnt/dietpi_userdata/homeassistant`

    Bitte beachten Sie die Online-Dokumentation: <https://home-assistant.io/docs/>

=== "Python-Umgebung anpassen"

    Home Assistant wird in einer dedizierten Python-Umgebung installiert, betrieben von: <https://github.com/pyenv/pyenv>.
    Dadurch wird eine eigenst�ndige Python-Instanz platziert, die v�llig unabh�ngig von anderen installierten Python-Instanzen oder -Modulen ausgef�hrt wird. Wenn Sie zus�tzliche Python-Module in dieser pyenv-Umgebung installieren, Python selbst aktualisieren oder �hnliches m�ssen, m�ssen Sie eine Shell als Benutzer �homeassistant� �ffnen und die pyenv-Umgebung aktivieren:

    ```sh
    sudo -u homeassistant bash
    . /home/homeassistant/pyenv-activate.sh
    pip3 install <module> # Or whichever install/update you need to do
    ```

=== "Home Assistant auf aktuelle Version aktualisieren"

    Um Home Assistant schnell auf die aktuelle Version zu aktualisieren, f�hren Sie Folgendes aus:

    ```sh
    /home/homeassistant/homeassistant-update.sh
    ```

=== "Bekannte zus�tzliche Abh�ngigkeiten f�r die Ger�teintegration"

    IKEA TR�DFRI: `apt install autoconf`

***

Offizielle Dokumentation: <https://home-assistant.io/docs>

## Domoticz

Domoticz ist ein Hausautomationssystem, mit dem Sie verschiedene Ger�te wie Lampen, Schalter, verschiedene Sensoren/Messger�te f�r Temperatur, Regen, Wind, UV-Strahlung, elektrische Felder, Gas, Wasser und vieles mehr �berwachen und konfigurieren k�nnen. Benachrichtigungen/Warnungen k�nnen an jedes mobile Ger�t gesendet werden.

![Screenshot der Domoticz-Weboberfl�che](../assets/images/dietpi-software-homeautomation-domoticz.jpg){: width="600" height="226" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    Das Webinterface ist �ber Port **8124** bzw. **8424**:

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

TasmoAdmin ist eine Verwaltungswebsite f�r mit Tasmota geflashte Ger�te, die f�r Smart-Home-Systeme verwendet werden sollen.

Installiert auch:

- Webserver (nach Ihren Vorlieben)
- PHP

![TasmoAdmin-Logo](../assets/images/dietpi-software-homeautomation-tasmoadmin.png){: width="302" height="184" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

`http://<Ihre.IP>/tasmoadmin`

***

Quellcode: <https://github.com/reloxx13/TasmoAdmin>
Credits: Implementiert von @svh1985

[Zur�ck zur **Liste der optimierten Software**](../../software/)
