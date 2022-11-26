# Versionshinweise

## Oktober 2021 (Version 7.7)

### &Uuml;berblick

Willkommen zur **Ver&ouml;ffentlichung vom Oktober 2021** :octicons-heart-16: von **DietPi**. Es ist eine inkrementelle Version, die sich auf Verbesserungen an den Skripten und Softwarepaketen konzentriert und die Art und Weise verbessert, wie Sie **DietPi** verwenden.

![DietPi Version 7.7](../assets/images/dietpi-version-77.jpg){: width="320" height="427" loading="lazy"}

!!! zitiere "_Foto von planet_fox, Pixabay_"

### Verbesserungen {: #verbesserungen-77 }

**DietPi-Software**:

- [**DietPi-JustBoom**](../../dietpi_tools/#dietpi-justboom) :octicons-arrow-right-16: M&ouml;glichkeit hinzugef&uuml;gt, eine Ausgabekanalanzahl zu erzwingen oder ein Audioformat nicht zu erzwingen -Wert, um das Eingabestreamformat beizubehalten, oder die Konvertierung ALSA &uuml;berlassen, was jetzt die Standardeinstellung beim Zur&uuml;cksetzen der Einstellungen ist. Ebenso kann der Audioausgabepuffer jetzt deaktiviert werden, um die MPD-Standardeinstellung beizubehalten. Wenn dies aus einem bestimmten Grund nicht erforderlich ist, wird im Allgemeinen empfohlen, den Audiostream nicht zu konvertieren und diese Einstellungen unver&auml;ndert/standardm&auml;&szlig;ig beizubehalten.

- [**Sintflut**](../../software/bittorrent/#sintflut):

- Die Protokollierung erfolgt nicht mehr nach `/var/log/deluged/`, sondern stattdessen ins Journal, erreichbar &uuml;ber `journalctl -u deluged -u deluge-web`. Diese &Auml;nderung wirkt sich nur auf Neuinstallationen und Neuinstallationen von Deluge aus.
- Bei Neuinstallationen ist die Webschnittstelle jetzt wie erwartet mit dem gew&auml;hlten globalen Softwarepasswort zug&auml;nglich, das mit einem frischen zuf&auml;lligen Salz gehasht gespeichert wird. Fr&uuml;her war das Passwort fest auf `dietpi` codiert.
– Behebung eines Problems bei Bullseye, bei dem der Webschnittstellendienst nicht gestartet wurde, da ein neues Befehlszeilen-Flag `-d` erforderlich ist, um ihn im Vordergrund zu halten. Vielen Dank an @quyentruong f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4785>

- [**Kodi**](../../software/media/#kodi):

- Auf Debian Bullseye, beginnend mit Kodi 19, ist die `GBM`-Unterst&uuml;tzung standardm&auml;&szlig;ig vorhanden, was bedeutet, dass [**Kodi**](../../software/media/#kodi) ohne ein umschlie&szlig;endes X gestartet werden kann Server. Dies geschieht jetzt standardm&auml;&szlig;ig beim Start von Kodi au&szlig;erhalb einer Desktop-Sitzung, einschlie&szlig;lich der Option dietpi-autostart. Das bedeutet auch, dass ein X-Server nicht mehr als Abh&auml;ngigkeit von Kodi installiert wird, sondern nur noch als Abh&auml;ngigkeit einer Desktop-Umgebung.
- Es kann jetzt auf allen Ger&auml;ten installiert werden. In einigen F&auml;llen kann die Videowiedergabeleistung schlecht sein, abh&auml;ngig von der GPU, ob gute Treiber verf&uuml;gbar sind und nat&uuml;rlich von der Videoqualit&auml;t. Es sollten jedoch unsere Benutzer anstelle von uns sein, die beurteilen, ob es ausreichend ist oder nicht. Mit Debian Bullseye, neuen Mesa-Treibern und Kodi 19, gestartet &uuml;ber `GBM`, sollte die Leistung viel besser sein als bei &auml;lteren Debian-/Paketversionen.
– Es wurde ein Problem auf RPi ARMv8/64-Bit-Systemen behoben, bei dem Kodi nicht gestartet werden konnte, wenn es ohne Desktop installiert wurde. Vielen Dank an @Klola f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?p=38079#p38079).

- [Dateibrowser](../../software/cloud/#file-browser) :octicons-arrow-right-16: Der Standard-Netzwerkport wurde auf `8084` ge&auml;ndert, um einen Konflikt mit [HTPC Manager] zu l&ouml;sen (../../software/bittorrent/#htpc-manager). Dies betrifft nur **neue** [Dateibrowser](../../software/cloud/#file-browser)-Installationen. Vielen Dank an @KamikazeePL f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?t=9507).

**Netzwerk- und Druckschnittstelle**:

- **Allgemein** :octicons-arrow-right-16: Das Skript `/boot/dietpi/func/obtain_network_details` wurde entfernt, einschlie&szlig;lich der zugeh&ouml;rigen Datei `/run/dietpi/.network`, um Netzwerkdetails abzurufen. Alle Verwendungen dieser Dateien wurden durch die neue Funktion `G_GET_NET` von DietPi-Globals ersetzt (siehe unten).
- **DietPi-Globals** :octicons-arrow-right-16: Eine neue globale Funktion `G_GET_NET` wurde hinzugef&uuml;gt, um Netzwerkschnittstellendetails zu drucken. Am wichtigsten ist, dass es Informationen f&uuml;r die Hauptschnittstelle ausgibt, indem es den Priorit&auml;ten von `/boot/dietpi/func/obtain_network_details folgt: Standard-Gateway => Status UP => IP zugewiesen`, aber es erlaubt zus&auml;tzlich nach IP-Familie, Typ, Schnittstellenname zu filtern oder drucken Sie das Standard-Gateway explizit aus. Es soll ein Ersatz f&uuml;r `/boot/dietpi/func/obtain_network_details` mit mehr Flexibilit&auml;t sein und es erm&ouml;glichen, immer aktuelle Schnittstelleninformationen abzuleiten, anstatt von der Korrektheit einer Cache-Datei abh&auml;ngig zu sein.
- DietPi-Globals | `G_GET_WAN_IP` :octicons-arrow-right-16: Wir verwenden jetzt unseren eigenen GEO-IP-Dienst, um die WAN-IP und den Standort des Systems im DietPi-Banner und DietPi-VPN anzuzeigen. Bei der Verwendung von Pi-hole wurde mit einem fr&uuml;heren Update `freegeoip.app` zur Whitelist von Pi-hole hinzugef&uuml;gt, was jetzt nicht mehr erforderlich ist. Sie k&ouml;nnen diesen Eintrag daher von der Whitelist entfernen.
- DietPi-Boot :octicons-arrow-right-16: Dieses Skript und dieser Dienst wurden entfernt: Das Warten auf das Netzwerk erfolgt jetzt &uuml;ber `DietPi-PostBoot` `"After=network-online.target"`, die Zeitsynchronisierung erfolgt in `DietPi-PostBoot`, aber im Hintergrund (meistens nicht erforderlich f&uuml;r Dienststarts) und vorinstalliertes Image-Stage-Handling wird jetzt auch in PostBoot durchgef&uuml;hrt.
- DietPi-Update :octicons-arrow-right-16: Eine &Uuml;berpr&uuml;fung der Netzwerkverbindung und der Zeitsynchronisierung wird jetzt durchgef&uuml;hrt, bevor nach Updates gesucht wird, &auml;hnlich wie es die `DietPi-Software` bei Installationen tut.

**Zeitsynchronization**:

- Verwenden Sie dieselbe Flag-Datei, die `systemd-timesyncd` selbst seit Buster verwendet, um einen zus&auml;tzlichen Neustart des Dienstes zu &uuml;berspringen und zu synchronisieren, wenn dies bereits geschehen ist.
- Wenn unsere Oneshot-Modi (nur booten, st&uuml;ndlich, t&auml;glich) ausgew&auml;hlt sind, ist `systemd-timesyncd` jetzt "aktiviert", um von systemd fr&uuml;her beim Booten gestartet zu werden, anstatt bei unserem Skriptaufruf. Zumal beide jetzt die gleiche Flag-Datei teilen (auf Buster und h&ouml;her), hat dies eine Chance, einen zus&auml;tzlichen Neustart des Dienstes zu verhindern, wenn die Zeitsynchronisierung bereits beendet ist, wenn PostBoot erreicht ist.

**DietPi-Login**:

- Das DietPi-Banner beim Login wird nicht mehr angezeigt, wenn `~/.hushlogin` existiert, was eine g&auml;ngige Methode ist, um zu verhindern, dass die Shell beim Login `/etc/motd` ausgibt, und sollte daher f&uuml;r das DietPi-Banner als respektiert werden Gut. Vielen Dank an @dnknth f&uuml;r diesen Vorschlag: <https://github.com/MichaIng/DietPi/issues/4786>

**Andere &Auml;nderungen**:

- **DietPi-Globals** :octicons-arrow-right-16: Die globalen Funktionen `G_DEV_1` und `G_DEV_BENCH` wurden entfernt, die nur zu Test- und Entwicklungszwecken existierten, aber in unseren aktuellen Arbeitsabl&auml;ufen nicht verwendet werden.

### Fehlerbehebungen {: #bug-fixes-77 }

**DietPi-Software-Korrekturen**:

- [DietPi-Software | **DietPi-JustBoom**](../../dietpi_tools/#dietpi-justboom) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Anwenden einiger MPD-Einstellungen nicht funktionierte. Vielen Dank an @elevader f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?t=9426).
- **DietPi-Software** :octicons-arrow-right-16: Behebung eines Problems, bei dem Softwaredienste mit einer kryptischen Fehlermeldung fehlschlugen, wenn ein erwartetes Verzeichnis nicht vorhanden war. Dies wurde insbesondere bei [Sonarr](../../software/bittorrent/#sonarr) und [Radarr](../../software/bittorrent/#radarr) gemeldet, wenn deren Logverzeichnis aus irgendeinem Grund fehlte . Wenn Verzeichnisse fehlen, die innerhalb des systemd-Dienstes explizit als schreib- und lesbar aufgef&uuml;hrt sind, gibt systemd `Failed at step NAMESPACE spawning` aus, w&auml;hrend [Sonarr](../../software/bittorrent/#sonarr) und [Radarr ](../../software/bittorrent/#radarr) selbst w&uuml;rde eine deutlichere Fehlermeldung &uuml;ber das fehlende Protokollverzeichnis ausgeben. Vielen Dank an @stevewitz f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?t=9463).
- [DietPi-Software | **Lighttpd**](../../software/webserver_stack/#lighttpd) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Upgrade von Buster auf Bullseye gem&auml;&szlig; unserer Anleitung fehlschl&auml;gt, wenn HTTPS &uuml;ber aktiviert wurde DietPi-LetsEncrypt vor. Vielen Dank an @fhals f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?t=9477).
- [DietPi-Software | **Home Assistant**](../../software/home_automation/#home-assistant) :octicons-arrow-right-16: Die mit Home Assistant kompilierte Python-Version wurde auf v3.9.7 angehoben, wodurch und behoben werden Problem mit Installationen auf 32-Bit-ARM-Systemen. Vielen Dank an @Przemek f&uuml;r die Meldung dieses Problems: [MichaIng/DietPi#4372](https://github.com/MichaIng/DietPi/issues/4372#issuecomment-936656595)
- [DietPi-Software | **Home Assistant**](../../software/home_automation/#home-assistant) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem Home Assistant aufgrund neu erforderlicher Laufzeitbibliotheken auf ARM-Systemen nicht gestartet wurde .
- [DietPi-Software | **Chromium**](../../software/desktop/#chromium) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem die Autostart-Option nicht funktionierte, wenn Chromium ohne Desktop installiert wurde. Vielen Dank an @jowelboy f&uuml;r die Meldung dieses Problems [im DietPi-Forum](https://dietpi.com/phpbb/viewtopic.php?t=9531).
- [DietPi-Software | **Chromium**](../../software/desktop/#chromium) :octicons-arrow-right-16: Behebung eines Problems auf RPi, bei dem das Starten von Chromium aufgrund einer fehlenden Abh&auml;ngigkeit fehlschlug, wenn kein Desktop installiert war. Vielen Dank an @Loader23 f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4782>
- DietPi-Software | X.Org X Server :octicons-arrow-right-16: Es wurde ein Problem mit Odroid N2- und C4-Modellen behoben, bei dem die Installation aufgrund eines Tippfehlers fehlschlug. Vielen Dank an @wiml f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4830>
- [DietPi-Software | **Airsonic**](../../software/media/#airsonic) :octicons-arrow-right-16: Da das Projekt archiviert wurde und Java 17 nicht unterst&uuml;tzt, wurde es auf Bullseye deaktiviert. Wir beobachten einen Fork (<https://github.com/airsonic-advanced/airsonic-advanced>), der aktiv entwickelt wird und bei dem zumindest das Webinterface mit Java 17 funktioniert. Das Abspielen von Audio schlug jedoch bei lokalen Tests fehl, daher Wir werden warten, bis es stabiler wird, um ein Drop-in-Ersatz f&uuml;r Airsonic im Allgemeinen zu sein und auch auf Bullseye mit Java 17 unterst&uuml;tzt zu werden. Vielen Dank an @Andaloup f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4847>
- [DietPi-Software | **FreshRSS**](../../software/social/#freshrss) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem verschachtelte /opt/FreshRSS/FreshRSS-master und /opt/FreshRSS/ neu installiert wurden. p/p wurden erstellt. Da FreshRSS &uuml;ber einen internen Updater verf&uuml;gt, werden Neuinstallationen die neue Version nicht herunterladen und installieren, solange /opt/FreshRSS bereits vorhanden ist. Das verschachtelte Verzeichnis und der Link werden beim n&auml;chsten DietPi-Update entfernt, sofern vorhanden. Vielen Dank an @kinoushe f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4775>

**Allgemeine DietPi- und Konfigurationstools**:

- **Allgemein** :octicons-arrow-right-16: Da der Armbian-Repository-Router HTTPS bei Umleitungen noch nicht zuverl&auml;ssig beibeh&auml;lt, schl&auml;gt APT manchmal fehl, wenn ein Downgrade von HTTPS auf HTTP erkannt wird. Wir &auml;ndern daher die `armbian.list`, um einfaches HTTP zu verwenden, bis die Probleme mit dem Router behoben sind.
- **Allgemein** :octicons-arrow-right-16: Umgehung eines Problems auf Debian Stretch, bei dem `systemctl enable/disable --now` den Dienst unter bestimmten Umst&auml;nden nicht startet/stoppt. Dies wird in unserem Fehlerhandler `G_EXEC` behoben, daher k&ouml;nnen Sie beim manuellen Aufruf von `systemctl` immer noch damit konfrontiert werden: <https://github.com/MichaIng/DietPi/issues/4815>
- **Allgemein** :octicons-arrow-right-16: Es wurde eine Problemumgehung auf Bullseye-Systemen mit &auml;lteren Linux-Versionen (v4.14 und darunter) angewendet, die die neue einheitliche `cgroup-Hierarchie` (auch bekannt als `cgroups-v2 `). Da das neuere systemd versucht, es automatisch zu verwenden, scheitern Docker und &auml;hnliche Software, die `cgroups` verwenden. Bei Ger&auml;ten mit bekannter Boot-Konfigurationsdatei werden die Kernel-Befehlszeilenargumente angewendet, um die Verwendung der alten `cgroups`-Hierarchie zu erzwingen.
- [**DietPi-Backup**](../../dietpi_tools/#dietpi-backup-backuprestore) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das L&ouml;schen des PATH-Cache &uuml;ber den Befehl `hash` nicht funktionierte funktionieren ab einem falschen Kommandozeilenargument: <https://github.com/MichaIng/DietPi/issues/4800>
- [DietPi-LetsEncrypt](../../dietpi_tools/#dietpi-letsencrypt) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem das Skript fehlschlug, wenn [ownCloud](../../software/cloud /#owncloud) oder [Nextcloud](../../software/cloud/#nextcloud) installiert wurden. Vielen Dank an @billouetaudrey f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4752>
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Es wurde ein Problem behoben, bei dem der WiFi-Verbindungsstatus f&auml;lschlicherweise als versehentlich das Ethernet erhalten werden konnte Schnittstellenindex wurde verwendet, um es abzuleiten.
- [**DietPi-Config**](../../dietpi_tools/#dietpi-configuration) :octicons-arrow-right-16: Behebung eines Problems auf [NanoPi NEO](../../hardware/ #nanopi-series-friendlyarm) (und wahrscheinlich andere Allwinner H3 SBCs), wo die Auswahl einer Soundkarte fehlschlug, da versucht wurde, eine ung&uuml;ltige Steuerung einzustellen. Vielen Dank an @VS-X f&uuml;r die Meldung dieses Problems: <https://github.com/MichaIng/DietPi/issues/4833>

Wie immer wurden viele kleinere Codeleistungs- und Stabilit&auml;tsverbesserungen sowie visuelle und Rechtschreibkorrekturen vorgenommen, zu viel, um sie alle hier aufzulisten. Sehen Sie sich alle Code&auml;nderungen dieser Version auf GitHub an: <https://github.com/MichaIng/DietPi/pull/4840>.

### Entfernte Software {: #removed-software-77 }

- **CouchPotato** :octicons-arrow-right-16: Leider wird das CouchPotato-Projekt nicht mehr gepflegt und wurde aufgegeben. Infolgedessen mussten wir es von DietPi entfernen. Die auf Ihrem System installierte Instanz bleibt erhalten, wird aber nicht mehr &uuml;ber die DietPi-Konfigurationstools verwaltet (sie kann nicht mehr installiert, neu installiert oder deinstalliert werden). Wir empfehlen, auf ein alternatives Projekt zu migrieren, wie [**Radarr**](../../software/bittorrent/#radarr), das in **DietPi-Software** gut zu finden ist. Bitte finden Sie [hier](https://github.com/MichaIng/DietPi/issues/4323#issuecomment-927128724) Deinstallationsanweisungen f&uuml;r eine manuelle Entfernung von CouchPotato.
