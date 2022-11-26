# Versionshinweise

## Februar 2021 (Version 7.0)

### �berblick

Willkommen zur **Ver�ffentlichung vom Februar 2021** :octicons-heart-16: von **DietPi**. Mit dieser Version haben wir die Hauptversionsnummer ge�ndert und sie wurde zu **Version 7**! Wir erwarten ein reibungsloses Upgrade :octicons-thumbsup-16:

![DietPi-Version 7](../assets/images/dietpi-version7.jpg){: width="300" loading="lazy"}

!!! info "Warum dieses Upgrade auf Version 7?"

Eine neue �berpr�fung der Systemupdates wurde implementiert. Dieser pr�ft auf eine mindestens erforderliche Debian- und DietPi-Version und migriert Systeme mit entweder zu alter Debian-Version oder zu alter DietPi-Version automatisch in einen anderen Git-Zweig. Dieser Prozess erleichtert die Migration unserer Codebasis auf neuere Debian-Versionen.

Der alternative Zweig kann verwendet werden, um Debian-Distributions-Upgrades zu informieren und zu unterst�tzen und um den DietPi-Code auf eine Zwischenversion zu aktualisieren, von der aus das System zur�ck zum regul�ren Stable/Master-Zweig migriert werden kann.

Da diese �nderung eine neue Repository-Versionsdatei erforderte, haben wir die DietPi-Kernversion auf v7.0 erh�ht. Der Wechsel zu Version 7 ist auch durch die lange Liste von Verbesserungen motiviert, die 2020 eingef�hrt wurden. All diese qualifizieren das System f�r ein Upgrade auf eine neue Version.

Diese �nderung hat KEINE Nebenwirkungen! Wir ermutigen Sie dazu. Alle bisher unterst�tzten DietPi- und Debian-Versionen werden weiterhin unterst�tzt! Diese �nderung erm�glicht es uns, KEINE neuen Image-Installationen f�r gr��ere Upgrades zu verlangen (wie wir es vor einigen Jahren getan haben, als ein Upgrade von v159 auf v6.0 erforderlich war).

Diese neue Version enth�lt **4 neue Softwaretitel** :octicons-paper-airplane-16:

### Neue optimierte Softwarepakete

**[Docker Compose](../../software/programming/#docker-compose)**

Docker Compose ist ein Tool zum Definieren und Ausf�hren von Docker-Anwendungen mit mehreren Containern. Es kann jetzt �ber unsere Softwareauswahl installiert werden. [Docker](../../software/programming/#docker) wird automatisch eingezogen (als Abh�ngigkeit).

**Was w�rde Docker Compose Ihnen bringen?**

Wann immer Sie mehrere Container :octicons-server-16: haben, m�ssen Sie viele Aufgaben erledigen: jeden einzelnen Container bereitstellen und konfigurieren und sie so konfigurieren, dass sie auch miteinander kommunizieren. Dies wird selbst bei wenigen Beh�ltern m�hsam.

Mit [Docker Compose](../../software/programming/#docker-compose) k�nnen Sie die Bereitstellung mehrerer Container mithilfe einer YAML-Datei automatisieren. Mit dieser Datei k�nnen Sie die Dienste Ihrer Anwendung konfigurieren und alle Dienste der App aus dieser Konfiguration erstellen.

![Docker Compose-Piktogramm](../assets/images/dietpi-docker-compose.png){: width="500" height="351" loading="lazy"}

Beispielanwendungen mit Docker Compose und weitere Details finden Sie auf der [Dokumentationsseite](../../software/programming/#docker-compose).

**[Steam](../../software/gaming/#steam)** & **[Box86](../../software/gaming/#box86)**

[Steam](../../software/gaming/#steam) f�r ARM-Prozessoren ist seit vielen Jahren eine Feature-Anfrage. Seit es m�glich ist, auf ARM-Boards zu installieren, ist es jetzt auch auf DietPi verf�gbar. [Box86](../../software/gaming/#box86) wird automatisch als Abh�ngigkeit installiert.

Die Steam-Plattform ist eine der gr��ten digitalen Vertriebsplattformen f�r Spiele. Auf ARMv7-Boards hat es jedoch eingeschr�nkte Funktionen und Spielunterst�tzung. Hier sind einige Beispielspiele, die mit [Box86](../../software/gaming/#box86) laufen:

<iframe src="https://www.youtube-nocookie.com/embed/z-4aGNqZ724?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading=" faul"></iframe>

!!! die Info ""

**Achtung:** Steam l�uft m�glicherweise noch nicht perfekt stabil :octicons-beaker-16:. Es k�nnte auch abst�rzen, wenn versucht wird, Speicherplatz f�r die Spiele zuzuweisen, und die Downloads werden fortgesetzt, sobald sie erneut gestartet wurden.

Wir sind optimistisch, dass weitere Verbesserungen diese Probleme angehen und in Zukunft weitere Verbesserungen verf�gbar sein werden :octicons-heart-16:

[Box86](../../software/gaming/#box86) ist ein x86-Wrapper/Emulator f�r ARMv7-Systeme und steht jetzt zur Installation zur Verf�gung. Dank der F�higkeit, gemeinsam genutzte ARMv7-Systembibliotheken zur Verwendung mit i386-Bin�rdateien zu verpacken, m�ssen h�ufig keine zus�tzlichen Bibliotheken installiert werden.

!!! die Info ""

Dank <https://github.com/tbinfm> wird es automatisch aufgerufen, wenn eine i386-Bin�rdatei ausgef�hrt wird.

**[mjpg-streamer](../../software/camera/#mjpg-streamer)**

**mjpg-streamer** ist ein leichtgewichtiger JPEG-Streamer mit mehreren Quellen und mehreren Ausgaben und kann jetzt installiert werden. Es kann verwendet werden, um JPEG-Dateien �ber ein IP-basiertes Netzwerk von einer Webcam zu verschiedenen Arten von Betrachtern zu streamen.

Standardm��ig wird Ihre angeh�ngte Kameraaufnahme an einen benutzerdefinierten HTTP-Port gestreamt. Wenn [OctoPrint](../../software/printing/#octoprint) installiert ist, wird mjpg-streamer automatisch f�r die Zusammenarbeit konfiguriert. Bei der Installation auf [Raspberry Pi](../../hardware/#raspberry-pi) wird die Unterst�tzung des Raspberry Pi-Kameramoduls standardm��ig aktiviert.

Weitere Einzelheiten finden Sie auf der Dokumentationsseite: [mjpg-streamer](../../software/camera/#mjpg-streamer).

### �nderungen / Verbesserungen / Optimierungen

- **Netzwerk** :octicons-arrow-right-16: Es wurde eine �nderung in der Reihenfolge implementiert, in der netzwerkbezogene systemd-Dienstziele erreicht werden. "`network.target`" und "`network-online.target`" werden nun erreicht, nachdem alle Netzwerkschnittstellen konfiguriert wurden, anstatt bereits, nachdem nur die Loopback-Schnittstelle "lo" konfiguriert wurde. Dies betrifft nur `systemd`-Dienste, die nicht von [DietPi-Services](../../dietpi_tools/#dietpi-services) gestartet werden, zB SSH/DNS/VPN/VNC-Server, so dass ihnen dies zugesichert wird in der Lage sein, an Schnittstellen/IPs zu binden, wo sie derzeit versagen w�rden. Der Nachteil ist, wenn man einen Ethernet-Adapter hat, der �ber dietpi-config oder /etc/network/interfaces (als `allow-hotplug`-Ger�t) konfiguriert ist, aber das Kabel nicht angeschlossen ist, k�nnen betroffene Dienste verz�gert werden, bis die Schnittstelle zeitlich eingestellt ist aus.
- [DietPi-Backup](../../dietpi_tools/#dietpi-backup-backuprestore) :octicons-arrow-right-16: Eine neue Funktion wurde hinzugef�gt, die es erm�glicht, ein dietpi-Backup beim ersten Booten automatisch wiederherzustellen.

Setzen Sie dazu die neue Option `dietpi.txt`

�Sch
AUTO_SETUP_BACKUP_RESTORE=1
```

, um eine Liste der gefundenen Backups zur Auswahl zu erhalten (funktioniert nicht in Kombination mit `AUTO_SETUP_AUTOMATED=1`).

Alle angeschlossenen Laufwerke werden tempor�r gemountet und automatisch durchsucht.
Satz

�Sch
AUTO_SETUP_BACKUP_RESTORE=2
```

um das erste gefundene Backup nicht interaktiv wiederherstellen zu lassen (dies funktioniert in Kombination mit `AUTO_SETUP_AUTOMATED=1`).

Die Wiederherstellung l�uft nach dem ersten Update, funktioniert also auch mit �lteren Images und kann �ber eine SSH-Verbindung erfolgen. Credits gehen an @ravenclaw900 f�r die Implementierung dieser Funktion: <https://github.com/MichaIng/DietPi/pull/4112>.

- **DietPi-Backup** :octicons-arrow-right-16: Unterst�tzung f�r XFS- und ZFS-Zieldateisystemtypen wurde hinzugef�gt, die die erforderlichen Symlink- und POSIX-Berechtigungsfunktionen vollst�ndig unterst�tzen.
- **DietPi-Konfig** | **RPi** :octicons-arrow-right-16: Eine Option wurde hinzugef�gt, um die SPI-Schnittstelle umzuschalten. Vielen Dank an @incanus f�r die Wiederbelebung dieser alten Funktionsanfrage: <https://github.com/MichaIng/DietPi/issues/98#issuecomment-783650204>.
- **DietPi-Software** :octicons-arrow-right-16: Der obligatorische Neustart nach Installationen wurde entfernt. Installierte Dienste, die nicht von DietPi-Services gesteuert werden, sondern beim Neustart automatisch starten w�rden, werden jetzt stattdessen am Ende der Installation gestartet. Ein manueller Neustart ist immer noch eine gute Idee, aber nur in seltenen F�llen unbedingt erforderlich. Vielen Dank an @Games-Crack f�r diesen Vorschlag: <https://github.com/MichaIng/DietPi/issues/4032>.
- **DietPi-Software** :octicons-arrow-right-16: Installationen implizieren nicht mehr alle APT-Paket-Upgrades. W�hrend wir empfehlen, alle APT-Pakete regelm��ig zu aktualisieren, hilft Ihnen der neue t�gliche APT-Check und die Informationen im DietPi-Banner dabei, Sie auf dem Laufenden zu halten, damit Sie selbst die beste Entscheidung treffen k�nnen, ob und wann Sie welches Paket-Upgrade anwenden. Bei Erstinstallationen wird jedoch das vollst�ndige Upgrade beibehalten, um sicherzustellen, dass jedes Image im vollst�ndig aktualisierten Zustand startet und Pakete, die f�r die eigentliche Softwareauswahl, die Sie installieren, erforderlich sind, ebenfalls aktualisiert werden, wenn sie bereits installiert sind.
- **DietPi-Software** :octicons-arrow-right-16: Deinstallationen stoppen andere Dienste nicht mehr. Beispielsweise bleibt Ihr Webserver oder Media-Streaming-Server aktiv, w�hrend Sie andere Software deinstallieren, die Sie nicht mehr ben�tigen. Da Deinstallationen nicht viel RAM oder CPU-Ressourcen ben�tigen, ist dies vollkommen in Ordnung. Vielen Dank an @mrgreaper f�r den Hinweis: <https://github.com/MichaIng/DietPi/issues/4116>.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Bei Installation in Kombination mit Pi-hole, keine zus�tzlichen Konfigurationsdatei wird nicht mehr erstellt, aber die angepasste Schnittstellenbindung und der Port werden auf "/etc/unbound/unbound.conf.d/dietpi.conf" angewendet. Das Deklarieren von �interface� in zwei Konfigurationsdateien �berschreibt sich nicht gegenseitig, sondern f�hrt zu zwei gleichzeitigen Bindungen, was nicht beabsichtigt ist. Die beiden Dateien, falls vorhanden, werden beim DietPi-Update ebenfalls zusammengef�hrt. Es ist daher beabsichtigt, dass Administratoren �dietpi.conf� bei Bedarf direkt �ndern und diese Datei bei Neuinstallationen nicht �berschrieben wird, um lokale �nderungen beizubehalten. Dar�ber hinaus wird die Konfigurationsdatei bei Neuinstallationen besser sortiert und enth�lt Kommentare, um ihren Zweck zu erl�utern.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Bei Neuinstallationen wird nun standardm��ig der Zugriff gew�hrt alle privaten IPv4- und IPv6-Adressbereiche statt nur zum Subnetz �192.168.0.0/16�, das VPN-Schnittstellen, Container und F�lle mehrerer lokaler Netzwerke umfasst, an die der Server angeschlossen ist.
- **DietPi-Software** - **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wird jetzt ein monatlicher Cron-Job erstellt, um die Wurzel zu behalten Hinweisdatei aktualisiert. Vielen Dank an @APraxx f�r diesen Vorschlag: <https://github.com/MichaIng/DietPi/issues/4077>.
- **DietPi-Software** | **Python 3**: Bei `pip`- und pip-basierten Installationen auf ARMv6- und ARMv7-Boards wird das piwheels.org-Repository f�r vorkompilierte R�der automatisch hinzugef�gt, was die Build-Abh�ngigkeiten und die Kompilierzeit drastisch reduzieren kann.
- **DietPi-Software** | **[Node-RED](../../software/hardware_projects/#node-red)**: Neuinstallationen und Neuinstallationen mit Setup [Node-RED](../../software/hardware_projects/#node -red) als lokales Modul f�r den �geknoteten� Dienstbenutzer und nicht als globales Systemmodul/Befehl. Dadurch k�nnen alle zugeh�rigen Node-Module �ber die Webschnittstelle aktualisiert und entfernt werden, anstatt nur diejenigen, die �ber die Webschnittstelle installiert wurden. Zus�tzlich wurde ein Konsolen-Alias f�r den CLI-Befehl �node-red-admin� hinzugef�gt, sodass die Ausf�hrung dieses Befehls mit einem beliebigen Benutzer die lokale Node-RED-Instanz als �geknoteter� Dienstbenutzer aufruft.
- **DietPi-Software** | **[Docker](../../software/programming/#docker)**: Das Docker-APT-Repository wird jetzt manuell installiert, anstatt das offizielle Docker-Installationsprogramm zu verwenden. Dies erm�glicht es uns, die Docker-Installationsoption f�r Debian Bullseye-Systeme zu aktivieren, und sei es nur, um erweiterte Tests dieser kommenden Debian-Ver�ffentlichung mit DietPi zu erm�glichen.

### Aktualisierungen der Benutzeroberfl�che

- **DietPi-Banner** :octicons-arrow-right-16: Das Ausf�hren des Skripts ohne Eingabeargument �ffnet jetzt das Men�, anstatt das Banner zu drucken. Der Konsolen-Alias wurde entsprechend angepasst, sodass es nun m�glich ist, �dietpi-banner 0� und �dietpi-banner 1� von der Konsole aus auszuf�hren, um vollst�ndige und kurze Bannerversionen drucken zu lassen. Der Konsolenbefehl �dietpi-banner� �ffnet weiterhin das Men�.

### Fehlerbehebung

- **Audio** :octicons-arrow-right-16: Es wurde ein Fehler mit Debian Buster behoben, bei dem der ALSA-Status-Daemon immer lief, auch wenn er nicht konfiguriert war.
- **DietPi-Globals** | `G_OBTAIN_CPU_TEMP` :octicons-arrow-right-16: Negativen Temperaturen wird nicht mehr vertraut, stattdessen wird "N/A" ausgegeben. Dies erm�glicht einen generischen Ansatz, um die Temperatursch�tzung auf weiteren SBC-Modellen festzulegen/zuzulassen. Vielen Dank an [phpBB:Thanapat](https://dietpi.com/phpbb/memberlist.php?username=Thanapat){: class="nospellcheck"} f�r die Meldung eines verwandten Problems auf Roseapple Pi: <https://dietpi .com/phpbb/viewtopic.php?t=8677>
- **DietPi-Set_swapfile** :octicons-arrow-right-16: Behebung eines Problems, bei dem `zram`/`zram0` `dietpi.txt`-Pfadeintr�ge gel�scht wurden, wenn das Skript ohne Eingabeargumente ausgef�hrt wurde. Dies brach besonders beim Anwenden von `zram-swap` beim ersten Booten. Vielen Dank an @Dr0bac f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4002>
- **DietPi-Software** | **[Bitwarden_RS](../../software/cloud/#vaultwarden)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das selbstsignierte TLS-Zertifikat nicht auf iOS importiert werden konnte. Um diesen Fix auf eine vorhandene Instanz anzuwenden, muss die Konfigurationsdatei �/mnt/dietpi_userdata/bitwarden_rs/bitwarden_rs.env� entfernt oder an einen anderen Speicherort verschoben werden, damit �dietpi-software reinstall 183� die Konfiguration neu erstellt und TLS-Zertifikat.
- **DietPi-Software** | **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem w�hrend der Installation in Kombination mit Pi-hole der Neustart des Dienstes fehlschlagen konnte. Vielen Dank an @Ernstian f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2409#issuecomment-739154892>
- **DietPi-Software** | **[Unbound](../../software/dns_servers/#unbound)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der Dienststart fehlschlug, wenn das Hostsystem eine lokale IP-Adresse au�erhalb der 192.168.0.0/16 Subnetz. Vielen Dank an @faxesystem f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2409#issuecomment-749174984>
- **DietPi-Software** | **[ReadyMedia](../../software/media/#readymedia)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Medienbibliothek beim Dienststart nicht erneut gescannt wurde. Vielen Dank an @AdamFarnsworth0 f�r die Meldung dieses Problems: <https://twitter.com/AdamFarnsworth0/status/1347977813635305475>
- **DietPi-Software** | **[WiFi-Hotspot](../../software/advanced_networking/#wifi-hotspot)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation auf Armbian-basierten Images mit `RTL8188C*` WiFi erfolgte Chip ausgefallen. Vielen Dank an [phpBB:smogan71](https://dietpi.com/phpbb/memberlist.php?username=smogan71){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?t=8523>
- **DietPi-Software** | **[Medusa](../../software/bittorrent/#medusa)** :octicons-arrow-right-16: Diese Softwareoption wurde auf Stretch-Systemen deaktiviert, da sie jetzt Python >=3.6 erfordert, was ist nicht im Debian-Stretch-Repository verf�gbar. Wenn Sie Medusa auf einem Stretch-System ausf�hren, wird es weiterhin funktionieren, aber eine Aktualisierung ist entweder nicht m�glich oder bricht ab. Vielen Dank an @aermak f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/3991>
- **DietPi-Software** | **[WiringPi](../../software/hardware_projects/#wiringpi)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Installation fehlschlug, wenn das Verzeichnis `/usr/local/bin` war nicht anwesend. Vielen Dank an [phpBB:bruz](https://dietpi.com/phpbb/memberlist.php?username=bruz){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?t=8609>
- **DietPi-Software** | **[PaperMC](../../software/gaming/#papermc)** :octicons-arrow-right-16: Behebung eines Problems, bei dem die Installation aufgrund ge�nderter Download-URLs fehlgeschlagen ist, und stabilisierter Dienststart und Konfigurationserstellung durch Festlegen der Java-Heap-Gr��e und Einr�umen von mehr Zeit f�r den Start auf kleineren SBCs. Vielen Dank an [phpBB:omavoss](https://dietpi.com/phpbb/memberlist.php?username=omavoss){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?p=30191#p30191>
- **DietPi-Software** | **[OpenTyrian](../../software/gaming/#opentyrian)** :octicons-arrow-right-16: Die Installationsoption wurde auf x86_64 deaktiviert, da das Debian-Paket eine andere Dateistruktur hat und Es wurde auf 64-Bit-RPi-Systemen deaktiviert, da die Bin�rdatei f�r "armhf" kompiliert wurde.
- **DietPi-Software** | **[Domoticz](../../software/home_automation/#domoticz)** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Speichern benutzerdefinierter Skripte und das Starten mit einer Vorlage nicht funktionierten. Vielen Dank an [phpBB:tec13](https://dietpi.com/phpbb/memberlist.php?username=tec13){: class="nospellcheck"} f�r die Meldung dieses Problems: <https://dietpi.com/phpbb /viewtopic.php?t=8627>
- **DietPi-Software** :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem f�r [ruTorrent](../../software/bittorrent/#rtorrent), [Koel](../../ software/media/#koel) und [Bitwarden_RS](../../software/cloud/#vaultwarden) schlug die automatische Erkennung der neuesten Version fehl und stattdessen wurde ein m�glicherweise �lteres Fallback verwendet. Vielen Dank an @kelvmod f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4105>
- **DietPi-Software** | **[LXQt](../../software/desktop/#lxqt)** :octicons-arrow-right-16: Visuelle Probleme mit unserer Standardkonfiguration von Debian Buster behoben, die von uns gelieferten Dateien drastisch vereinfacht und bereinigt .
- **DietPi-Software** | **[SABnzbd](../../software/bittorrent/#sabnzbd)** :octicons-arrow-right-16: Es wurde ein Problem auf Stretch behoben, bei dem die Installation aufgrund eines erh�hten Minimums [Python](../) fehlschlug ../software/programming/#python-3) Version mit SABnzbd v3.2.0. Wenn Python 3.5 installiert ist, wird jetzt SABnzbd v3.1.1 installiert, damit die Installationsoption vorerst aktiviert bleibt. Vielen Dank an @19eighties f�r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/2762#issuecomment-787118995>

!!! Hinweis ""

Wie immer wurden viele kleinere Codeleistungs- und Stabilit�tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code�nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4126>
