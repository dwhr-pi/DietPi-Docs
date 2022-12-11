# Entwicklung & Programmierung

## &Uuml;berblick

- [**Python 3 - Hochrangige interpretierte Programmiersprache**](#python-3)
- [**Go - Programmiersprache**](#go)
- [**Node.js - Open-Source, JavaScript-Laufzeitumgebung**](../webserver_stack/#nodejs)
- [**Docker – Anwendungen mithilfe von Containern erstellen, bereitstellen und ausf&uuml;hren**](#docker)
- [**Docker Compose - Docker-Anwendungen mit mehreren Containern definieren und ausf&uuml;hren**](#docker-compose)
- [**Portainer - Lightweight Management UI, Verwaltung Ihres Docker-Hosts oder Swarm-Clusters**](#portainer)
- [**VSCodium - FLOSS-Version von Microsoft VSCode**](#vscodium)

??? Information "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef&uuml;hrten **DietPi-optimierten Softwareelemente** zu installieren, f&uuml;hren Sie es &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software durchsuchen** und w&auml;hlen Sie einen oder mehrere Artikel aus. W&auml;hlen Sie abschlie&szlig;end `Installieren`.
    DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

##Python 3

Python ist eine textbasierte interpretierte Programmiersprache mit objektorientierten Programmieroptionen f&uuml;r allgemeine Anwendungen.

![Python-Logo](../assets/images/dietpi-software-programming-pythonlogo.png){: width="200" height="59" loading="lazy"}

Quelle: Von [www.python.org](https://www.python.org/community/logos/), [GPL](https://commons.wikimedia.org/w/index.php?curid=34991637 )

Sie finden Python &uuml;berall in der Welt der Computerprogrammierung. Beispielsweise ist Python die Grundlage einiger der weltweit beliebtesten Websites [^3], darunter Reddit, Dropbox und YouTube, um nur einige zu nennen. Das Python-Webframework [Django](https://www.djangoproject.com) unterst&uuml;tzt sowohl Instagram als auch Pinterest.

Derzeit ist Python die drittbeliebteste Programmiersprache [^4].

=== "Installationsdetails"

    Die Installationsoption installiert ausdr&uuml;cklich nur **Python 3**.
    Der Python-Paketmanager `pip`/`pip3` und Entwicklungsheader sind enthalten.
    Um den `pip`-Paketmanager zu verwenden, ist eine typische Verwendung `pip3 install -U <module>`.

=== "Python-IDE-Pakete"

    Es sind viele Python-IDE-Pakete verf&uuml;gbar. Es folgt eine kurze Liste bekannter und weithin akzeptierter IDE-Pakete (alphabetische Reihenfolge):

    | Name                | URL                                                    |
    | :-----------------: | ------------------------------------------------------ |
    | **Atom**            | <https://atom.io>                                      |
    | **Eclipse + Pydev** | <https://www.eclipse.org> und <https://www.pydev.org/> |
    | **LEERLAUF**        | <https://docs.python.org/3/library/idle.html>          |
    | **Pycharm**         | <https://www.jetbrains.com/pycharm>                    |
    | **Spyder**          | <https://github.com/spyder-ide/spyder>                 |
    | **Thonny**          | <https://thony.org>                                    |
    | **VSCodium**        | [VSCodium](#vscodium) unten                            |

***

Website: <https://www.python.org>
Offizielle Dokumentation, vom Anf&auml;nger bis zum Fortgeschrittenen: <https://www.python.org/doc/>
Verwendung von Python: Ihre ersten Schritte <https://realpython.com/python-first-steps/>
Wikipedia: <https://wikipedia.org/wiki/Python_(programming_language)>

## Go

Go ist eine Open-Source-Programmiersprache, die es einfach macht, einfache, zuverl&auml;ssige und effiziente Software zu erstellen.

![DietPi Go Open-Source-Programmiersprache](../assets/images/dietpi-software-programming-golang.svg)

Quelle: Von [https://golang.org](https://blog.golang.org/go-brand), Creative Commons Attribution 3.0

Go ist eine kompilierte, schnelle und leistungsstarke Sprache, die einfach sein soll und leicht zu lesen und zu verstehen ist. Go wurde bei Google von Rob Pike, Robert Griesemer und Ken Thompson entwickelt und erschien erstmals im November 2009.

Go wird von einigen der gro&szlig;en Organisationen wie Google, BBC, Uber, Soundcloud, Twitch, Medium, Daily Motion[^2] verwendet. Uber hat einen besseren Durchsatz, eine h&ouml;here Leistung, Latenz und Betriebszeit gemeldet. BBC, der Hausname f&uuml;r die Ausstrahlung von Weltnachrichten, verwendet es f&uuml;r das Backend, einschlie&szlig;lich Crawler und Web Scraper. Das Build- und Bereitstellungssystem von Soundcloud befindet sich in Go.

=== "Erste Schritte"

    Um den Code zu bearbeiten, k&ouml;nnen Sie einen Editor Ihrer Wahl verwenden oder [VSCodium](#vscodium) verwenden. Die in VSCodium verf&uuml;gbare _Go-Erweiterung_ bietet umfassende Sprachunterst&uuml;tzung f&uuml;r die Programmiersprache Go.

    Nur um einen Vorgeschmack zu bekommen, k&ouml;nnten Sie einige Befehle in [_Go Spielplatz_](https://play.golang.org/p/AAX1cLCmA1c) ausf&uuml;hren.

    Sehen Sie sich auch das offizielle Tutorial [Erste Schritte mit Go] an (https://golang.org/doc/tutorial/getting-started).

=== "Installieren / Deinstallieren"

    - Wir haben auf automatische Go-Versionserkennung umgestellt. Hier ist ein Beispiel:

        ```sh
        root@DietPi3:~# go version
        go version go1.16.3 linux/arm
        ```

    - Wenn das Go-Paket deinstalliert wird, bleibt der Ordner `/mnt/dietpi_userdata/go` erhalten.
      Dies ist der Ort, an dem Pakete installiert werden, benutzerdefinierte Kompilierungen ausgef&uuml;hrt werden, Quellen heruntergeladen werden usw.

        Es ist besonders wichtig, `/mnt/dietpi_userdata/go` beizubehalten, solange wir kein gutes Abh&auml;ngigkeitssystem haben, das die Deinstallation von Abh&auml;ngigkeiten blockiert. Andernfalls w&auml;re es m&ouml;glich, Go zu deinstallieren, w&auml;hrend [OpenBazaar](../social/#openbazaar) noch installiert ist.
        Als Nebeneffekt w&uuml;rde das Entfernen von `/mnt/dietpi_userdata/go` bedeuten, dass auch [OpenBazaar](../social/#openbazaar) entfernt wird.

=== "Verzeichnisse"

    - `/mnt/dietpi_userdata/go`: Dies ist der Ort, an dem Pakete installiert, benutzerdefinierte Kompilierungen ausgef&uuml;hrt, Quellen heruntergeladen werden usw.
       Dieser Pfad ist in der Umgebungsvariable GOPATH angegeben.

        !!! note "GOPATH ist eine globale Einstellung"
        In normalen Go-Installationen ist GOPATH eine benutzerspezifische Umgebungsvariable. In DietPi ist es global, dh alle Benutzer haben den gleichen Modul-Cache und alle sehen die gleichen Binaries unterhalb von GOPATH/bin.

    - `/usr/local/go`: Dies ist der Ort, an dem das Go-Paket installiert ist.
    - `/mnt/dietpi_userdata/go/pkg/mod`: Dies ist der Pfad f&uuml;r Go-Pakete von Drittanbietern. Darauf weist die Umgebungsvariable GOMODCACHE hin.

=== "Erste Schritte"

    Einige g&auml;ngige Go-Befehle sind:

    - `go version`: Druckt die installierte Go-Version
    - `go env`: Druckt die internen Umgebungsvariablen von Go (zB GOPATH). Kann auch zB wie `$(go env GOPATH)/bin` verwendet werden
    - `go mod tidy <MODULNAME>`: Generiert ein Go-Modul
    - `go help`: Startet die Go-interne Hilfe allgemein, Details f&uuml;r Befehle zB &uuml;ber `go help build`

=== "Auf neueste Version aktualisieren"

    ```sh
    dietpi-software reinstall 188
    ```

    Um die Installation zu &uuml;berpr&uuml;fen, f&uuml;hren Sie `go version` aus.

    Siehe auch <https://golang.org/doc/install> bzw
    <https://gist.github.com/nikhita/432436d570b89cab172dcf2894465753>.

***

Website: <https://golang.org>
Offizielle Dokumentation, Referenzen und F&uuml;hrungen von Go-Programmen: <https://golang.org/doc>
Eine Beispielquelle zum Graben f&uuml;r Go-Bibliotheken: <https://github.com/avelino/awesome-go>
Wikipedia: <https://en.wikipedia.org/wiki/Go_(programming_language)>

## Docker

2013 f&uuml;hrte Docker Container ein. Dabei handelt es sich um eine standardisierte Softwareeinheit, die es Entwicklern erm&ouml;glicht, ihre Anwendung von der Umgebung zu isolieren. Docker ist der De-facto-Standard zum Erstellen und Freigeben von containerisierten Anwendungen – von Einplatinencomputern (SBC) bis hin zu Desktops oder Clouds.

Ein Docker-Container-Image ist ein einfaches, eigenst&auml;ndiges, ausf&uuml;hrbares Softwarepaket, das alles enth&auml;lt, was zum Ausf&uuml;hren einer Anwendung erforderlich ist: Code, Laufzeit, Systemtools, Systembibliotheken und Einstellungen.

<!-- ![Docker-Logo](../assets/images/dietpi-software-programming-docker1.svg){: width="200" height="???" loading="faul"} -->
![Docker-Funktionsblockdiagramm](../assets/images/dietpi-software-programming-docker2.svg){: width="400" height="369" loading="lazy"}

Quelle: [Benutzer: `Maklaan` - Basierend auf einem Docker-Blogbeitrag] (https://commons.wikimedia.org/w/index.php?curid=37965701)

=== "Protokolle anzeigen"

    Auf Docker-Protokolle kann mit dem n&auml;chsten Befehl zugegriffen werden:

    ```sh
    journalctl -u docker -u containerd
    ```

=== "Konfigurationsdateien"

    Der Speicherort der Docker-Konfigurationsdateien:

    - Docker: `/etc/docker/daemon.json`
    - containerd: `/etc/containerd/config.toml`

***

Offizielle Dokumentation: <https://docs.docker.com/get-started/overview>
Konfigurationsdatei: <https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file>
Protokollierung: <https://docs.docker.com/config/containers/logging/configure>
Wikipedia: <https://wikipedia.org/wiki/Docker_(software)>

Eine kurze Einf&uuml;hrung finden Sie unter **DietPi Docker Setup auf Raspberry Pi 3 B Plus**:

<iframe src="https://www.youtube-nocookie.com/embed/y_VfLOGm5nA?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

## Docker Compose

Docker Compose ist ein [Docker](#docker)-Tool zum Definieren und Ausf&uuml;hren von Multi-Container-Anwendungen. Mit Compose verwenden Sie eine `YAML`-Datei, um die Dienste Ihrer Anwendung aus dieser Konfigurationsdatei zu erstellen und zu konfigurieren.

`docker-compose` ist ein hervorragendes Tool f&uuml;r Entwicklungs-, Test-, Continuous Integration (CI)-Workflows und Staging-Umgebungen.

<!-- ![Docker Compose-Logo](https://raw.githubusercontent.com/docker/compose/master/logo.png) -->
![docker compose](../assets/images/dietpi-docker-compose.png){: width="500" height="351" loading="lazy"}

_Docker (einzelner Container) vs. Docker-Compose (mehrere Container) - Quelle: [A Beginner's Guide to Docker](https://www.freecodecamp.org/news/a-beginners-guide-to-docker-how-to -erstelle-einen-client-serverseitig-mit-docker-compose-12c8cf0ae0aa/)_

=== "Auf neueste Version aktualisieren"

    Das Tool steht kurz nach der Installation zur Verf&uuml;gung. Falls Sie es aktualisieren m&uuml;ssen, hier ist der Befehl:

    ```sh
    sudo pip3 install docker-compose --upgrade
    ```

***

Offizielle Dokumentation: <https://docs.docker.com/compose>
Erste Schritte: <https://docs.docker.com/compose/gettingstarted>
Beispiel-Apps mit Compose: <https://docs.docker.com/compose/samples-for-compose/>
Versionshinweise: <https://docs.docker.com/compose/release-notes/>
Wikipedia: <https://wikipedia.org/wiki/Docker_(software)>

## Portainer

Portainer vereinfacht Ihr Docker-Container-Management &uuml;ber die Portainer-Weboberfl&auml;che. Es erm&ouml;glicht eine schnellere Bereitstellung der Anwendungen und bietet Transparenz in Echtzeit.

![Portainer-Screenshot](../assets/images/dietpi-software-portainer.jpg){: width="1159" height="636" loading="lazy"}

=== "Zugriff auf die Weboberfl&auml;che"

    Das Webinterface ist &uuml;ber Port **9002**[^1] erreichbar:

    - URL = `http://<Ihre.IP>:9002`

=== "Auf neueste Version aktualisieren"

    Um Portainer zu aktualisieren, installieren Sie ihn einfach neu:

    ```sh
    dietpi-software reinstall 185
    ```

***

Offizielle Dokumentation: <https://documentation.portainer.io>
Anf&auml;ngerleitfaden: <https://codeopolis.com/posts/beginners-guide-to-portainer/>
Quellcode: <https://github.com/portainer/portainer>
Open-Source-Lizenz: [zlib](https://github.com/portainer/portainer/blob/develop/LICENSE)

## VSCodium

VSCodium ist eine FLOSS-Version von [Microsofts Visual Studio-Code](https://code.visualstudio.com/), die direkt aus der Quelle auf GitHub erstellt wurde, ohne Branding, Nachverfolgung oder Telemetrie.

![VSCodium-Screenshot](../assets/images/dietpi-software-programming-vscodium.png){: width="1028" height="799" loading="lazy"}

=== "Auf neueste Version aktualisieren"

    VSCodium wird als APT-Paket installiert, daher k&ouml;nnen Sie es aktualisieren, indem Sie die folgenden Befehle ausf&uuml;hren:

    ```sh
    apt update
    apt install codium
    ```

Dokumentation (Visual Studio Code): <https://code.visualstudio.com/docs>
Dokumentation (VSCodium): <https://github.com/VSCodium/vscodium/blob/master/DOCS.md>
Quellcode: <https://github.com/VSCodium/vscodium>
Lizenz: [MIT](https://github.com/VSCodium/vscodium/blob/master/LICENSE)

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

[^1]:
[Logitech Media Server](../media/#logitech-media-server) hat Port `9000` bereits abgeh&ouml;rt, und deshalb wurde **Portainer** so konfiguriert, dass er mit der Verwendung von Port `9002` beginnt. Weitere Details zur Implementierung von Portainer in DietPi finden Sie im GitHub-Task: <https://github.com/MichaIng/DietPi/pull/3933>

[^2]: [7 ber&uuml;hmteste Unternehmen, die Golang verwenden](https://www.agiratech.com/blog/companies-using-golang/)

[^3]: [8 erstklassige Softwareunternehmen, die Python verwenden](https://realpython.com/world-class-companies-using-python/)

[^4]: [Index der TIOBE-Programmiergemeinschaft](https://www.tiobe.com/tiobe-index/)
