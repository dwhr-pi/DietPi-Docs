# Sozial / Suche

## �berblick

- [**FreshRSS - Ein selbst gehosteter RSS-Feed-Aggregator**](#freshrss)
- [**phpBB - Kostenlose Flat-Forum-Bulletin-Board-Softwarel�sung**](#phpbb)
- [**Wordpress - Website-Blog und Ver�ffentlichungsplattform**](#wordpress)
- [**Single File PHP Gallery - Hosten und durchsuchen Sie Ihre Bilder �ber eine Weboberfl�che**](#single-file-php-gallery)
- [**Ba�kal - Lightweight CalDAV + CardDAV-Server**](#baikal)
- [**OpenBazaar - Dezentraler Peer-to-Peer-Marktserver mit Bitcoin**](#openbazaar)
- [**Synapse - Dezentrale Kommunikation mit dem Matrix-Protokoll**](#synapse)

??? ??? Information " "Wie f�hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef�hrten **DietPi-optimierten Softwareelemente** zu installieren, f�hren Sie es �ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W�hlen Sie **Software durchsuchen** und w�hlen Sie einen oder mehrere Artikel aus. W�hlen Sie abschlie�end �Installieren�.
    DietPi f�hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men�-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur�ck zur **Liste der optimierten Software**](../../software/)

## FreshRSS

FreshRSS ist ein selbst gehosteter RSS-Feed-Aggregator.

![FreshRSS-Screenshot](../assets/images/dietpi-software-social-freshrss.jpg){: width="400" height="247" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    - URL = `<http://<Ihre.IP>/freshrss`
    - Benutzername = `dietpi`
    - Passwort = `dietpi`

***

Offizielle Dokumentation: <https://freshrss.github.io/FreshRSS/en/users/02_First_steps.html>

## phpBB

Wenn Sie schon immer Ihr eigenes Forum haben wollten, ist phpBB alles, was Sie brauchen.

Installiert auch:

- Webserver

![Screenshot des phpBB-Beispielforums](../assets/images/dietpi-software-social-phpbb.png){: width="400" height="298" loading="lazy"}

### Zugriff auf Foren

URL = `http://<Ihre.IP>/phpbb`

### Ersteinrichtung einrichten

DietPi erstellt automatisch die SQL-Datenbank f�r phpBB. Bitte befolgen Sie die nachstehenden Schritte, um diese Details in phpBB einzugeben und die Einrichtung abzuschlie�en.

#### Zugriff auf die phpBB-Website

- URL = `http://<Ihre.IP>/phpbb`
- Klicken Sie auf die Registerkarte "Installieren".
- Klicken Sie auf �Weiter zum n�chsten Schritt�
- Klicken Sie auf "Installation starten"

#### MySQL/MariaDB-Datenbankdetails

So geben Sie die MySQL/MariaDB-Datenbankdetails ein:

- Datenbankserver-Hostname oder Datenquellenname (DSN) = `localhost`
- Datenbankbenutzername = `phpbb`
- Datenbankname = `phpbb`
- Datenbank-Passwort = `dietpi` (bzw. Ihr gew�hltes globales Software-Passwort)

- Klicken Sie auf �Weiter zum n�chsten Schritt�
- Klicken Sie auf �Weiter zum n�chsten Schritt�

#### Erstellen Sie Ihr Administratorkonto

Dieses Konto wird f�r den vollen Zugriff auf das phpBB-Forum verwendet.

- Klicken Sie auf �Weiter zum n�chsten Schritt�
- Klicken Sie auf �Weiter zum n�chsten Schritt�
- Klicken Sie auf �Weiter zum n�chsten Schritt�

#### E-Mail- und Server-URL-Einstellungen

Verwenden Sie die Standardwerte.

- Klicken Sie auf �Weiter zum n�chsten Schritt�
- Klicken Sie auf �Weiter zum n�chsten Schritt�

Die Datenbanktabellen werden nun generiert, bitte warten.

#### Anmeldung

Klicken Sie auf "Anmelden"
Mit Ihren zuvor erstellten Admin-Login-Daten k�nnen Sie nun Ihre Forenseiten verwalten und erstellen.

Da die Installation nun abgeschlossen ist, m�ssen Sie den Installationsordner entfernen, bevor das Forum live gehen kann. F�hren Sie den folgenden Befehl aus:

```sh
rm -R /var/www/phpbb/install
```

Ihr Forum ist nun bereit.

## WordPress

WordPress ist eine hochmoderne semantische Personal-Publishing-Plattform mit Fokus auf �sthetik, Webstandards und Benutzerfreundlichkeit.
Damit k�nnen Sie Ihre eigene Website erstellen.

![Wordpress-Logo und Nutzungspiktogramm](../assets/images/dietpi-software-social-wordpress.jpg){: width="400" height="242" loading="lazy"}

=== "Zugriff auf die Weboberfl�che"

    URL = `http://<your.IP>/wordpress`

=== "Erste Verbindung"

Geben Sie bei der ersten Verbindung die folgenden MySQL-Datenbankdetails ein:

    - Datenbankname = `wordpress`
    - Benutzername = `wordpress`
    - Passwort = Ihr globales Anwendungspasswort
    - Datenbankhost = `localhost`
    - Tabellenpr�fix = `wp_`

## Einzeldatei-PHP-Galerie

*Single File PHP Gallery* erm�glicht es Ihnen, Ihre Bilder von einer Weboberfl�che aus zu hosten und zu durchsuchen.

Installiert auch:

- LASP-Webserver

![Screenshot der Single File PHP Gallery-Weboberfl�che](../assets/images/dietpi-software-social-imagegallery.png){: width="400" height="248" loading="lazy"}

=== "Zugriff auf Bildergalerie"

    URL = `http://<your.IP>/gallery`

=== "Bilder hinzuf�gen"

So f�gen Sie Ihre eigenen Bilder hinzu:

    - Erstellen Sie Ihren Bildordner

        ```sh
        mkdir /var/www/gallery/MyImageFolder
        ```

    - Legen Sie eine Bilddatei in Ihren neuen Ordner

        ```sh
        wget https://dietpi.com/images/dietpi-logo_192x192.png
        mv dietpi-logo_192x192.png /var/www/gallery/MyImageFolder/
        ```

***

Website: <https://sye.dk/sfpg>

YouTube-Video-Tutorial: *DietPi: Einfaches Einrichten von Raspberry Pi-Projekten (z. B. eine gemeinsame Fotogalerie)*.

<iframe src="https://www.youtube-nocookie.com/embed/0by117lpq_o?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading="lazy" ></iframe>

## Baikal

Ba�kal ist ein leichtgewichtiger CalDAV + CardDAV-Server.

![Screenshot der Ba�kal-Weboberfl�che](../assets/images/dietpi-software-social-baikal.png){: width="400" height="219" loading="lazy"}

=== "Erste Ausf�hrung einrichten"

    Greifen Sie auf die Setup-Seite zu:

    - URL = `http://<your.IP>/baikal/html`
    - Geben Sie ein neues Admin-Passwort f�r Ihr Konto ein und klicken Sie dann auf die Schaltfl�che Weiter/Speichern.

    Geben Sie MySQL-Details ein:

    - MySQL verwenden = Ja
    - MySQL-Host = �127.0.0.1�.
    - Name der MySQL-Datenbank = `baikal`
    - MySQL-Benutzername = `baikal`
    - MySQL-Passwort = Ihr globales Software-Passwort (Standard: `dietpi`)

=== "Zugriff auf die Weboberfl�che"

    - URL = `http://<your.IP>/baikal/html/admin`
    - Benutzername = `admin`
    - Passwort = Das, was Sie w�hrend der ersten Ausf�hrung oben festgelegt haben.

## OpenBazaar

OpenBazaar ist ein kostenloser dezentraler Peer-to-Peer-Marktserver f�r alle. Keine Geb�hren. Verwendung von Bitcoins.
Oldschool: Denken Sie an Napster, aber f�r den Kauf und Verkauf von Sachen mit Ihren Bitcoins.

![Screenshot des OpenBazaar-Clients](../assets/images/dietpi-software-social-openbazaar.png){: width="400" height="240" loading="lazy"}

=== "OpenBazaar-Client"

    Der Client erm�glicht es Ihnen, innerhalb des Marktnetzwerks von OpenBazaar zu st�bern und zu handeln.
    <https://www.openbazaar.org/download/>

=== "OpenBazaar-Client mit Ihrem OpenBazaar-Server verbinden"

    Schritt 1:
    W�hrend der Installation werden Sie aufgefordert, einen Benutzernamen, ein Passwort und eine zul�ssige IP-Adresse einzugeben.

    Schritt 2:
    Als n�chstes m�ssen Sie den OpenBazaar-Client �ffnen und Ihren Server hinzuf�gen:

    - Klicken Sie auf Men� (oben rechts)
    - Klicken Sie auf Neuer Server
    - W�hlen Sie Eigenst�ndig
    - Geben Sie die IP-Adresse Ihres DietPi-Ger�ts sowie den Benutzernamen und das Passwort ein, die Sie in Schritt 1 vergeben haben.

## Synapse

Synapse ist ein in Python geschriebener Server f�r die Kommunikation �ber das Matrix-Protokoll.

=== "Kunde"

    F�r die Kommunikation mit Synapse k�nnen Sie [Element](https://element.io/) verwenden, aber jeder Client, der das Matrix-Protokoll unterst�tzt, sollte funktionieren.

=== "F�deration"

    Synapse ist standardm��ig als privater Server ohne Verbindung zu anderen Servern eingerichtet. ??? Information "rmationen zum Verbinden mit anderen Servern (Federate) finden Sie unter https://github.com/matrix-org/synapse/blob/develop/docs/federate.md. Beachten Sie, dass frp derzeit nicht mit Synapse funktioniert.

=== "Konfiguration"

    - Config-Verzeichnis:
     `/mnt/dietpi_userdata/synapse`
    - Hauptkonfigurationsdatei:
    `/mnt/dietpi_userdata/synapse/homeserver.yaml`
    - DietPi-Konfiguration �berschreiben:
    `/mnt/dietpi_userdata/synapse/homeserver.yaml.d/00-dietpi.yaml`
    Diese enth�lt auch die PostgreSQL-Datenbankdetails und diese Datei ist daher nur f�r Root oder den Benutzer "synapse" lesbar.

    Um Einstellungen hinzuzuf�gen oder zu �ndern, empfiehlt es sich, eine neue Override-Konfiguration zu erstellen, z. B.:

    ```
    /mnt/dietpi_userdata/synapse/homeserver.yaml.d/99-local.yaml
    ```

    Damit die �nderungen wirksam werden, muss der Dienst neu geladen werden:

    ```sh
    systemctl reload synapse
    ```

=== "Serviceabwicklung"

    Die DietPi-Synapse-Implementierung erstellt einen systemd-Dienst �synapse.service�, um den Synapse-Server zu starten und zu steuern. Folgende Befehle k�nnen verwendet werden:

    - Start: `systemctl start synapse`
    - Stop: `systemctl stop synapse`
    - Neustart: `systemctl restart synapse`
    - Konfiguration neu laden: `systemctl reload synapse`
    - Druckstatus: `systemctl start synapse`

=== "Protokolle anzeigen"

    Protokolle werden im Systemjournal erstellt und k�nnen angezeigt werden �ber:

    ```sh
    journalctl -u synapse
    ```

=== "Auf neueste Version aktualisieren"

    Da Synapse �ber Python 3 Pip installiert wird, k�nnen Sie es aktualisieren �ber:

    ```sh
    pip3 install -U matrix-synapse
    ```

***

Offizielle Website: <https://matrix.org/>
Offizielle Dokumentation: <https://matrix.org/docs/guides>
Quellcode: <https://github.com/matrix-org/synapse>
Lizenz: [Apache 2.0](https://github.com/matrix-org/synapse/blob/develop/LICENSE)

[Zur�ck zur **Liste der optimierten Software**](../../software/)
