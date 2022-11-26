# Versionshinweise

## Dezember 2021 (Version 7.9)

### &Uuml;berblick

Willkommen zur **Ver&ouml;ffentlichung vom Dezember 2021** :octicons-heart-16: von **DietPi**. Es aktiviert den Passwortschutz f&uuml;r [**DietPi-Dashboard**](../../software/system_stats/#dietpi-dashboard), [**DietPi-Backup**](../../dietpi_tools/ #dietpi-backup-backuprestore) beginnt mehrere Backups zu unterst&uuml;tzen und der **[Apache](../../software/webserver_stack/#apache)** Webserver verwendet den dedizierten `PHP-FPM`-Server, was die Gesamtleistung verbessert . Und vieles mehr.

### Bekanntmachung

!!! Warnung `**Debian `Stretch`-Unterst&uuml;tzung**`

Debian 9 `Stretch` wurde 2017 ver&ouml;ffentlicht und wurde zun&auml;chst von Debian 10 `Buster` und dann von Debian 11 `Bullseye` abgel&ouml;st.

**DietPi v7.9 wird die letzte Version mit Unterst&uuml;tzung f&uuml;r Debian Stretch sein**. Die n&auml;chste Version wird **DietPi v8.0** sein und erfordert Debian Buster oder neuer.

Lesen Sie unseren Artikel [**Warum Sie Ihr Stretch-System jetzt aktualisieren sollten**] (https://dietpi.com/blog/?p=1001), um mehr &uuml;ber die Notwendigkeit dieses Upgrades zu erfahren und wie Sie dies ganz einfach tun k&ouml;nnen Debian Buster und noch weiter bis zur neuesten Version (**Debian Bullseye**).

### Verbesserungen {: #verbesserungen-79 }

- [**DietPi-Dashboard**](../../software/system_stats/#dietpi-Dashboard)
- Bei Neuinstallationen ist der Passwortschutz jetzt standardm&auml;&szlig;ig aktiviert und verwendet das **globale Softwarepasswort**.

![DietPi-Dashboard-Passwort](../assets/images/dietpi-dashboard-login.jpg){: width="800" height="576" loading="lazy"}

Sie k&ouml;nnen dies manuell anwenden oder &auml;ndern, indem Sie den Anweisungen in unserer [Dokumentation](../../software/system_stats/#dietpi-dashboard) folgen.

- Der Standard-TCP-Netzwerkport wurde von `8088` auf `5252` ge&auml;ndert, um einen Portkonflikt mit InfluxDB zu l&ouml;sen. Wenn Sie DietPi-Dashboard bereits installiert haben, werden Sie gefragt, ob Sie diese &Auml;nderung w&auml;hrend des Updates &uuml;bernehmen m&ouml;chten.

![DietPi-Dashboard Standardport](../assets/images/dietpi-dashboard-port-change.jpg){: width="800" height="252" loading="lazy"}

Vielen Dank an @blablazzz f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4966>

- [**DietPi-Backup**](../../dietpi_tools/#dietpi-backup-backuprestore)
- Es kann jetzt ein Backup-Archiv mit einer w&auml;hlbaren Anzahl von zu behaltenden Backups erstellt werden. Backups werden automatisch rotiert und wenn die maximale Menge erreicht ist, wird das &auml;lteste Backup als Grundlage f&uuml;r die inkrementelle neue Backup-Synchronisierung verwendet, um Schreibvorg&auml;nge zu reduzieren und die Geschwindigkeit zu erh&ouml;hen.

![DietPi-Sicherungsmenge](../assets/images/dietpi-Sicherungsmenge.jpg){: width="800" height="265" loading="lazy"}

Vielen Dank an [phpBB:johnvick](https://dietpi.com/phpbb/memberlist.php?username=johnvick){: class="nospellcheck"} und viele andere f&uuml;r die Anfrage nach dieser Funktion [im DietPi-Forum](https ://dietpi.com/phpbb/viewtopic.php?t=3593).

- Backups k&ouml;nnen jetzt au&szlig;erhalb von `/mnt` in jedem Verzeichnis oder Einh&auml;ngepunkt gespeichert werden, solange das Dateisystem `symlinks` und UNIX-`Berechtigungen` unterst&uuml;tzt.
– Es wurde ein Problem behoben, bei dem Sicherung und Wiederherstellung fehlschlugen, wenn ein nicht standardm&auml;&szlig;iger Sicherungsspeicherort verwendet wurde, da ein falscher Protokolldateipfad verwendet wurde. Dies ist eine v7.8-Regression. Vielen Dank an [phpBB:Malinka](https://dietpi.com/phpbb/memberlist.php?username=Malinka){: class="nospellcheck"} f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https:// dietpi.com/phpbb/viewtopic.php?p=39909#p39909).

- [**Himbeer-Pi**](../../hardware/#raspberry-pi)
- Seit Bullseye verwenden einige Mediensoftwaretitel, vor allem `FFmpeg` und solche, die `FFmpeg`-Bibliotheken verwenden, die f&uuml;r die Raspberry Pi-Firmware kompiliert wurden (**Kodi**, **Jellyfin**, **Chromium**), Verwendung die Raspberry Pi V4L2-Codec-Treiber. Diese wurden zuvor mit dem RPi-Kameramodulschalter in dietpi-config aktiviert/deaktiviert. Die Hardware-Codec-Treiber sind nun zu einem eigenen CLI-Befehl und Men&uuml;schalter in den Anzeigeoptionen der dietpi-config geworden und werden automatisch aktiviert, wenn einer der genannten Softwaretitel auf Bullseye (oder h&ouml;her) installiert oder neu installiert wird.

- **DietPi-Software** | **[SABnzbd](../../software/bittorrent/#sabnzbd)**
- Bei Neuinstallationen wurde die Dateiprotokollierung zugunsten der Journalprotokollierung deaktiviert. Alle Dienst- und Prozessprotokolle k&ouml;nnen daher jetzt &uuml;berpr&uuml;ft werden &uuml;ber: `journalctl -u sabnzbd`
– Behebung eines Problems, bei dem Installationen auf ARMv6- und ARMv7-Stretch-Systemen fehlschlugen. Vielen Dank an @bensp f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4997>.

- **DietPi-Software** | **[Apache](../../software/webserver_stack/#apache)**
- Neuinstallationen und Neuinstallationen werden mit `PHP-FPM` anstelle von `mod_php` konfiguriert. Als Voraussetzung wird statt Prefork das Event `MPM` verwendet. Dies reduziert die Speichernutzung und erh&ouml;ht die Zugriffsleistung bei gleichzeitigen Anfragen erheblich, da der Apache-Elternprozess nicht f&uuml;r jeden einzelnen Prozess einen neuen Kindprozess forken muss.
- Es wird weiter optimiert, indem nur ein einziger statischer untergeordneter Prozess erzeugt wird, w&auml;hrend gleichzeitige Anforderungen von einer ausreichenden Anzahl von Prozess-Threads verarbeitet werden. Dies erm&ouml;glicht Apache, Speicher effizient zu teilen und macht es ziemlich leicht. Es sind keine Nachteile bekannt, wenn nur ein einzelner Prozess verwendet wird, im Vergleich zu mehreren Prozessen mit jeweils weniger Threads. Weitere Informationen finden Sie in den verwandten Fragen und Antworten zu StackExchange: [StackExchange - Apache2 MPM event: More threads vs more processes?](https://superuser.com/questions/1611015/apache2-mpm-event-more-threads-vs-more- Prozesse)
- Die Standard-/Basiskonfiguration wird jetzt als separate Datei hinzugef&uuml;gt, sodass die Hauptdatei `apache2.conf` nicht mehr ber&uuml;hrt wird. Au&szlig;erdem wird der standardm&auml;&szlig;ige `vhost` jetzt vor der Paketinstallation vorab erstellt, sodass er bei einer Neuinstallation &uuml;bersprungen werden kann, um benutzerdefinierte Einstellungen nicht zu &uuml;berschreiben. Diese in Kombination erm&ouml;glichen eine sichere und saubere Neuinstallation, ohne vom Administrator vorgenommene &Auml;nderungen zu besch&auml;digen, mit der kleinen Ausnahme, dass das Webroot auf `/var/www` gesetzt ist, was f&uuml;r alle unsere Softwareoptionen erforderlich ist, die einen externen Webserver verwenden .
- Die neue Standardkonfiguration bietet maximale Datenschutzeinstellungen und Sicherheitsheader. Es ist einfach, diese mit eigenen Konfigurationen auf `vhost`- oder Verzeichnisebene zu &uuml;berschreiben.
- Die Protokollierung erfolgt jetzt standardm&auml;&szlig;ig im Journal, und Sie k&ouml;nnen sie anzeigen, indem Sie den n&auml;chsten Befehl ausf&uuml;hren:

`Sch
journalctl -u apache2
```

- Die Direktive `ServerName` wird mit der **lokalen IP** hinzugef&uuml;gt, um entsprechende Startwarnungen stummzuschalten.
Dies kann zu Zugriffs- und CORS-Fehlern f&uuml;hren, wenn Anwendungen den Servernamen als zul&auml;ssigen Hostnamen pr&uuml;fen, aber andere externe IPs/Hostnamen f&uuml;r den Zugriff verwendet wurden. In einem solchen Fall bieten Anwendungen im Allgemeinen eine M&ouml;glichkeit, eine Liste zul&auml;ssiger Hostnamen zu definieren. Ohne einen festgelegten Servernamen wendet der Webserver normalerweise einfach den `HTTP_HOST`-Header an, der jede damit verbundene &Uuml;berpr&uuml;fung umgeht. Laut der protokollierten Warnung scheint Apache dann `127.0.1.1` zu verwenden.

- **DietPi-Software** | [**Kodi**](../../software/media/#kodi)
- Auf **Raspberry Pi Bullseye**-Systemen ist jetzt das neue offizielle **Raspberry Pi**-Repository-Build f&uuml;r Kodi 19.3 installiert. Sie k&ouml;nnen das Upgrade manuell anwenden, indem Sie Kodi neu installieren.

`Sch
dietpi-software neu installieren 31
```

- Das Addon-Repository wird jetzt standardm&auml;&szlig;ig bei allen Kodi-Installationen installiert, was zuvor nur bei RPi und Odroids der Fall war. Wenn es derzeit fehlt, kann es manuell installiert werden

`Sch
apt installiere kodi-repository-kodi
```

- **DietPi-Software** | [**Gitea**](../../software/cloud/#gitea)
- Der Dienst l&auml;uft jetzt als dedizierter Benutzer `gitea` mit seinem Heimatverzeichnis `/mnt/dietpi_userdata/gitea`, um eine einfache &Uuml;bertragung und Verwendung von SSH-Schl&uuml;sseln f&uuml;r den Fernzugriff zu erm&ouml;glichen. Dies gilt f&uuml;r neu installierte oder neu installierte Gitea-Instanzen. Vielen Dank an @LilTrublMakr f&uuml;r die Meldung der damit verbundenen Einschr&auml;nkung mit dem zuvor verwendeten `dietpi`-Benutzer: <https://github.com/MichaIng/DietPi/issues/4620>.
- [**Gitea**](../../software/cloud/#gitea) und [**Gogs**](../../software/cloud/#gogs) kollidieren miteinander, da beide Verwenden Sie standardm&auml;&szlig;ig den Port "3000". DietPi verwendet ein neues Konfliktmanagementsystem, um zu verhindern, dass beide gleichzeitig installiert werden.

- **DietPi-Software** | [**Chromium**](../../software/desktop/#chromium) :octicons-arrow-right-16: Auf Raspberry Pi wird nun das Paket `chromium-codecs-ffmpeg-extra` zusammen mit installiert Chromium, das zus&auml;tzliche Codecs f&uuml;r patentierte Video-/Audioformate hinzuf&uuml;gt. Vielen Dank an @Krawei f&uuml;r die Identifizierung dieser Chromium-Videowiedergabeverbesserung – siehe <https://github.com/MichaIng/DietPi/issues/5013>.

- **DietPi-Software** | [**rTorrent**](../../software/bittorrent/#rtorrent) :octicons-arrow-right-16: Bei Neuinstallationen lauscht rTorrent jetzt standardm&auml;&szlig;ig auf **TCP-Port 49164** auf eingehende BitTorrent Verbindungen. Abgesehen von `DHT` war das Lauschen auf eingehende Verbindungen zuvor komplett deaktiviert, was je nach verwendetem Tracker zu langsamen oder gar keinen Peer-Verbindungen f&uuml;hrte. Vielen Dank an @Camry2731 f&uuml;r die Meldung dieser Inkonsistenz mit unseren anderen BitTorrent-Serveroptionen.

- **DietPi-Software** - **Dateiserver** :octicons-arrow-right-16: Dieses Auswahlmen&uuml; wurde aus der DietPi-Software entfernt, da die meisten Dateiserver gleichzeitig laufen k&ouml;nnen. Somit ist es nicht mehr erforderlich, zuerst den bestehenden Dateiserver (zB einen Samba-Server) zu entfernen und dann etwas Neues (zB einen FTP-Server) zu installieren. Dadurch ist kein dedizierter Men&uuml;punkt in der DietPi-Software notwendig.

Dateiserver k&ouml;nnen &uuml;ber die Men&uuml;s `Browse Software` oder `Search Software` in `dietpi-software` oder &uuml;ber CLI ausgew&auml;hlt werden. Siehe die Dokumentation f&uuml;r die verf&uuml;gbaren [DietPi-Dateiserver] (../../software/file_servers/).

![DietPi-Software](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

Die zugeh&ouml;rige `dietpi.txt`-Einstellung wurde auch f&uuml;r neue Bilder entfernt, aber sie wird immer noch ber&uuml;cksichtigt, wenn sie vorhanden ist. Verwenden Sie f&uuml;r eine automatische Installation mit neuen Images stattdessen die Einstellung `AUTO_SETUP_INSTALL_SOFTWARE_ID`.

- **DietPi-Dokumentation** | [**Anleitung**](../../usage/#how-to-do-an-automatic-base-installation-at-first-boot-dietpi-automation) :octicons-arrow-right-16 : Abschnitt hinzugef&uuml;gt, der die **automatische Basisinstallation beim ersten Booten** &uuml;ber die Datei `/boot/dietpi.txt` (DietPi-Automation) beschreibt.

### Fehlerbehebungen {: #bug-fixes-79 }

- [**Raspberry Pi**](../../hardware/#raspberry-pi) :octicons-arrow-right-16: Es wurde ein Problem in den DietPi-Images behoben, bei dem beim ersten Booten zwei serielle Anmeldekonsolen auf dem generischen `symlinked` und tats&auml;chliche serielle Ger&auml;te k&ouml;nnten gestartet worden sein. Dies verdoppelte die Eingaben und brach beim ersten Start die erfolgreiche Anmeldung mit `Benutzername` und `Passwort` &uuml;ber die serielle Konsole. Vielen Dank an @ad7718 f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/5014>.
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration)
– Es wurde ein Problem behoben, bei dem die Aktivierung des LCD-Panels `odroid-lcd35` auf Odroids fehlschlug, da SPI standardm&auml;&szlig;ig aktiviert ist und dieselben GPIO-Ports blockiert. Vielen Dank an @MarcProux f&uuml;r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/4154>.
– Es wurde ein Problem behoben, bei dem das Netzwerkadaptermen&uuml; die statischen DNS-Server nicht angezeigt hat, die effektiv beim ersten Start basierend auf den Einstellungen von `dietpi.txt` angewendet wurden. Vielen Dank an @nils-trubkin f&uuml;r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/5054>.
- **DietPi-Software** :octicons-arrow-right-16: Eine DietPi v7.8-Regression behoben, bei der [ReadyMedia](../../software/media/#readymedia), [Deluge](../ ../software/bittorrent/#deluge), [Sonarr](../../software/bittorrent/#sonarr) und [Jellyfin](../../software/media/#jellyfin) Installationen schlugen mit einem fehl Fehler auf `usermod`, da die Dienste nicht zuerst gestoppt wurden. Dies wurde auch &uuml;ber Live-Patches f&uuml;r DietPi v7.8 geliebt.
- **DietPi-Software** | [**Transmission**](../../software/bittorrent/#transmission) :octicons-arrow-right-16: Es wurde eine v7.8-Regression behoben, bei der bei Neuinstallationen die beabsichtigte Konfiguration nicht bereitgestellt wurde. Vielen Dank an [phpBB:kannz](https://dietpi.com/phpbb/memberlist.php?username=kannz){: class="nospellcheck"} und [phpBB:alessandro.psrt](https://dietpi. com/phpbb/memberlist.php?username=alessandro.psrt){: class="nospellcheck"} f&uuml;r die Meldung dieses Problems im DietPi-Forum: ["&Uuml;bertragungseinstellungen?"](https://dietpi.com/phpbb/viewtopic .php?t=9567) oder ["Falsche `settings.json` im &Uuml;bertragungsdaemon"](https://dietpi.com/phpbb/viewtopic.php?t=9683).
- **DietPi-Software** | [**Deluge**](../../software/bittorrent/#deluge) :octicons-arrow-right-16: Umgehung eines Problems auf Raspberry Pi ARMv6-Userland-Systemen, bei dem der Dienst nicht gestartet werden konnte. _Deluge_ wurde daher f&uuml;r diese Systeme wieder aktiviert. Vielen Dank an @themagicbullet f&uuml;r die Bereitstellung der Problemumgehung: <https://github.com/MichaIng/DietPi/issues/4944>.
- **DietPi-Software** | **UnRAR** :octicons-arrow-right-16: Es wurde ein Problem auf Raspberry Pi 1 an Zero (1) behoben, bei dem eine inkompatible `unrar`-Bin&auml;rdatei installiert war. `unrar-free` von Raspbian ist jetzt auf diesen Modellen installiert, aber beachten Sie, dass es nicht alle RAR-Formate vollst&auml;ndig unterst&uuml;tzt. Daher kann es in manchen F&auml;llen fehlschlagen, Archive zu extrahieren.
- **DietPi-Software** | [**rTorrent**](../../software/bittorrent/#rtorrent) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der `/RPC2`-Proxy zum rTorrent-UNIX-Socket beim Apache-Webserver nicht funktionierte Arbeit wegen ung&uuml;ltiger Syntax. Vielen Dank an @Camry2731 f&uuml;r die Meldung dieses Problems.
- **DietPi-Software** | [**RealVNC**](../../software/remote_desktop/#realvnc-server) :octicons-arrow-right-16: Problemumgehung f&uuml;r einen fehlgeschlagenen ersten Start von RealVNC aufgrund einer gel&ouml;schten Passwortdatei aktualisiert/behoben . Vielen Dank an @xmicky f&uuml;r die Meldung dieses Problems <https://github.com/MichaIng/DietPi/issues/5050>.

Wie immer wurden viele kleinere Codeleistungs- und Stabilit&auml;tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code&auml;nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/issues/5019>

F&uuml;r alle zus&auml;tzlichen Probleme, die nach der Ver&ouml;ffentlichung auftreten k&ouml;nnen, besuchen Sie bitte den folgenden Link f&uuml;r aktive Tickets: <https://github.com/MichaIng/DietPi/issues>.
