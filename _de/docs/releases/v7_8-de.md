# Versionshinweise

## November 2021 (Version 7.8)

### �berblick

Diese Version f�gt DietPi eine wesentliche Verbesserung hinzu und bietet unser eigenes offizielles DietPi-Dashboard, um Ihre DietPi-Installationen sowohl zu **�berwachen als auch zu verwalten**. Es bietet auch volle Unterst�tzung f�r die neuesten Produkteinf�hrungen: **Raspberry Pi Zero 2 W** und **Radxa Zero SBCs** � zwei leistungsstarke und ultrakleine SBC-Varianten!

### Neue Software {: #new-software-78 }

- [**DietPi-Dashboard**](../../software/system_stats/#dietpi-Dashboard)
Wir sind stolz darauf, die offizielle DietPi-Webschnittstelle zur �berwachung und Verwaltung Ihres DietPi-Systems mit Ihrem Webbrowser anzuk�ndigen: octicons-heart-16:! Sie k�nnen verschiedene Statistiken sehen und sogar Befehle in der in die Webseite eingebetteten Konsole ausf�hren! Danke an die tolle Arbeit von @ravenclaw900!

![DietPi-Dashboard Screenshot](../assets/images/dietpi-dashboard.jpg){: width="700" height="346" loading="lazy"}

!!! Warnung "DietPi-Dashboard"

**Es befindet sich noch in der Betaphase**, da wir weitere Funktionen testen und nach und nach implementieren. Wir empfehlen daher noch nicht, in sensiblen Produktionssystemen aktiv zu verwenden.

Wir w�rden uns freuen, wenn Sie versuchen w�rden, es zu installieren, entweder mit der dietpi-Software oder mit dem Befehl in der Konsole:

�Sch
dietpi-software installieren 200
```

Bitte teilen Sie Ihr Feedback! Weitere Details finden Sie in der urspr�nglichen GitHub-Ausgabe: <https://github.com/MichaIng/DietPi/issues/448>

### Neue unterst�tzte SBCs {: #new-sbc-78 }

- [**Radxa Zero**](../../hardware/#radxa)
DietPi bietet Unterst�tzung f�r diesen winzigen Quad-Core-SBC. Es hat den gleichen Formfaktor wie Raspberry Pi Zero, ist aber viel leistungsf�higer. Dieser SBC wurde DietPi mit der Hardware-ID �74� hinzugef�gt. Vielen Dank an @almirus und @dhry f�r die Hilfe beim Testen und Debuggen eines fr�hen Images: <https://github.com/MichaIng/DietPi/issues/4831>

![DietPi Radxa Zero Foto](../assets/images/dietpi-radxa-zero.jpg){: width="500" height="281" loading="lazy"}

- [**Raspberry Pi Zero 2 W**](../../hardware/#raspberry-pi)
Der Raspberry Pi Zero 2 W bringt eine erh�hte Rechenleistung. Laut Raspberry sind Multithreading-Aufgaben bis zu f�nfmal schneller, was eine deutliche Steigerung darstellt, w�hrend genau der gleiche Formfaktor beibehalten wird.

![Raspberry Pi Zero 2 Foto](../assets/images/dietpi-raspberry-pi-zero-2.jpg){: width="500" height="333" loading="lazy"}

Mit dieser Version wurde die anf�ngliche DietPi-Unterst�tzung f�r diesen Raspberry Pi Zero / Zero W-Nachfolger hinzugef�gt. Es wird auch mit �bertaktungsprofilen geliefert, die hilfreich sind, um eine noch bessere Leistung zu erzielen. Es verwendet die Hardware-ID �3� (gemeinsam mit RPi 3/3+, da diese Version denselben Prozessor wie das urspr�ngliche Raspberry Pi 3 hat).

Vielen Dank an [phpBB:CassTG](https://dietpi.com/phpbb/memberlist.php?username=CassTG){: class="nospellcheck"} f�r die Bereitstellung der fr�hen Hardwareinformationen und die Durchf�hrung intensiver �bertaktungstests: <https: //dietpi.com/phpbb/viewtopic.php?t=9599>.

### Verbesserungen {: #verbesserungen-78 }

- [**DietPi-Backup**](../../dietpi_tools/#dietpi-backup-backuprestore)
- Eine Funktion wurde hinzugef�gt, um die t�gliche Systemsicherung per Cron-Job zu erm�glichen. Vielen Dank an @Lycidias93 f�r den Vorschlag dieser Funktion: <https://github.com/MichaIng/DietPi/issues/3871>
![DietPi Backup Daily](../assets/images/dietpi-backup-daily.png){: width="713" height="300" loading="lazy"}

- `Rsync` / �bertragungsprotokolle werden jetzt in `dietpi-backup.log` innerhalb des Backup-Verzeichnisses erstellt. So bleiben sie auch bei aktiviertem `DietPi-RAMlog` bestehen und k�nnen zu einem sp�teren Zeitpunkt eingesehen werden. Dies ist besonders hilfreich, wenn t�gliche Sicherungen per Cron-Job aktiviert sind, bei denen das Protokoll offensichtlich nicht direkt angezeigt wird, wenn die Sicherung abgeschlossen ist. Eine verwandte Option zum �berpr�fen des letzten �bertragungsprotokolls wurde dem Hauptmen� von dietpi-backup hinzugef�gt. Die alte Protokolldatei `/var/log/dietpi-backup.log` wird an den neuen Speicherort verschoben, wenn beim n�chsten DietPi-Update ein Backup vorhanden ist.
- Bei Verwendung eines NFS-Mounts als Sicherungsziel wird nun �berpr�ft, ob die NFS-Freigabe UNIX-Berechtigungen unterst�tzt, um die Erstellung einer fehlerhaften Systemsicherung von vornherein zu verhindern.

- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration)
- �bertaktungsprofile f�r die meisten Raspberry Pi-Modelle wurden **aktualisiert**, um den effektiven 100-MHz-ARM/CPU-Frequenzschritten zu entsprechen, die von der aktuellen Firmware verwendet werden.
- Bei einigen Modellen wurde ein **Energiesparprofil** hinzugef�gt, das minimale und maximale Spannung etwas reduziert, wodurch der Energieverbrauch und die W�rmeabgabe im Leerlauf und unter Last etwas reduziert werden.
![DietPi-�bertaktungsprofile](../assets/images/dietpi-overclocking-profiles.jpg){: width="744" height="300" loading="lazy"}
- Die Option, IPv4-Verbindungen zu bevorzugen, wenn IPv6 aktiviert ist, wurde entfernt: Dies funktionierte nur f�r APT und `wget`, w�hrend zB `cURL` und ping nie von dieser Einstellung betroffen waren, was zu einem inkonsistenten Verhalten f�hrte. Wenn bei aktiviertem IPv6 Probleme auftreten, sollte es einfach deaktiviert werden, anstatt IPv4 nur f�r bestimmte Tools zu bevorzugen/zu erzwingen.

- [**DietPi-Drive_Manager**](../../dietpi_tools/#dietpi-drive-manager)
- Beim �bertragen der DietPi-Benutzerdaten auf ein anderes Laufwerk wird nun gepr�ft, ob sich der Zielort innerhalb eines unterst�tzten Dateisystemtyps befindet, eines mit nativem Symlink und UNIX-Berechtigungsunterst�tzung. Das Gleiche geschieht bei Verwendung des CLI-Skripts `/boot/dietpi/func/dietpi-set_userdata`.
- Die �bertragung des Root-Dateisystems wird jetzt auf Odroid C4/HC4-Modellen unterst�tzt.
- Die Option zum �bertragen des Root-Dateisystems wird nun auch angezeigt, wenn das Laufwerk kein Dateisystem enth�lt. Der Prozess impliziert sowieso eine Formatierung mit einem unterst�tzten Dateisystem, wodurch die Bedingung obsolet wird. Au�erdem ist es nicht mehr erforderlich, das Dateisystem zuerst manuell auszuh�ngen, da dies automatisch vor dem Formatieren erfolgt. Im zugeh�rigen Formatmen� werden nur unterst�tzte Dateisysteme aufgelistet, also ext4 und zus�tzlich F2FS auf dem Raspberry Pi. Das Eingabefeld zur Eingabe eines benutzerdefinierten Einh�ngepunkts entf�llt, da es nur vor�bergehend verwendet wird, bis die �bertragung des Root-Dateisystems abgeschlossen ist. Die Auslagerungsdatei wird nicht mehr deaktiviert, da sie ohne Probleme kopiert und unver�ndert auf dem neuen Root-Dateisystem wiederverwendet werden kann.
- Beim �bertragen des Root-Dateisystems werden weitere Pr�fungen durchgef�hrt: Es muss eine dedizierte Boot-Partition vorhanden sein (erforderlich auf Raspberry Pi und standardm��ig auf unseren aktuellen Odroid-Images), da dies die �bertragungsschritte erwarten und der einzige Grund f�r das Verschieben nur der Root-Dateisystem, anstatt das gesamte Laufwerk zu klonen oder das DietPi-Image �berhaupt auf ein externes Laufwerk zu flashen. Die erwarteten Boot-/Kernel-Konfigurationsdateien m�ssen vorhanden sein, damit der Kernel angewiesen werden kann, das neue Root-Dateisystem einzuh�ngen. Die DietPi-Benutzerdaten d�rfen sich derzeit nicht auf der Zielpartition befinden, da diese formatiert w�rden und somit alle Daten verloren gingen.
- Auf ext4-Dateisystemen wird jetzt der Prozentsatz der reservierten Bl�cke angezeigt und kann auch ge�ndert werden, wenn das Laufwerk derzeit nicht gemountet ist.

- [**DietPi-RAMlog**](../../software/log_system/#dietpi-ramlog) :octicons-arrow-right-16: Die `/var/log`-Verzeichnisstruktur wird jetzt mit der persistenten Festplattenspeicher nach Softwareinstallationen und �ber t�gliche Cron-Jobs, um fehlende Protokolldateien oder Verzeichnisse bei unsauberem Herunterfahren zu verhindern, was normalerweise zu fehlgeschlagenen Dienststarts f�hrt.
- [DietPi-Software | **Roon Server**](../../software/media/#roon-server) :octicons-arrow-right-16: Unterst�tzung f�r die neue .NET-Core-basierte Version hinzugef�gt, die am 3 Es wird erwartet, dass die Leistung im Vergleich zur alten Mono-basierten Version verbessert wurde. Um ein altes Problem mit unserer Roon-Server-Implementierung (siehe unten) zu beheben, wird w�hrend des DietPi-Updates eine Neuinstallation durchgef�hrt, die auch die .NET-Core-Abh�ngigkeiten mit einbezieht. Dies wird jedoch NICHT die Roon Server-Version aktualisieren, um Probleme mit m�glicherweise erforderlichen Migrationsschritten zu vermeiden. Verwenden Sie nach dem Update von DietPi den internen Updater von Roon, um von der neuen Version zu profitieren.

### Fehlerbehebungen {: #bug-fixes-78 }

- [**Raspberry Pi**](../../hardware/#raspberry-pi) :octicons-arrow-right-16: Umgehung eines Problems auf Raspberry Pi ARMv6/7 Bullseye-Systemen, bei dem einige Software nicht gestartet werden konnte , zB RealVNC, wenn Bin�rdateien gegen eine �ltere `libraspberrypi0`-Version mit anderen gemeinsam genutzten Bibliotheksnamen kompiliert wurden.
- [**DietPi-Drive_Manager**](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Gr��en�nderung von F2FS-Dateisystemen fehlschlug, wenn sie aktuell gemountet waren. Im Gegensatz zu den Dokumenten und der Fehlerausgabe reicht es nicht aus, das Dateisystem schreibgesch�tzt zu mounten, sondern es muss stattdessen ausgeh�ngt werden, was jetzt vor der Gr��en�nderung automatisch erfolgt und danach wieder eingeh�ngt wird.
- [**DietPi-Drive_Manager**](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Gr��en�nderung von ext4-Dateisystemen fehlschlagen konnte, wenn sie derzeit nicht gemountet waren. Insbesondere wenn das Laufwerk neu angeschlossen wird, muss ein vollst�ndiges `fsck` einmal durchgef�hrt werden, bevor die Gr��e ge�ndert werden kann. Dies geschieht jetzt automatisch, sodass Dateisystemfehler interaktiv behoben werden k�nnen, bevor die Gr��e eines Offline-ext4-Dateisystems ge�ndert wird.
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem �bertaktungsprofile f�r Raspberry Pi 4 auf Raspberry Pi 400 angeboten wurden. A Neue Profile wurden jetzt speziell f�r den Raspberry Pi 400 hinzugef�gt.
- [DietPi-Software | **IceCast**](../../software/media/#icecast) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem eine Neuinstallation aufgrund eines versuchten Vorgangs an einer nicht vorhandenen Datei fehlschlug. Vielen Dank an @killtux f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4858>
- [DietPi-Software | **Logitech Media Server**](../../software/media/#logitech-media-server) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Deinstallation fehlschlug, als das Skript �postinst� des Pakets versuchte um den Dienstbenutzer zu entfernen, bevor der Dienst beendet wurde.
- [DietPi-Software | **Roon Server**](../../software/media/#roon-server) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der interne Updater alle Daten und Konfigurationen von Roon Server gel�scht hat, da die Daten Verzeichnis befand sich innerhalb des Installationsverzeichnisses. Roon Server wird nun nach `/opt/roonserver` installiert, w�hrend das Datenverzeichnis unter `/mnt/dietpi_userdata/roonserver` verbleibt. Diese �nderung wird auch �ber das DietPi-Update angewendet, Ihre Daten und Konfigurationen bleiben unber�hrt. Vielen Dank an @JanKoudijs f�r die Meldung dieses Problems und die Bereitstellung einer L�sung: <https://github.com/MichaIng/DietPi/pull/4897>
- [DietPi-Software | **LXDE**](../../software/desktop/#lxde) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem in einigen F�llen beim ersten Desktop-Start Desktop-Symbole fehlten, und ein weiteres Problem bei Bullseye Systemen, bei denen beim Desktop-Start die Fehlermeldung �No session for pid� auftauchte. Vielen Dank an @kerryland f�r das Melden dieser Probleme: <https://github.com/MichaIng/DietPi/issues/4914>
- [DietPi-Software | **LXDE**](../../software/desktop/#lxde) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Firefox-Browser-Bedienfeldsymbol vorhanden war, selbst wenn kein Firefox installiert war. In diesem Fall wird nun entweder Chromium oder der Texteditor als Ersatz hinzugef�gt.
- [DietPi-Software | **Home Assistant**](../../software/home_automation/#home-assistant) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation auf ARMv6/ARMv7 Bullseye-Systemen fehlschlug.
- [DietPi-Software | **Tor Relay**](../../software/distributed_projects/#tor-relay) :octicons-arrow-right-16: Diese Softwareoption wurde auf Stretch deaktiviert. Das vom Debian-Stretch-Repository gelieferte Tor-Paket ist zu alt, um die erforderlichen Protokolle des Tor-Netzwerks zu unterst�tzen, wenn ein Relay ausgef�hrt wird. Vielen Dank an @cptechnik f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4925>
- [DietPi-Software | **Deluge**](../../software/bittorrent/#deluge) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem bei Neuinstallationen die Dienste aufgrund einer ung�ltigen Konfigurationsdateisyntax fehlschlugen. Vielen Dank an [phpBB:bookedirl](https://dietpi.com/phpbb/memberlist.php?username=bookedirl){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?t=9553>
- [DietPi-Software | **Deluge**](../../software/bittorrent/#deluge) :octicons-arrow-right-16: Da das Paket von Raspbian Bullseye derzeit fehlschl�gt, mussten wir Deluge f�r Raspberry Pi-Systeme mit ARMv6 Bullseye deaktivieren Bild. Der Fehler wurde den Raspbian-Maintainern gemeldet und wir hoffen auf eine Behebung bis zum n�chsten DietPi-Release: <https://github.com/MichaIng/DietPi/issues/4944>
- [DietPi-Software | **Lighttpd**](../../software/webserver_stack/#lighttpd) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem Neuinstallationen auf einem Bullseye-System mit verwendetem DietPi-LetsEncrypt f�lschlicherweise eine SSL-Konfiguration aktivierten, die k�nnte den Dienststart verhindern.

Wie immer wurden viele kleinere Codeleistungs- und Stabilit�tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code�nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4951>

### Entfernte Software {: #removed-software-78 }

- **Subsonic** :octicons-arrow-right-16: Da es nicht mehr weiterentwickelt wird und aufgrund von Shared-Library-Abh�ngigkeiten nur mit Debian Stretch kompatibel ist, haben wir Subsonic aus der DietPi-Software entfernt. Mit Airsonic-Advanced stellen wir in K�rze eine gut gepflegte und Bullseye-kompatible Alternative zur Verf�gung. Wenn Sie derzeit Subsonic installiert haben, bleibt es bestehen. Wenn Sie es deinstallieren m�chten, folgen Sie den Anweisungen hier: <https://github.com/MichaIng/DietPi/pull/4895>
- **emonHub** :octicons-arrow-right-16: Da wir keine einzige gemeldete Installation haben, haben wir emonHub aus der DietPi-Software entfernt. Wenn Sie derzeit emonHub installiert haben, bleibt es bestehen. Wenn Sie es weiterhin verwenden und aktualisieren m�chten, werfen Sie einen Blick auf das offizielle Repository unter <https://github.com/openenergymonitor/emonhub>. Wenn Sie es deinstallieren m�chten, folgen Sie den Anweisungen hier: <https://github.com/MichaIng/DietPi/pull/4895>

### Unterst�tzter SBC entfernt {: #removed-SBC-78 }

- **Odroid N1** :octicons-arrow-right-16: Es gibt kein einziges gemeldetes DietPi Odroid N1-System, was Sinn macht, da dieses Modell nie wirklich ver�ffentlicht wurde. Nur eine kleine Anzahl von Entwicklerbeispielen schwimmt herum, es lohnt sich nicht, ein Image und einen dedizierten Code zu pflegen. Wenn es da drau�en nicht gemeldete Odroid N1 DietPi-Systeme gibt, werden sie beim DietPi-Update automatisch auf die generische Rockchip RK3399-Ger�te-ID migriert.
