# Datenbanken und Datenspeicher

## &Uuml;berblick

- [**MariaDB** - relationale Open-Source-Datenbank](#mariadb)
- [**phpMyAdmin** - SQL-Administrationstool f&uuml;r MariaDB](#phpmyadmin)
- [**SQLite** - Kleine, schnelle und hochzuverl&auml;ssige SQL-Datenbank-Engine](#sqlite)
- [**Redis** - Open-Source-In-Memory-Schl&uuml;sselwert-Datenspeicher](#redis)
- [**InfluxDB** - Open-Source-Zeitreihendatenbank](#influxdb)
- [**PostgreSQL** - Persistente und fortschrittliche SQL-Datenbank-Engine](#postgresql)

??? Information "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**?"
    Um eine der unten aufgef&uuml;hrten **DietPi-optimierten Software** zu installieren, f&uuml;hren Sie sie &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software-optimiert** und w&auml;hlen Sie einen oder mehrere Artikel aus. Klicken Sie abschlie&szlig;end auf `Installieren`. DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

## MariaDB

**MariaDB** Server ist eine der beliebtesten relationalen Open-Source-Datenbanken. Es wurde von den urspr&uuml;nglichen Entwicklern von MySQL erstellt und bleibt garantiert Open Source[^1]. Es ist Teil der meisten Cloud-Angebote und der Standard in den meisten Linux-Distributionen.

![MariaDB-Logo](../assets/images/dietpi-software-webstack-mariadb.png){: width="200" height="61" loading="lazy"}

Quelle: [MariaDB](https://mariadb.com/), [LGPL](https://commons.wikimedia.org/w/index.php?curid=55946550).

=== "Schnellzugriff"

    F&uuml;hren Sie als `root`-Benutzer `mariadb` von der Befehlszeile aus, es ist keine separate Authentifizierung erforderlich. Beachten Sie jedoch, dass dies nicht &uuml;ber sudo funktioniert, sondern eine interaktive Root-Benutzer-Shell-Sitzung erforderlich ist.

    - Benutzername = `root`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort, Standard ist `dietpi`

***

Offizielle Dokumentation: <https://mariadb.org>
Erste-Schritte-Dokumentation: <https://mariadb.org/documentation/#getting-started>

### phpMyAdmin

![phpMyAdmin-Logo](../assets/images/dietpi-software-webstack-phpmyadmin.png){: width="160" height="120" loading="lazy"}

**phpMyAdmin** ist ein kostenloses Softwaretool, das in [PHP](#php) geschrieben ist und f&uuml;r die Verwaltung von MySQL / MariaDB &uuml;ber das Web vorgesehen ist.

H&auml;ufig verwendete Operationen (_wie: Verwaltung von Datenbanken, Tabellen, Spalten, Relationen, Indizes etc._) k&ouml;nnen &uuml;ber die Web-Benutzeroberfl&auml;che ausgef&uuml;hrt werden. Mit derselben Anwendung k&ouml;nnen Sie auch direkt beliebige SQL-Anweisungen ausf&uuml;hren.

=== "Schnellzugriff"

    - URL = `http://<Ihre.IP>/phpmyadmin`
    - Benutzername = `phpmyadmin`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort, Standard ist `dietpi`

***

Website: <https://www.phpmyadmin.net>
Offizielle Dokumentation: <https://www.phpmyadmin.net/docs/>

## SQLite

![SQLite-Logo](../assets/images/dietpi-software-webstack-sqlite.svg){: width="200" height="95" loading="lazy"}

Quelle: Teil der SQLite-Dokumentation, die vom Autor D. Richard Hipp als gemeinfrei freigegeben wurde. SVG-Konvertierung von Mike Toews. [&Ouml;ffentlicher Bereich](https://commons.wikimedia.org/w/index.php?curid=11675072)

**SQLite** ist eine eingebettete relationale Datenbank-Engine. Es ist eine eigenst&auml;ndige, hochzuverl&auml;ssige und voll funktionsf&auml;hige SQL-Datenbank-Engine. Es ist sehr beliebt und wird heute weltweit in Hunderten von Millionen Exemplaren verwendet[^2].

=== "Schnellstart"

    Um eine Datenbank zu erstellen und Befehle auszuf&uuml;hren, verwenden Sie die [Schnellstartdokumentation](https://www.sqlite.org/quickstart.html).

***

Website: <https://www.sqlite.org/index.html>
Offizielle Dokumentation: <https://www.sqlite.org/docs.html>

## Redis

Ein nicht SQL-basierter Datenspeicher.

![Redis-Logo](../assets/images/dietpi-software-webstack-redis.svg){: width="200" height="67" loading="lazy"}

Quelle: [Carlos Prioglio](https://redis.io/images/redis-logo.svg), [Lizenz](https://commons.wikimedia.org/w/index.php?curid=95020509).

**Redis** ist ein Open Source (BSD-lizenzierter) In-Memory-Datenstrukturspeicher, der als Datenbank, Cache und Nachrichtenbroker verwendet wird.

**Redis** geh&ouml;rt zur Familie der Datenbanken, die Schl&uuml;sselwertspeicher genannt werden. Das Wesentliche eines Schl&uuml;sselwertspeichers ist die F&auml;higkeit, einige Daten, die als Wert bezeichnet werden, in einem Schl&uuml;ssel zu speichern. Diese Daten k&ouml;nnen sp&auml;ter nur abgerufen werden, wenn wir den genauen Schl&uuml;ssel kennen, mit dem sie gespeichert wurden.

=== "Schnellstart"

    Das erste, was Sie tun m&uuml;ssen, um zu &uuml;berpr&uuml;fen, ob Redis ordnungsgem&auml;&szlig; funktioniert, ist das Senden eines PING-Befehls:

    ```sh
    redis-cli ping
    ```

    Weitere Befehle und eine Einf&uuml;hrung in Redis-Datentypen und -Befehle finden Sie in der [Schnellstartdokumentation] (https://redis.io/topics/data-types-intro).

***

Website: <https://redis.io/>
Offizielle Dokumentation: <https://redis.io/documentation>
Befehle: <https://redis.io/commands>

## InfluxDB

**InfluxDB** ist eine _Zeitreihen_-Datenbank und f&uuml;r hohe Schreib- und Abfragelasten optimiert. Zu diesem Zweck eignet es sich sehr gut, um Sensordaten oder Zeitreiheninformationen aus verschiedenen Protokollen zu speichern. InfluxDB ist nicht nur eine Zeitreihenplattform, sondern bietet auch eine Web-Benutzeroberfl&auml;che und Dashboard-Tools, Hintergrundverarbeitung und einen &Uuml;berwachungsagenten.

Die Hauptschnittstelle zur Datenbank f&uuml;r die Verwaltung und Daten&uuml;bertragung sind HTTP-Anforderungen, die direkt vom Dienst `influxdb` verarbeitet werden (der verwendete Standardport ist `8086`).

Die Daten k&ouml;nnen sch&ouml;n mit [**Grafana**](../hardware_projects/#grafana) betrachtet werden. Diese Installation und Dokumentation war m&ouml;glich dank [@marcobrianza](https://github.com/MichaIng/DietPi/issues/1784#issuecomment-390778313).

=== "Schnellstart"

    Nach der Installation erfolgen die Daten&uuml;bertragungen &uuml;ber die HTTP-Anfragen und werden direkt vom InfluxDB-Dienst abgewickelt, der auf `http://<your.IP>:8086` l&auml;uft.

    Erstellen Sie eine Datenbank mit "influxdb" &uuml;ber das Befehlszeilentool. Dieses Tool verwendet auch HTTP, sodass es eine Datenbank auf einem Remote-Computer verwalten kann, indem es die Option "-host" einstellt:

    ```sh
    influx -execute 'create database myfirstdb'
    ```

    Erstellen Sie eine Datenbank mit einer HTTP-Anforderung und dem Tool `curl`:

    ```sh
    curl -i -X POST http://<your.IP>:8086/query --data-urlencode 'q=CREATE DATABASE myfirstdb'
    ```

    Post-Daten:

    ```sh
    curl -i -X POST 'http://<your.IP>:8086/write?db=myfirstdb' --data-binary 'temperature value=20.12'
    ```

    Daten aus der Datenbank abrufen und anzeigen:

    ```sh
    influx -database myfirstdb -execute 'SELECT * FROM temperature'
    ```  

    Rufen Sie Daten mit einer HTTP-Anfrage und dem Tool `curl` ab:

    ```sh
    curl -i -XPOST http://<your.IP>:8086/query?db=mydb --data-urlencode "q=SELECT * FROM temperature"
    ```

=== "Benutzer und Sicherheit"

    **Erstellen Sie Benutzer und Berechtigungen** mit der Befehlszeile `influx`.

    Um die InfluxDB-Datenbankverwaltungsschnittstelle zu starten, geben Sie Folgendes ein:

    ```sh
    influx -username admin -password admin01
    ```

    Erstellen Sie dann die Datenbankeintr&auml;ge:

    ```sh
    CREATE USER admin WITH PASSWORD 'admin01' WITH ALL PRIVILEGES
    CREATE USER test_user WITH PASSWORD 'test_user01'
    GRANT ALL ON mydb TO test_user
    exit
    ```

=== "Gesicherten Zugriff aktivieren (HTTPS)"

    Standardm&auml;&szlig;ig ist die _HTTP_-Authentifizierung deaktiviert. Um es zu aktivieren, folgen Sie den n&auml;chsten zwei Schritten:

    1. N&auml;chste Einstellung in der Konfigurationsdatei `/etc/influxdb/influxdb.conf` &auml;ndern:

        ```
        auth-enabled = true
        ```

    2. Starten Sie den Dienst neu:

        ```sh
        systemctl restart influxdb
        ```

=== "Informationen installieren"

    Der Datenspeicherort f&uuml;r InfluxDB ist gespeichert bzw. mit symbolischen Links zum DietPi-Benutzerdatenverzeichnis verkn&uuml;pft: `/mnt/dietpi_userdata/influxdb`

***

Website: <https://www.influxdata.com/products/influxdb/>
Offizielle Dokumentation: <https://docs.influxdata.com/influxdb/v1.8/>
Erste Schritte: <https://docs.influxdata.com/influxdb/v1.8/introduction/get-started/>

##PostgreSQL

PostgreSQL ist ein persistenter, fortschrittlicher objektrelationaler Datenbankserver, der in &auml;hnlichen Szenarien wie MariaDB verwendet wird.

![PostgreSQL-Logo](../assets/images/dietpi-software-postgresql.png){: width="200" height="206" loading="lazy"}

=== "Implementierungsdetails"

    W&auml;hrend das Debian-Paket PostgreSQL mit einem aktiven TCP/IP-Listener ausliefert, allerdings nur auf localhost, ist dieser bei der Installation &uuml;ber die DietPi-Software standardm&auml;&szlig;ig deaktiviert. Wir empfehlen die Verwendung des UNIX-Domain-Sockets in `/run/postgresql`, um eine Verbindung zur Datenbank herzustellen, was Leistungsvorteile bietet. Wenn TCP/IP-Verbindungen erforderlich sind, empfiehlt es sich, eine &Uuml;berschreibungskonfiguration wie `/etc/postgresql/*/main/conf.d/99local.conf` zu erstellen und die Listening-Adresse festzulegen:

    ```
    listen_addresses = 'localhost'
    ```

    Ersetzen Sie `localhost` durch eine tats&auml;chliche IP-Adresse, um den Fernzugriff zu erm&ouml;glichen, oder durch `*`, um alle Zugriffe &uuml;ber alle LAN- und &ouml;ffentlichen IP-Adressen und Dom&auml;nennamen zu erm&ouml;glichen.

    Bei der Installation &uuml;ber die DietPi-Software werden die eigentlichen Datenbankdateien in `/mnt/dietpi_userdata/postgresql` gespeichert, sodass sie zusammen mit anderen DietPi-Benutzerdaten einfach auf ein externes Laufwerk verschoben werden k&ouml;nnen. Aus Gr&uuml;nden der Abw&auml;rtskompatibilit&auml;t wird ein Symlink unter `/var/lib/postgresql` erstellt.

=== "Konfiguration"

    - Config-Verzeichnis:
        `/etc/postgresql/*/main`
        wobei das Sternchen die PostgreSQL-Versionsnummer ist, zB `11` oder `13`
    - Hauptkonfigurationsdatei:
        `/etc/postgresql/*/main/postgresql.conf`
    - DietPi-Konfiguration &uuml;berschreiben:
        `/etc/postgresql/*/main/conf.d/00dietpi.conf`

    Um Einstellungen hinzuzuf&uuml;gen oder zu &auml;ndern, empfiehlt es sich, eine neue Override-Konfiguration zu erstellen, z. B.:

    ```
    /etc/postgresql/*/main/conf.d/99local.conf
    ```

    Damit die &Auml;nderungen wirksam werden, muss der Dienst neu geladen werden:

    ```sh
    systemctl reload postgresql
    ```

=== "Serviceabwicklung"

Der systemd-Dienst `postgresql.service` wird verwendet, um den PostgreSQL-Server zu starten und zu steuern. Folgende Befehle k&ouml;nnen verwendet werden:

    - Start: `systemctl start postgresql`
    - Stop: `systemctl stop postgresql`
    - Neustart: `systemctl restart postgresql`
    - Konfiguration neu laden: `systemctl reload postgresql`
    - Druckstatus: `systemctl start postgresql`

=== "Protokolle anzeigen"

    Serviceprotokolle werden im Systemjournal erstellt und k&ouml;nnen angezeigt werden &uuml;ber:

    ```sh
    journalctl -u postgresql
    ```

    Der Server selbst protokolliert standardm&auml;&szlig;ig in einer Datei:

    ```sh
    cat /var/log/postgresql/postgresql-*-main.log
    ```

=== "Auf neueste Version aktualisieren"

    Da PostgreSQL &uuml;ber APT installiert wird, kann es aktualisiert werden &uuml;ber:

    ```sh
    apt install postgresql
    ```

***

Offizielle Website: <https://www.postgresql.org/>
Offizielle Dokumentation: <https://www.postgresql.org/docs/>
Quellcode: <https://git.postgresql.org/gitweb/?p=postgresql.git>
Lizenz: [PostgreSQL-Lizenz](https://www.postgresql.org/about/licence/)

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

[^1]: [&Uuml;ber MariaDB Server und MariaDB Foundation](https://mariadb.org/about/)

[^2]: [&Uuml;ber SQLite](https://www.sqlite.com/about.html)
