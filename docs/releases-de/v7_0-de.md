# Versionshinweise

## Februar 2021 (Version 7.0)

### Ü;berblick

Willkommen zur **Ver&ouml;ffentlichung vom Februar 2021** :octicons-heart-16: von **DietPi**. Mit dieser Version haben wir die Hauptversionsnummer geändert und sie wurde zu **Version 7**! Wir erwarten ein reibungsloses Upgrade :octicons-thumbsup-16:

![DietPi-Version 7](../assets/images/dietpi-version7.jpg){: width="300" loading="lazy"}

!!! info "Warum dieses Upgrade auf Version 7?"

Eine neue Ü;berprüfung der Systemupdates wurde implementiert. Dieser prüft auf eine mindestens erforderliche Debian- und DietPi-Version und migriert Systeme mit entweder zu alter Debian-Version oder zu alter DietPi-Version automatisch in einen anderen Git-Zweig. Dieser Prozess erleichtert die Migration unserer Codebasis auf neuere Debian-Versionen.

Der alternative Zweig kann verwendet werden, um Debian-Distributions-Upgrades zu informieren und zu unterstützen und um den DietPi-Code auf eine Zwischenversion zu aktualisieren, von der aus das System zurück zum regulären Stable/Master-Zweig migriert werden kann.

Da diese Änderung eine neue Repository-Versionsdatei erforderte, haben wir die DietPi-Kernversion auf v7.0 erh&ouml;ht. Der Wechsel zu Version 7 ist auch durch die lange Liste von Verbesserungen motiviert, die 2020 eingeführt wurden. All diese qualifizieren das System für ein Upgrade auf eine neue Version.

Diese Änderung hat KEINE Nebenwirkungen! Wir ermutigen Sie dazu. Alle bisher unterstützten DietPi- und Debian-Versionen werden weiterhin unterstützt! Diese Änderung erm&ouml;glicht es uns, KEINE neuen Image-Installationen für gr&ouml;&szlig;ere Upgrades zu verlangen (wie wir es vor einigen Jahren getan haben, als ein Upgrade von v159 auf v6.0 erforderlich war).

Diese neue Version enthält **4 neue Softwaretitel** :octicons-paper-airplane-16:

### Neue optimierte Softwarepakete

**[Docker Compose](../../software/programming/#docker-compose)**

Docker Compose ist ein Tool zum Definieren und Ausführen von Docker-Anwendungen mit mehreren Containern. Es kann jetzt über unsere Softwareauswahl installiert werden. [Docker](../../software/programming/#docker) wird automatisch eingezogen (als Abhängigkeit).

**Was würde Docker Compose Ihnen bringen?**

Wann immer Sie mehrere Container :octicons-server-16: haben, müssen Sie viele Aufgaben erledigen: jeden einzelnen Container bereitstellen und konfigurieren und sie so konfigurieren, dass sie auch miteinander kommunizieren. Dies wird selbst bei wenigen Behältern mühsam.

Mit [Docker Compose](../../software/programming/#docker-compose) k&ouml;nnen Sie die Bereitstellung mehrerer Container mithilfe einer YAML-Datei automatisieren. Mit dieser Datei k&ouml;nnen Sie die Dienste Ihrer Anwendung konfigurieren und alle Dienste der App aus dieser Konfiguration erstellen.

![Docker Compose-Piktogramm](../assets/images/dietpi-docker-compose.png){: width="500" height="351" loading="lazy"}

Beispielanwendungen mit Docker Compose und weitere Details finden Sie auf der [Dokumentationsseite](../../software/programming/#docker-compose).

**[Steam](../../software/gaming/#steam)** & **[Box86](../../software/gaming/#box86)**

[Steam](../../software/gaming/#steam) für ARM-Prozessoren ist seit vielen Jahren eine Feature-Anfrage. Seit es m&ouml;glich ist, auf ARM-Boards zu installieren, ist es jetzt auch auf DietPi verfügbar. [Box86](../../software/gaming/#box86) wird automatisch als Abhängigkeit installiert.

Die Steam-Plattform ist eine der gr&ouml;&szlig;ten digitalen Vertriebsplattformen für Spiele. Auf ARMv7-Boards hat es jedoch eingeschränkte Funktionen und Spielunterstützung. Hier sind einige Beispielspiele, die mit [Box86](../../software/gaming/#box86) laufen:

<iframe src="https://www.youtube-nocookie.com/embed/z-4aGNqZ724?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading=" faul"></iframe>

!!! die Info ""

**Achtung:** Steam läuft m&ouml;glicherweise noch nicht perfekt stabil :octicons-beaker-16:. Es k&ouml;nnte auch abstürzen, wenn versucht wird, Speicherplatz für die Spiele zuzuweisen, und die Downloads werden fortgesetzt, sobald sie erneut gestartet wurden.

Wir sind optimistisch, dass weitere Verbesserungen diese Probleme angehen und in Zukunft weitere Verbesserungen verfügbar sein werden :octicons-heart-16:

[Box86](../../software/gaming/#box86) ist ein x86-Wrapper/Emulator für ARMv7-Systeme und steht jetzt zur Installation zur Verfügung. Dank der Fähigkeit, gemeinsam genutzte ARMv7-Systembibliotheken zur Verwendung mit i386-Binärdateien zu verpacken, müssen häufig keine zusätzlichen Bibliotheken installiert werden.

!!! die Info ""

Dank <https://github.com/tbinfm> wird es automatisch aufgerufen, wenn eine i386-Binärdatei ausgeführt wird.

**[mjpg-streamer](../../software/camera/#mjpg-streamer)**

**mjpg-streamer** ist ein leichtgewichtiger JPEG-Streamer mit mehreren Quellen und mehreren Ausgaben und kann jetzt installiert werden. Es kann verwendet werden, um JPEG-Dateien über ein IP-basiertes Netzwerk von einer Webcam zu verschiedenen Arten von Betrachtern zu streamen.

Standardmä&szlig;ig wird Ihre angehängte Kameraaufnahme an einen benutzerdefinierten HTTP-Port gestreamt. Wenn [OctoPrint](../../software/printing/#octoprint) installiert ist, wird mjpg-streamer automatisch für die Zusammenarbeit konfiguriert. Bei der Installation auf [Raspberry Pi](../../hardware/#raspberry-pi) wird die Unterstützung des Raspberry Pi-Kameramoduls standardmä&szlig;ig aktiviert.

Weitere Einzelheiten finden Sie auf der Dokumentationsseite: [mjpg-streamer](../../software/camera/#mjpg-streamer).

### Änderungen / Verbesserungen / Optimierungen

- **Netzwerk** :octicons-arrow-right-16: Es wurde eine Änderung in der Reihenfolge implementiert, in der netzwerkbezogene systemd-Dienstziele erreicht werden. "`network.target`" und "`network-online.target`" werden nun erreicht, nachdem alle Netzwerkschnittstellen konfiguriert wurden, anstatt bereits, nachdem nur die Loopback-Schnittstelle "lo" konfiguriert wurde. Dies betrifft nur `systemd`-Dienste, die nicht von [DietPi-Services](../../dietpi_tools/#dietpi-services) gestartet werden, zB SSH/DNS/VPN/VNC-Server, so dass ihnen dies zugesichert wird in der Lage sein, an Schnittstellen/IPs zu binden, wo sie derzeit versagen würden. Der Nachteil ist, wenn man einen Ethernet-Adapter hat, der über dietpi-config oder /etc/network/interfaces (als `allow-hotplug`-Gerät) konfiguriert ist, aber das Kabel nicht angeschlossen ist, k&ouml;nnen betroffene Dienste verz&ouml;gert werden, bis die Schnittstelle zeitlich eingestellt ist aus.
- [DietPi-Backup](../../dietpi_tools/#dietpi-backup-backuprestore) :octicons-arrow-right-16: Eine neue Funktion wurde hinzugefügt, die es erm&ouml;glicht, ein dietpi-Backup beim ersten Booten automatisch wiederherzustellen.

    Setzen Sie dazu die neue Option `dietpi.txt`

    ```sh
    AUTO_SETUP_BACKUP_RESTORE=1
    ```

    , um eine Liste der gefundenen Backups zur Auswahl zu erhalten (funktioniert nicht in Kombination mit `AUTO_SETUP_AUTOMATED=1`).

    Alle angeschlossenen Laufwerke werden temporär gemountet und automatisch durchsucht.
    Satz

    ```sh
    AUTO_SETUP_BACKUP_RESTORE=2
    ```

    um das erste gefundene Backup nicht interaktiv wiederherstellen zu lassen (dies funktioniert in Kombination mit `AUTO_SETUP_AUTOMATED=1`).

    Die Wiederherstellung läuft nach dem ersten Update, funktioniert also auch mit älteren Images und kann über eine SSH-Verbindung erfolgen. Credits gehen an @ravenclaw900 für die Implementierung dieser Funktion: <https://github.com/MichaIng/DietPi/pull/4112>.

- **DietPi-Backup** :octicons-arrow-right-16: Unterstützung für XFS- und ZFS-Zieldateisystemtypen wurde hinzugefügt, die die erforderlichen Symlink- und POSIX-Berechtigungsfunktionen vollständig unterstützen.
- **DietPi-Konfig** | **RPi** :octicons-arrow-right-16: Eine Option wurde hinzugefügt, um die SPI-Schnittstelle umzuschalten. Vielen Dank an @incanus für die Wiederbelebung dieser alten Funktionsanfrage: <https://github.com/MichaIng/DietPi/issues/98#issuecomment-783650204>.
- **DietPi-Software** :octicons-arrow-right-16: Der obligatorische Neustart nach Installationen wurde entfernt. Installierte Dienste, die nicht von DietPi-Services gesteuert werden, sondern beim Neustart automatisch starten würden, werden jetzt stattdessen am Ende der Installation gestartet. Ein manueller Neustart ist immer noch eine gute Idee, aber nur in seltenen Fällen unbedingt erforderlich. Vielen Dank an @Games-Crack für diesen Vorschlag: <https://github.com/MichaIng/DietPi/issues/4032>.
- **DietPi-Software** :octicons-arrow-right-16: Installationen implizieren nicht mehr alle APT-Paket-Upgrades. Während wir empfehlen, alle APT-Pakete regelmä&szlig;ig zu aktualisieren, hilft Ihnen der neue tägliche APT-Check und die Informationen im DietPi-Banner dabei, Sie auf dem Laufenden zu halten, damit Sie selbst die beste Entscheidung treffen k&ouml;nnen, ob und wann Sie welches Paket-Upgrade anwenden. Bei Erstinstallationen wird jedoch das vollständige Upgrade beibehalten, um sicherzustellen, dass jedes Image im vollständig aktualisierten Zustand startet und Pakete, die für die eigentliche Softwareauswahl, die Sie installieren, erforderlich sind, ebenfalls aktualisiert werden, wenn sie bereits installiert sind.
- **DietPi-Software** :octicons-arrow-right-16: Deinstallationen stoppen andere Dienste nicht mehr. Beispielsweise bleibt Ihr Webserver oder Media-Streaming-Server aktiv, während Sie andere Software deinstallieren, die Sie nicht mehr ben&ouml;tigen. Da Deinstallationen nicht viel RAM oder CPU-Ressourcen ben&ouml;tigen, ist dies vollkommen in Ordnung. Vielen Dank an @mrgreaper für den Hinweis: <https://github.com/MichaIng/DietPi/issues/4116>.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Bei Installation in Kombination mit Pi-hole, keine zusätzlichen Konfigurationsdatei wird nicht mehr erstellt, aber die angepasste Schnittstellenbindung und der Port werden auf "/etc/unbound/unbound.conf.d/dietpi.conf" angewendet. Das Deklarieren von `interface` in zwei Konfigurationsdateien überschreibt sich nicht gegenseitig, sondern führt zu zwei gleichzeitigen Bindungen, was nicht beabsichtigt ist. Die beiden Dateien, falls vorhanden, werden beim DietPi-Update ebenfalls zusammengeführt. Es ist daher beabsichtigt, dass Administratoren `dietpi.conf` bei Bedarf direkt ändern und diese Datei bei Neuinstallationen nicht überschrieben wird, um lokale Änderungen beizubehalten. Darüber hinaus wird die Konfigurationsdatei bei Neuinstallationen besser sortiert und enthält Kommentare, um ihren Zweck zu erläutern.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Bei Neuinstallationen wird nun standardmä&szlig;ig der Zugriff gewährt alle privaten IPv4- und IPv6-Adressbereiche statt nur zum Subnetz `192.168.0.0/16`, das VPN-Schnittstellen, Container und Fälle mehrerer lokaler Netzwerke umfasst, an die der Server angeschlossen ist.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wird jetzt ein monatlicher Cron-Job erstellt, um die Wurzel zu behalten Hinweisdatei aktualisiert. Vielen Dank an @APraxx für diesen Vorschlag: <https://github.com/MichaIng/DietPi/issues/4077>.
- **DietPi-Software** | **Python 3**: Bei `pip`- und pip-basierten Installationen auf ARMv6- und ARMv7-Boards wird das piwheels.org-Repository für vorkompilierte Räder automatisch hinzugefügt, was die Build-Abhängigkeiten und die Kompilierzeit drastisch reduzieren kann.
- **DietPi-Software** | **[Node-RED](../../software/hardware_projects/#node-red)**: Neuinstallationen und Neuinstallationen mit Setup [Node-RED](../../software/hardware_projects/#node -red) als lokales Modul für den `geknoteten` Dienstbenutzer und nicht als globales Systemmodul/Befehl. Dadurch k&ouml;nnen alle zugeh&ouml;rigen Node-Module über die Webschnittstelle aktualisiert und entfernt werden, anstatt nur diejenigen, die über die Webschnittstelle installiert wurden. Zusätzlich wurde ein Konsolen-Alias für den CLI-Befehl `node-red-admin` hinzugefügt, sodass die Ausführung dieses Befehls mit einem beliebigen Benutzer die lokale Node-RED-Instanz als `geknoteter` Dienstbenutzer aufruft.
- **DietPi-Software** | **[Docker](../../software/programming/#docker)**: Das Docker-APT-Repository wird jetzt manuell installiert, anstatt das offizielle Docker-Installationsprogramm zu verwenden. Dies erm&ouml;glicht es uns, die Docker-Installationsoption für Debian Bullseye-Systeme zu aktivieren, und sei es nur, um erweiterte Tests dieser kommenden Debian-Ver&ouml;ffentlichung mit DietPi zu erm&ouml;glichen.

### Aktualisierungen der Benutzeroberfläche

- **DietPi-Banner** :octicons-arrow-right-16: Das Ausführen des Skripts ohne Eingabeargument &ouml;ffnet jetzt das Menü, anstatt das Banner zu drucken. Der Konsolen-Alias wurde entsprechend angepasst, sodass es nun m&ouml;glich ist, `dietpi-banner 0` und `dietpi-banner 1` von der Konsole aus auszuführen, um vollständige und kurze Bannerversionen drucken zu lassen. Der Konsolenbefehl `dietpi-banner` &ouml;ffnet weiterhin das Menü.

### Fehlerbehebung

- **Audio** :octicons-arrow-right-16: Es wurde ein Fehler mit Debian Buster behoben, bei dem der ALSA-Status-Daemon immer lief, auch wenn er nicht konfiguriert war.
- **DietPi-Globals** | `G_OBTAIN_CPU_TEMP` :octicons-arrow-right-16: Negativen Temperaturen wird nicht mehr vertraut, stattdessen wird "N/A" ausgegeben. Dies erm&ouml;glicht einen generischen Ansatz, um die Temperaturschätzung auf weiteren SBC-Modellen festzulegen/zuzulassen. Vielen Dank an [phpBB:Thanapat](https://dietpi.com/phpbb/memberlist.php?username=Thanapat){: class="nospellcheck"} für die Meldung eines verwandten Problems auf Roseapple Pi: <https://dietpi.com/phpbb/viewtopic.php?t=8677>
- **DietPi-Set_swapfile** :octicons-arrow-right-16: Behebung eines Problems, bei dem `zram`/`zram0` `dietpi.txt`-Pfadeinträge gel&ouml;scht wurden, wenn das Skript ohne Eingabeargumente ausgeführt wurde. Dies brach besonders beim Anwenden von `zram-swap` beim ersten Booten. Vielen Dank an @Dr0bac für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4002>
- **DietPi-Software** | **[Bitwarden_RS](../../software/cloud/#vaultwarden)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das selbstsignierte TLS-Zertifikat nicht auf iOS importiert werden konnte. Um diesen Fix auf eine vorhandene Instanz anzuwenden, muss die Konfigurationsdatei `/mnt/dietpi_userdata/bitwarden_rs/bitwarden_rs.env` entfernt oder an einen anderen Speicherort verschoben werden, damit `dietpi-software reinstall 183` die Konfiguration neu erstellt und TLS-Zertifikat.
- **DietPi-Software** | **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem während der Installation in Kombination mit Pi-hole der Neustart des Dienstes fehlschlagen konnte. Vielen Dank an @Ernstian für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2409#issuecomment-739154892>
- **DietPi-Software** | **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der Dienststart fehlschlug, wenn das Hostsystem eine lokale IP-Adresse au&szlig;erhalb der 192.168.0.0/16 Subnetz. Vielen Dank an @faxesystem für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2409#issuecomment-749174984>
- **DietPi-Software** | **[ReadyMedia](../../software/media/#readymedia)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Medienbibliothek beim Dienststart nicht erneut gescannt wurde. Vielen Dank an @AdamFarnsworth0 für die Meldung dieses Problems: <https://twitter.com/AdamFarnsworth0/status/1347977813635305475>
- **DietPi-Software** | **[WiFi-Hotspot](../../software/advanced_networking/#wifi-hotspot)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation auf Armbian-basierten Images mit `RTL8188C*` WiFi erfolgte Chip ausgefallen. Vielen Dank an [phpBB:smogan71](https://dietpi.com/phpbb/memberlist.php?username=smogan71){: class="nospellcheck"} für die Meldung dieses Problems: <https://dietpi.com/phpbb/viewtopic.php?t=8523>
- **DietPi-Software** | **[Medusa](../../software/bittorrent/#medusa)** :octicons-arrow-right-16: Diese Softwareoption wurde auf Stretch-Systemen deaktiviert, da sie jetzt Python >=3.6 erfordert, was ist nicht im Debian-Stretch-Repository verfügbar. Wenn Sie Medusa auf einem Stretch-System ausführen, wird es weiterhin funktionieren, aber eine Aktualisierung ist entweder nicht m&ouml;glich oder bricht ab. Vielen Dank an @aermak für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/3991>
- **DietPi-Software** | **[WiringPi](../../software/hardware_projects/#wiringpi)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation fehlschlug, wenn das Verzeichnis `/usr/local/bin` war nicht anwesend. Vielen Dank an [phpBB:bruz](https://dietpi.com/phpbb/memberlist.php?username=bruz){: class="nospellcheck"} für die Meldung dieses Problems: <https://dietpi.com/phpbb/viewtopic.php?t=8609>
- **DietPi-Software** | **[PaperMC](../../software/gaming/#papermc)** :octicons-arrow-right-16: Behebung eines Problems, bei dem die Installation aufgrund geänderter Download-URLs fehlgeschlagen ist, und stabilisierter Dienststart und Konfigurationserstellung durch Festlegen der Java-Heap-Gr&ouml;&szlig;e und Einräumen von mehr Zeit für den Start auf kleineren SBCs. Vielen Dank an [phpBB:omavoss](https://dietpi.com/phpbb/memberlist.php?username=omavoss){: class="nospellcheck"} für die Meldung dieses Problems: <https://dietpi.com/phpbb/viewtopic.php?p=30191#p30191>
- **DietPi-Software** | **[OpenTyrian](../../software/gaming/#opentyrian)** :octicons-arrow-right-16: Die Installationsoption wurde auf x86_64 deaktiviert, da das Debian-Paket eine andere Dateistruktur hat und Es wurde auf 64-Bit-RPi-Systemen deaktiviert, da die Binärdatei für "armhf" kompiliert wurde.
- **DietPi-Software** | **[Domoticz](../../software/home_automation/#domoticz)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Speichern benutzerdefinierter Skripte und das Starten mit einer Vorlage nicht funktionierten. Vielen Dank an [phpBB:tec13](https://dietpi.com/phpbb/memberlist.php?username=tec13){: class="nospellcheck"} für die Meldung dieses Problems: <https://dietpi.com/phpbb/viewtopic.php?t=8627>
- **DietPi-Software** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem für [ruTorrent](../../software/bittorrent/#rtorrent), [Koel](../../ software/media/#koel) und [Bitwarden_RS](../../software/cloud/#vaultwarden) schlug die automatische Erkennung der neuesten Version fehl und stattdessen wurde ein m&ouml;glicherweise älteres Fallback verwendet. Vielen Dank an @kelvmod für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4105>
- **DietPi-Software** | **[LXQt](../../software/desktop/#lxqt)** :octicons-arrow-right-16: Visuelle Probleme mit unserer Standardkonfiguration von Debian Buster behoben, die von uns gelieferten Dateien drastisch vereinfacht und bereinigt .
- **DietPi-Software** | **[SABnzbd](../../software/bittorrent/#sabnzbd)** :octicons-arrow-right-16: Es wurde ein Problem auf Stretch behoben, bei dem die Installation aufgrund eines erh&ouml;hten Minimums [Python](../../software/programming/#python-3) fehlschlug Version mit SABnzbd v3.2.0. Wenn Python 3.5 installiert ist, wird jetzt SABnzbd v3.1.1 installiert, damit die Installationsoption vorerst aktiviert bleibt. Vielen Dank an @19eighties für die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2762#issuecomment-787118995>

!!! Hinweis ""

Wie immer wurden viele kleinere Codeleistungs- und Stabilitätsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Codeänderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4126>
