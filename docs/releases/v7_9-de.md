# Versionshinweise

## Dezember 2021 (Version 7.9)

### �berblick

Willkommen zur **Ver�ffentlichung vom Dezember 2021** :octicons-heart-16: von **DietPi**. Es aktiviert den Passwortschutz f�r [**DietPi-Dashboard**](../../software/system_stats/#dietpi-dashboard), [**DietPi-Backup**](../../dietpi_tools/ #dietpi-backup-backuprestore) beginnt mehrere Backups zu unterst�tzen und der **[Apache](../../software/webserver_stack/#apache)** Webserver verwendet den dedizierten `PHP-FPM`-Server, was die Gesamtleistung verbessert . Und vieles mehr.

### Bekanntmachung

!!! Warnung �**Debian �Stretch�-Unterst�tzung**�

Debian 9 �Stretch� wurde 2017 ver�ffentlicht und wurde zun�chst von Debian 10 �Buster� und dann von Debian 11 �Bullseye� abgel�st.

**DietPi v7.9 wird die letzte Version mit Unterst�tzung f�r Debian Stretch sein**. Die n�chste Version wird **DietPi v8.0** sein und erfordert Debian Buster oder neuer.

Lesen Sie unseren Artikel [**Warum Sie Ihr Stretch-System jetzt aktualisieren sollten**] (https://dietpi.com/blog/?p=1001), um mehr �ber die Notwendigkeit dieses Upgrades zu erfahren und wie Sie dies ganz einfach tun k�nnen Debian Buster und noch weiter bis zur neuesten Version (**Debian Bullseye**).

### Verbesserungen {: #verbesserungen-79 }

- [**DietPi-Dashboard**](../../software/system_stats/#dietpi-Dashboard)
- Bei Neuinstallationen ist der Passwortschutz jetzt standardm��ig aktiviert und verwendet das **globale Softwarepasswort**.

![DietPi-Dashboard-Passwort](../assets/images/dietpi-dashboard-login.jpg){: width="800" height="576" loading="lazy"}

Sie k�nnen dies manuell anwenden oder �ndern, indem Sie den Anweisungen in unserer [Dokumentation](../../software/system_stats/#dietpi-dashboard) folgen.

- Der Standard-TCP-Netzwerkport wurde von �8088� auf �5252� ge�ndert, um einen Portkonflikt mit InfluxDB zu l�sen. Wenn Sie DietPi-Dashboard bereits installiert haben, werden Sie gefragt, ob Sie diese �nderung w�hrend des Updates �bernehmen m�chten.

![DietPi-Dashboard Standardport](../assets/images/dietpi-dashboard-port-change.jpg){: width="800" height="252" loading="lazy"}

Vielen Dank an @blablazzz f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4966>

- [**DietPi-Backup**](../../dietpi_tools/#dietpi-backup-backuprestore)
- Es kann jetzt ein Backup-Archiv mit einer w�hlbaren Anzahl von zu behaltenden Backups erstellt werden. Backups werden automatisch rotiert und wenn die maximale Menge erreicht ist, wird das �lteste Backup als Grundlage f�r die inkrementelle neue Backup-Synchronisierung verwendet, um Schreibvorg�nge zu reduzieren und die Geschwindigkeit zu erh�hen.

![DietPi-Sicherungsmenge](../assets/images/dietpi-Sicherungsmenge.jpg){: width="800" height="265" loading="lazy"}

Vielen Dank an [phpBB:johnvick](https://dietpi.com/phpbb/memberlist.php?username=johnvick){: class="nospellcheck"} und viele andere f�r die Anfrage nach dieser Funktion [im DietPi-Forum](https ://dietpi.com/phpbb/viewtopic.php?t=3593).

- Backups k�nnen jetzt au�erhalb von `/mnt` in jedem Verzeichnis oder Einh�ngepunkt gespeichert werden, solange das Dateisystem `symlinks` und UNIX-`Berechtigungen` unterst�tzt.
� Es wurde ein Problem behoben, bei dem Sicherung und Wiederherstellung fehlschlugen, wenn ein nicht standardm��iger Sicherungsspeicherort verwendet wurde, da ein falscher Protokolldateipfad verwendet wurde. Dies ist eine v7.8-Regression. Vielen Dank an [phpBB:Malinka](https://dietpi.com/phpbb/memberlist.php?username=Malinka){: class="nospellcheck"} f�r die Meldung dieses Problems [im DietPi-Forum](https:// dietpi.com/phpbb/viewtopic.php?p=39909#p39909).

- [**Himbeer-Pi**](../../hardware/#raspberry-pi)
- Seit Bullseye verwenden einige Mediensoftwaretitel, vor allem `FFmpeg` und solche, die `FFmpeg`-Bibliotheken verwenden, die f�r die Raspberry Pi-Firmware kompiliert wurden (**Kodi**, **Jellyfin**, **Chromium**), Verwendung die Raspberry Pi V4L2-Codec-Treiber. Diese wurden zuvor mit dem RPi-Kameramodulschalter in dietpi-config aktiviert/deaktiviert. Die Hardware-Codec-Treiber sind nun zu einem eigenen CLI-Befehl und Men�schalter in den Anzeigeoptionen der dietpi-config geworden und werden automatisch aktiviert, wenn einer der genannten Softwaretitel auf Bullseye (oder h�her) installiert oder neu installiert wird.

- **DietPi-Software** | **[SABnzbd](../../software/bittorrent/#sabnzbd)**
- Bei Neuinstallationen wurde die Dateiprotokollierung zugunsten der Journalprotokollierung deaktiviert. Alle Dienst- und Prozessprotokolle k�nnen daher jetzt �berpr�ft werden �ber: `journalctl -u sabnzbd`
� Behebung eines Problems, bei dem Installationen auf ARMv6- und ARMv7-Stretch-Systemen fehlschlugen. Vielen Dank an @bensp f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4997>.

- **DietPi-Software** | **[Apache](../../software/webserver_stack/#apache)**
- Neuinstallationen und Neuinstallationen werden mit `PHP-FPM` anstelle von `mod_php` konfiguriert. Als Voraussetzung wird statt Prefork das Event `MPM` verwendet. Dies reduziert die Speichernutzung und erh�ht die Zugriffsleistung bei gleichzeitigen Anfragen erheblich, da der Apache-Elternprozess nicht f�r jeden einzelnen Prozess einen neuen Kindprozess forken muss.
- Es wird weiter optimiert, indem nur ein einziger statischer untergeordneter Prozess erzeugt wird, w�hrend gleichzeitige Anforderungen von einer ausreichenden Anzahl von Prozess-Threads verarbeitet werden. Dies erm�glicht Apache, Speicher effizient zu teilen und macht es ziemlich leicht. Es sind keine Nachteile bekannt, wenn nur ein einzelner Prozess verwendet wird, im Vergleich zu mehreren Prozessen mit jeweils weniger Threads. Weitere Informationen finden Sie in den verwandten Fragen und Antworten zu StackExchange: [StackExchange - Apache2 MPM event: More threads vs more processes?](https://superuser.com/questions/1611015/apache2-mpm-event-more-threads-vs-more- Prozesse)
- Die Standard-/Basiskonfiguration wird jetzt als separate Datei hinzugef�gt, sodass die Hauptdatei `apache2.conf` nicht mehr ber�hrt wird. Au�erdem wird der standardm��ige �vhost� jetzt vor der Paketinstallation vorab erstellt, sodass er bei einer Neuinstallation �bersprungen werden kann, um benutzerdefinierte Einstellungen nicht zu �berschreiben. Diese in Kombination erm�glichen eine sichere und saubere Neuinstallation, ohne vom Administrator vorgenommene �nderungen zu besch�digen, mit der kleinen Ausnahme, dass das Webroot auf `/var/www` gesetzt ist, was f�r alle unsere Softwareoptionen erforderlich ist, die einen externen Webserver verwenden .
- Die neue Standardkonfiguration bietet maximale Datenschutzeinstellungen und Sicherheitsheader. Es ist einfach, diese mit eigenen Konfigurationen auf `vhost`- oder Verzeichnisebene zu �berschreiben.
- Die Protokollierung erfolgt jetzt standardm��ig im Journal, und Sie k�nnen sie anzeigen, indem Sie den n�chsten Befehl ausf�hren:

�Sch
journalctl -u apache2
```

- Die Direktive �ServerName� wird mit der **lokalen IP** hinzugef�gt, um entsprechende Startwarnungen stummzuschalten.
Dies kann zu Zugriffs- und CORS-Fehlern f�hren, wenn Anwendungen den Servernamen als zul�ssigen Hostnamen pr�fen, aber andere externe IPs/Hostnamen f�r den Zugriff verwendet wurden. In einem solchen Fall bieten Anwendungen im Allgemeinen eine M�glichkeit, eine Liste zul�ssiger Hostnamen zu definieren. Ohne einen festgelegten Servernamen wendet der Webserver normalerweise einfach den `HTTP_HOST`-Header an, der jede damit verbundene �berpr�fung umgeht. Laut der protokollierten Warnung scheint Apache dann `127.0.1.1` zu verwenden.

- **DietPi-Software** | [**Kodi**](../../software/media/#kodi)
- Auf **Raspberry Pi Bullseye**-Systemen ist jetzt das neue offizielle **Raspberry Pi**-Repository-Build f�r Kodi 19.3 installiert. Sie k�nnen das Upgrade manuell anwenden, indem Sie Kodi neu installieren.

�Sch
dietpi-software neu installieren 31
```

- Das Addon-Repository wird jetzt standardm��ig bei allen Kodi-Installationen installiert, was zuvor nur bei RPi und Odroids der Fall war. Wenn es derzeit fehlt, kann es manuell installiert werden

�Sch
apt installiere kodi-repository-kodi
```

- **DietPi-Software** | [**Gitea**](../../software/cloud/#gitea)
- Der Dienst l�uft jetzt als dedizierter Benutzer `gitea` mit seinem Heimatverzeichnis `/mnt/dietpi_userdata/gitea`, um eine einfache �bertragung und Verwendung von SSH-Schl�sseln f�r den Fernzugriff zu erm�glichen. Dies gilt f�r neu installierte oder neu installierte Gitea-Instanzen. Vielen Dank an @LilTrublMakr f�r die Meldung der damit verbundenen Einschr�nkung mit dem zuvor verwendeten `dietpi`-Benutzer: <https://github.com/MichaIng/DietPi/issues/4620>.
- [**Gitea**](../../software/cloud/#gitea) und [**Gogs**](../../software/cloud/#gogs) kollidieren miteinander, da beide Verwenden Sie standardm��ig den Port "3000". DietPi verwendet ein neues Konfliktmanagementsystem, um zu verhindern, dass beide gleichzeitig installiert werden.

- **DietPi-Software** | [**Chromium**](../../software/desktop/#chromium) :octicons-arrow-right-16: Auf Raspberry Pi wird nun das Paket `chromium-codecs-ffmpeg-extra` zusammen mit installiert Chromium, das zus�tzliche Codecs f�r patentierte Video-/Audioformate hinzuf�gt. Vielen Dank an @Krawei f�r die Identifizierung dieser Chromium-Videowiedergabeverbesserung � siehe <https://github.com/MichaIng/DietPi/issues/5013>.

- **DietPi-Software** | [**rTorrent**](../../software/bittorrent/#rtorrent) :octicons-arrow-right-16: Bei Neuinstallationen lauscht rTorrent jetzt standardm��ig auf **TCP-Port 49164** auf eingehende BitTorrent Verbindungen. Abgesehen von `DHT` war das Lauschen auf eingehende Verbindungen zuvor komplett deaktiviert, was je nach verwendetem Tracker zu langsamen oder gar keinen Peer-Verbindungen f�hrte. Vielen Dank an @Camry2731 f�r die Meldung dieser Inkonsistenz mit unseren anderen BitTorrent-Serveroptionen.

- **DietPi-Software** - **Dateiserver** :octicons-arrow-right-16: Dieses Auswahlmen� wurde aus der DietPi-Software entfernt, da die meisten Dateiserver gleichzeitig laufen k�nnen. Somit ist es nicht mehr erforderlich, zuerst den bestehenden Dateiserver (zB einen Samba-Server) zu entfernen und dann etwas Neues (zB einen FTP-Server) zu installieren. Dadurch ist kein dedizierter Men�punkt in der DietPi-Software notwendig.

Dateiserver k�nnen �ber die Men�s �Browse Software� oder �Search Software� in �dietpi-software� oder �ber CLI ausgew�hlt werden. Siehe die Dokumentation f�r die verf�gbaren [DietPi-Dateiserver] (../../software/file_servers/).

![DietPi-Software](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

Die zugeh�rige `dietpi.txt`-Einstellung wurde auch f�r neue Bilder entfernt, aber sie wird immer noch ber�cksichtigt, wenn sie vorhanden ist. Verwenden Sie f�r eine automatische Installation mit neuen Images stattdessen die Einstellung �AUTO_SETUP_INSTALL_SOFTWARE_ID�.

- **DietPi-Dokumentation** | [**Anleitung**](../../usage/#how-to-do-an-automatic-base-installation-at-first-boot-dietpi-automation) :octicons-arrow-right-16 : Abschnitt hinzugef�gt, der die **automatische Basisinstallation beim ersten Booten** �ber die Datei `/boot/dietpi.txt` (DietPi-Automation) beschreibt.

### Fehlerbehebungen {: #bug-fixes-79 }

- [**Raspberry Pi**](../../hardware/#raspberry-pi) :octicons-arrow-right-16: Es wurde ein Problem in den DietPi-Images behoben, bei dem beim ersten Booten zwei serielle Anmeldekonsolen auf dem generischen `symlinked` und tats�chliche serielle Ger�te k�nnten gestartet worden sein. Dies verdoppelte die Eingaben und brach beim ersten Start die erfolgreiche Anmeldung mit �Benutzername� und �Passwort� �ber die serielle Konsole. Vielen Dank an @ad7718 f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5014>.
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration)
� Es wurde ein Problem behoben, bei dem die Aktivierung des LCD-Panels �odroid-lcd35� auf Odroids fehlschlug, da SPI standardm��ig aktiviert ist und dieselben GPIO-Ports blockiert. Vielen Dank an @MarcProux f�r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/4154>.
� Es wurde ein Problem behoben, bei dem das Netzwerkadaptermen� die statischen DNS-Server nicht angezeigt hat, die effektiv beim ersten Start basierend auf den Einstellungen von �dietpi.txt� angewendet wurden. Vielen Dank an @nils-trubkin f�r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/5054>.
- **DietPi-Software** :octicons-arrow-right-16: Eine DietPi v7.8-Regression behoben, bei der [ReadyMedia](../../software/media/#readymedia), [Deluge](../ ../software/bittorrent/#deluge), [Sonarr](../../software/bittorrent/#sonarr) und [Jellyfin](../../software/media/#jellyfin) Installationen schlugen mit einem fehl Fehler auf `usermod`, da die Dienste nicht zuerst gestoppt wurden. Dies wurde auch �ber Live-Patches f�r DietPi v7.8 geliebt.
- **DietPi-Software** | [**Transmission**](../../software/bittorrent/#transmission) :octicons-arrow-right-16: Es wurde eine v7.8-Regression behoben, bei der bei Neuinstallationen die beabsichtigte Konfiguration nicht bereitgestellt wurde. Vielen Dank an [phpBB:kannz](https://dietpi.com/phpbb/memberlist.php?username=kannz){: class="nospellcheck"} und [phpBB:alessandro.psrt](https://dietpi. com/phpbb/memberlist.php?username=alessandro.psrt){: class="nospellcheck"} f�r die Meldung dieses Problems im DietPi-Forum: ["�bertragungseinstellungen?"](https://dietpi.com/phpbb/viewtopic .php?t=9567) oder ["Falsche `settings.json` im �bertragungsdaemon"](https://dietpi.com/phpbb/viewtopic.php?t=9683).
- **DietPi-Software** | [**Deluge**](../../software/bittorrent/#deluge) :octicons-arrow-right-16: Umgehung eines Problems auf Raspberry Pi ARMv6-Userland-Systemen, bei dem der Dienst nicht gestartet werden konnte. _Deluge_ wurde daher f�r diese Systeme wieder aktiviert. Vielen Dank an @themagicbullet f�r die Bereitstellung der Problemumgehung: <https://github.com/MichaIng/DietPi/issues/4944>.
- **DietPi-Software** | **UnRAR** :octicons-arrow-right-16: Es wurde ein Problem auf Raspberry Pi 1 an Zero (1) behoben, bei dem eine inkompatible �unrar�-Bin�rdatei installiert war. �unrar-free� von Raspbian ist jetzt auf diesen Modellen installiert, aber beachten Sie, dass es nicht alle RAR-Formate vollst�ndig unterst�tzt. Daher kann es in manchen F�llen fehlschlagen, Archive zu extrahieren.
- **DietPi-Software** | [**rTorrent**](../../software/bittorrent/#rtorrent) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der `/RPC2`-Proxy zum rTorrent-UNIX-Socket beim Apache-Webserver nicht funktionierte Arbeit wegen ung�ltiger Syntax. Vielen Dank an @Camry2731 f�r die Meldung dieses Problems.
- **DietPi-Software** | [**RealVNC**](../../software/remote_desktop/#realvnc-server) :octicons-arrow-right-16: Problemumgehung f�r einen fehlgeschlagenen ersten Start von RealVNC aufgrund einer gel�schten Passwortdatei aktualisiert/behoben . Vielen Dank an @xmicky f�r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/5050>.

Wie immer wurden viele kleinere Codeleistungs- und Stabilit�tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code�nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/issues/5019>

F�r alle zus�tzlichen Probleme, die nach der Ver�ffentlichung auftreten k�nnen, besuchen Sie bitte den folgenden Link f�r aktive Tickets: <https://github.com/MichaIng/DietPi/issues>.
