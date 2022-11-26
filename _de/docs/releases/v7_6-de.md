# Versionshinweise

## September 2021 (Version 7.6)

### Neue Software {: #new-software-76 }

- [Box64](../../software/gaming/#box64) :octicons-arrow-right-16: Mit diesem x86_64-Userspace-Emulator k�nnen Sie x86_64-Bin�rdateien auf einem ARMv8/arm64-System ausf�hren. Es funktioniert sehr �hnlich wie Box86, ist also in der Lage, gemeinsam genutzte arm64-Bibliotheken mit den x86_64-Bin�rdateien zu verwenden, sodass h�ufig keine zus�tzlichen Bibliotheken installiert werden m�ssen. Dank binfmt wird es automatisch aufgerufen, wenn versucht wird, eine x86_64-Bin�rdatei auszuf�hren. Vielen Dank an @ravenclaw900 f�r die Implementierung dieses Softwaretitels: <https://github.com/MichaIng/DietPi/pull/4625>
- [Dateibrowser](../../software/cloud/#file-browser) :octicons-arrow-right-16: Greifen Sie mit diesem leichten Remote-Dateimanager von �berall �ber den Browser auf Ihre Daten zu und verwalten Sie sie. Anders als ownCloud und Nextcloud greift es auf die Rohdaten in Ihrem Dateisystem zu, basierend auf einem ausgew�hlten Stammverzeichnis, was es �hnlich wie Syncthing macht. Sie k�nnen mehrere Benutzer mit ihrem eigenen Stammverzeichnis einrichten und auch das Teilen von Dateien und Verzeichnissen �ber einen passwortgesch�tzten Link ist m�glich.
- [Spotifyd](../../software/media/#spotifyd) :octicons-arrow-right-16: Spotifyd streamt Musik genau wie der offizielle Client, ist aber leichter. Es unterst�tzt auch das Spotify Connect-Protokoll, wodurch es als Ger�t angezeigt wird, das von den offiziellen Clients gesteuert werden kann. Vielen Dank an @ressu f�r die Implementierung dieses Softwaretitels: <https://github.com/MichaIng/DietPi/pull/4713>

### Verbesserungen {: #verbesserungen-76 }

- **Allgemein** :octicons-arrow-right-16: Erste Erkennung und Unterst�tzung f�r Debian 12 Bookworm (die neue "Test"-Version) wurde zu DietPi hinzugef�gt. Jeder ist eingeladen, ein Upgrade auf Bookworm durchzuf�hren, um auf dem neuesten Stand zu bleiben. Beachten Sie nur, dass aufgrund von anhaltenden Breaking Changes, die mit Paket-Upgrades einhergehen, einige Funktionen und Softwareinstallationen defekt sind oder werden. Wir freuen uns dann �ber Ihren Fehlerbericht, um notwendige �nderungen in DietPi so schnell wie bahnbrechende �nderungen in Bookworm zu implementieren, bis es die neue stabile Debian-Ver�ffentlichung wird, die im Sommer 2023 erwartet wird.
- **DietPi-FS_partition_resize** :octicons-arrow-right-16: Beim ersten Start erweitert DietPi automatisch die Root-Partition und das Dateisystem, um die volle Festplattengr��e abzudecken. Unter Umst�nden, zB bei �lteren Kernel-Versionen, kann es vorkommen, dass die beiden verwendeten Befehle `partprobe` und `partx -u` den Kernel nicht �ber die ge�nderte Partitionstabelle informieren und somit das Dateisystem nicht erweitert wird. In diesem Fall wird das System nun automatisch einmal neu gestartet, um sicherzustellen, dass die neue Partitionstabelle geladen und das Dateisystem anschlie�end erweitert wird. Diese �nderung betrifft nur neue Bilder, die DietPi v7.6 bereits enthalten, da diese Erweiterung durchgef�hrt wird, bevor DietPi sich selbst aktualisiert. Vielen Dank an @Dtrieb f�r die Meldung eines Falls, bei dem die Dateisystemerweiterung fehlgeschlagen ist: <https://github.com/MichaIng/DietPi/issues/4582>
- [DietPi-Drive_Manager](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Die native exFAT-Unterst�tzung von Linux wird jetzt erkannt und ber�cksichtigt, indem die Installation des veralteten FUSE-Treibers f�r den Fall �bersprungen wird. Zus�tzlich werden die neuen `exfatprogs` auf Bullseye installiert, geschrieben und implementiert mit Debian Bullseye zusammen mit der nativen Linux-exFAT-Implementierung.
- [DietPi-Drive_Manager](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: exFAT-Mounts haben jetzt den 775-Modus und geh�ren der "dietpi"-Gruppe, falls dies der Fall war nicht manuell entfernt. Wenn der FUSE-Treiber verwendet wird, haben Mounts standardm��ig den 777-Modus, sodass alle Benutzer vollen Zugriff haben, was aus Sicherheitsgr�nden nicht optimal ist. Bei nativer Linux exFAT-Unterst�tzung haben Mounts standardm��ig den 755-Modus, sodass die Download- und Media-Software-Implementierungen von DietPi-Software keinen Schreibzugriff haben. "775 root:dietpi" ist ein guter Kompromiss, wenn die Gruppe "dietpi" existiert und die Berechtigungen f�r Inhaltsverzeichnisse in `/mnt/dietpi_userdata` entsprechen. Vielen Dank an @K92Pi f�r die Meldung eines �hnlichen Problems: <https://github.com/MichaIng/DietPi/issues/4680>
- [DietPi-Drive_Manager](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Unterst�tzung f�r das Verschieben des Root-Dateisystems auf ein anderes Laufwerk auf Odroid N2 hinzugef�gt.
- [DietPi-AutoStart](../../dietpi_tools/#dietpi-autostart) :octicons-arrow-right-16: Eine neue Autostart-Option "Benutzerdefiniertes Skript (Vordergrund, mit automatischer Anmeldung)" wurde hinzugef�gt, die ausgef�hrt wird das benutzerdefinierte Skript `/var/lib/dietpi/dietpi-autostart/custom.sh` nach dem Einloggen mit dem gew�hlten Benutzer automatisch im Vordergrund auf dem Hauptbildschirm. Um es vern�nftiger zu trennen, wurde die vorherige Option f�r benutzerdefinierte Skripte in "Benutzerdefiniertes Skript (Hintergrund, keine automatische Anmeldung)" ge�ndert, das �ber den systemd-Dienst ausgef�hrt wird, unabh�ngig von jedem Anmeldestatus wie zuvor, aber nicht auf der Vordergrundkonsole gedruckt wird mehr. Stattdessen geht die Ausgabe an das Journal (journalctl -u dietpi-autostart_custom), wie es die meisten anderen systemd-Dienste tun. Der Vordergrundmodus verh�lt sich jetzt wie die meisten anderen Vordergrund-/GUI-Autostart-Optionen, startet nach der automatischen Anmeldung am Hauptbildschirm (`TTY1`) und kann, wenn es sich um einen lang andauernden Prozess handelt, mit `CTRL+C` abgebrochen werden, genau wie CAVA oder `DietPi-CloudShell`. Wenn man ein benutzerdefiniertes Skript im Vordergrund auf dem Hauptbildschirm vor/unabh�ngig von einer Anmeldung ausf�hren m�chte, ist es eine weitere Option, es in `/var/lib/dietpi/postboot.d/` zu platzieren. Alle enthaltenen Skripte werden am Ende des Bootvorgangs als Root-Benutzer auf dem Hauptbildschirm ausgef�hrt, ohne dass eine manuelle Anmeldung erforderlich ist. Vielen Dank an @scorgna f�r die Implementierung dieser Funktion: <https://github.com/MichaIng/DietPi/pull/4634>
- [DietPi-Software | **TigerVNC**](../../software/remote_desktop/#tigervnc-server) :octicons-arrow-right-16: Anstelle von `x11vnc` wird jetzt der TigerVNC-eigene Scraping-Server f�r den Shared-Desktop-Modus verwendet, der ist etwas leichter und teilt viele Bibliotheken mit dem eigenst�ndigen TigerVNC-Serverpaket.
- [DietPi-Software | **RealVNC**](../../software/remote_desktop/#realvnc-server) :octicons-arrow-right-16: Wenn die automatische Desktop-Anmeldung aktiviert ist, wird der Shared-Desktop-VNC-Modus nicht mehr erzwungen. Au�erdem ruft unser `vncserver.service` nicht RealVNC `vncserver-x11-serviced.service` f�r den Shared-Desktop-Modus auf, sondern stattdessen wird direkt die eigentliche ausf�hrbare `vncserver-x11`-Datei aufgerufen. Dies hat einige Vorteile, z. B. erm�glicht es, unseren Dienst f�r einen virtuellen Desktop zu verwenden, w�hrend der RealVNC-Dienst verwendet wird, um Verbindungen zum freigegebenen lokalen Desktop unabh�ngig zu erm�glichen. Vielen Dank an @K92Pi f�r diese Idee: <https://github.com/MichaIng/DietPi/issues/4672>
- [DietPi-Software | **RealVNC**](../../software/remote_desktop/#realvnc-server) :octicons-arrow-right-16: Der VNC-Server wird jetzt standardm��ig mit `VncAuth`-Authentifizierung gestartet, was jeden VNC-Viewer zul�sst zu verbinden, nicht nur RealVNC. Verwenden Sie `vncpasswd`, um das Passwort zu �ndern, das jetzt unabh�ngig von den UNIX-Benutzerpassw�rtern ist. Bei einer Neuinstallation wird standardm��ig das globale Softwarekennwort verwendet.
- [DietPi-Software | **Amiberry**](../../software/gaming/#amiberry) :octicons-arrow-right-16: Aufgrund von �nderungen in DietPi v7.5 �ndert das Aktivieren des Amiberry-Schnellstarts nicht die TTY f�r den Start /kernel auf Raspberry Pi nicht mehr, da sie die Amiberry-Bildschirmausgabe nicht mehr direkt st�ren. Aber aufgrund dieser �nderung ist bei �nderungen des Bildschirmmodus f�r kurze Zeit die rohe Konsolenausgabe sichtbar, was das Amiga-Feeling bricht. Um das Problem zu beheben, wechselt Amiberry jetzt, anstatt die Kernel-Befehlszeile (`cmdline`) zu �ndern, beim Start zu einem anderen leeren TTY und beim Stoppen zur�ck zum Haupt-TTY, einschlie�lich des Fehlerfalls. Da dies mit dem Amiberry-Dienst selbst erreicht wird, profitiert auch die standardm��ige Boot-Option von Amiberry davon, ebenso wie manuelle �systemctl start amiberry�-Aufrufe, und es ist nicht wie zuvor auf den Raspberry Pi beschr�nkt TTY-�nderung war. Vielen Dank an @zompiexx f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4692>
- **DietPi-Software | MPD** :octicons-arrow-right-16: Die Dienstdatei und die Standarddatei `mpd.conf` werden nicht mehr �berschrieben (ab Buster), sondern die erforderlichen �nderungen werden der Standarddatei hinzugef�gt, die mit dem Debian-Paket geliefert wird. Dies behebt einige Fehlermeldungen beim MPD-Start auf Bullseye und l�sst die meisten benutzerdefinierten �nderungen bei einer Neuinstallation unber�hrt. Dar�ber hinaus protokolliert MPD jetzt standardm��ig im Journal, auf das �ber `journalctl -u mpd` zugegriffen werden kann. Vielen Dank an @maartenlangeveld f�r das Melden der MPD-Startfehler: <https://github.com/MichaIng/DietPi/issues/4690>
- [DietPi-Software | **Kodi**](../../software/media/#kodi) :octicons-arrow-right-16: Unser Raspberry Pi-beschleunigtes Kodi-Paket wird jetzt auch auf ARMv7-RPi-Systemen installiert.

### Fehlerbehebungen {: #bug-fixes-76 }

- **Allgemein** :octicons-arrow-right-16: Es wurde ein Problem auf ARMv7-Buster- und Bullseye-Systemen behoben, bei dem der �haveged�-Entropie-Daemon aufgrund eingeschr�nkter Syscall-Berechtigungen abst�rzt. Dies kann zu mehreren Problemen f�hren, z. B. h�ngendem Start, h�ngenden Installationen oder Dienststarts. Vielen Dank an @jg777 f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4710>
- [DietPi-Drive_Manager](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Korrigierte falsche Informationen bei der Durchf�hrung einer exFAT-Dateisystempr�fung und -reparatur: Bis Stretch nur Pr�fung auf exFAT Fehler werden unterst�tzt, aber nicht repariert. Ab Buster wird beides voll unterst�tzt.
- [DietPi-Drive_Manager](../../dietpi_tools/#dietpi-drive-manager) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem auf Odroid C2 das Verschieben des Root-Dateisystems auf ein anderes Laufwerk fehlschlug. Vielen Dank an @yandritos f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4733>
- [DietPi-LetsEncrypt](../../dietpi_tools/#dietpi-letsencrypt) :octicons-arrow-right-16: Beim Aktivieren von HTTPS-Redirect oder HSTS und installierter ownCloud oder Nextcloud wird die `overwrite.cli.url` Die Einstellung in der `config.php` wird entsprechend aktualisiert, um die prim�re HTTPS-Domain zu enthalten. Dies ist f�r Cron-Jobs und die `occ/ncc`-Befehle erforderlich, um �ber den Webserver auf ownCloud/Nextcloud zuzugreifen, da das `Let's Encrypt`-Zertifikat nur f�r den externen Domainnamen und nicht f�r `localhost` g�ltig ist. Vielen Dank an @droogi f�r die Meldung eines m�glicherweise verwandten Problems: <https://github.com/MichaIng/DietPi/issues/4353>
- [DietPi-Software | **TigerVNC**](../../software/remote_desktop/#tigervnc-server) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem Remote-Verbindungen standardm��ig auf Bullseye-Systemen nicht funktionierten Konfigurationsdatei verwendet wird.
- [DietPi-Software | **LXDE**](../../software/desktop/#lxde) :octicons-arrow-right-16: Es wurde ein Problem auf Raspberry Pi behoben, bei dem der Aufruf von �lxappearance� (Look and Feel anpassen) aufgrund von Inkompatibilit�t fehlschlug RPi-Desktop-Pakete. Vielen Dank an @pinipon f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4687>
- [DietPi-Software | **LXDE**](../../software/desktop/#lxde) :octicons-arrow-right-16: Es wurde ein Problem mit Bullseye behoben, bei dem einige Symboldesigns aufgrund einer fehlenden SVG-Bibliothek nicht angewendet werden konnten. Vielen Dank an @pinipon f�r das Melden des Problems und der L�sung: <https://github.com/MichaIng/DietPi/issues/4687>
- [DietPi-Software | **LXDE**](../../software/desktop/#lxde) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Hotkey-Setup wegen eines fehlenden `openbox`-Plugins nicht funktionierte. Vielen Dank an @pinipon f�r das Melden des Problems und der L�sung: <https://github.com/MichaIng/DietPi/issues/4687>
- [DietPi-Software | **Blynk**](../../software/hardware_projects/#blynk-server): Es wurde ein Problem behoben, bei dem das Protokollverzeichnis m�glicherweise fehlt, was den Start des Dienstes unterbricht, wenn die Benutzerdaten von einem System zu einem migriert wurden ein neues. Vielen Dank an @Phil1988 f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4721>
- [DietPi-Software | **qBittorrent**](../../software/bittorrent/#qbittorrent) :octicons-arrow-right-16: Behebung eines Problems auf Bullseye-Systemen, bei dem die Anmeldung an der Weboberfl�che mit dem globalen Softwarepasswort seitdem nicht m�glich war der erforderliche Hash-Algorithmus hat sich ge�ndert. Vielen Dank an [phpBB:robex](https://dietpi.com/phpbb/memberlist.php?username=aftensleuk){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?p=22564#p22564>
- [DietPi-Software | **ReadyMedia**](../../software/media/#readymedia) :octicons-arrow-right-16: Es wurde ein Problem mit Bullseye behoben, bei dem der Dienst nicht gestartet wird, es sei denn, das Protokollverzeichnis wird manuell erstellt. Aufgrund eines Debian-Paket-Patches werden auf Bullseye Protokolle gezwungen, die Protokollierung erneut zu erstellen, sodass `/var/log/minidlna` erneut vorhanden sein muss. Vielen Dank an @AnzoP f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4745>

Wie immer wurden viele kleinere Codeleistungs- und Stabilit�tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code�nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4747>