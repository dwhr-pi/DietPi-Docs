# Web Entwicklung

## Überblick

[**Stacks für die Webentwicklung**](#stacks-for-web-development)

- [**LAMP** Webstack - **Apache / MariaDB / PHP**](#lamp-web-stack)
- [**LASP** Webstack - **Apache / SQLite / PHP**](#lasp-web-stack)
- [**LEMP** Webstack - **Nginx / MariaDB / PHP**](#lemp-web-stack)
- [**LESP** Webstack - **Nginx / SQLite / PHP**](#lesp-web-stack)
- [**LLMP** Webstack - **Lighttpd / MariaDB / PHP**](#llmp-web-stack)
- [**LLSP** Webstack - **Lighttpd / SQLite / PHP**](#llsp-web-stack)

[**Webserver**](#webservers)

- [**Apache** - Webserver mit vielen Funktionen](#apache)
- [**Nginx** - Hochleistungs-Webserver, Load-Balancer und Reverse-Proxy](#nginx)
- [**Lighttpd** - Extrem leichter Webserver](#lighttpd)
- [**Tomcat** - Apache Tomcat-Server](#Tomcat)

[**Webentwicklung - Programmierung & Frameworks**](#web-development-programming-frameworks)

- [**Flask** - Micro-Web-Framework powered by Python](#flask)
- [**PHP** - Skriptsprache, die für die Webentwicklung geeignet ist](#php)
- [**Node.js** - JavaScript-Laufzeitumgebung zum Erstellen skalierbarer Netzwerkanwendungen](#nodejs)

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschließend „Installieren“.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## Stacks für die Webentwicklung

DietPi bietet eine **Ein-Klick-Installation** der folgenden Webentwicklungs-Stacks:

- [**LAMP** Webstack - **Apache / MariaDB / PHP**](#lamp-web-stack)
- [**LASP** Webstack - **Apache / SQLite / PHP**](#lasp-web-stack)
- [**LEMP** Webstack - **Nginx / MariaDB / PHP**](#lemp-web-stack)
- [**LESP** Webstack - **Nginx / SQLite / PHP**](#lesp-web-stack)
- [**LLMP** Webstack - **Lighttpd / MariaDB / PHP**](#llmp-web-stack)
- [**LLSP** Webstack - **Lighttpd / SQLite / PHP**](#llsp-web-stack)

!!! Hinweis "Bedeutung der Akronyme *LAMP*, *LASP*, *LEMP*, *LESP*, *LLMP*, *LLSP*"

    - Betriebssystem: **L** für Linux / DietPi
    - Webserver: **A** für Apache, **E** für [Nginx](#nginx), **L** für [Lighttpd](#lighttpd)
    - Datenbank: **M** für MariaDB, **S** für [SQLite](../databases/#sqlite)
    - Skriptsprache: **P** für [PHP](#php)

!!! Hinweis ""
    Alle Stacks werden mit **PHP-Caches** (APCu und OPcache) geliefert, die basierend auf einem Anteil des Gesamtspeichers optimiert werden.

### Welcher Web Application Stack ist der beste für Sie?

=== "Welchen WEBSERVER WÄHLEN?"

    **[Apache](#apache)**

    - Speichernutzung = **Hoch** | Multithreading = **Ja**

    Es ist funktionsreich und beliebt. Es wird Anfängern und Benutzern empfohlen, die Apache-basierten Anleitungen folgen möchten.

    **[Nginx](#nginx)**

    - Speichernutzung = **M    ittel** | Multithreading = **Ja**

    Es ist eine leichtgewichtige Alternative zu [Apache](#apache) und behauptet[^4] eine schnellere Webserverleistung im Vergleich zu [Apache](#apache). Es ist ideal für Situationen mit mittlerem bis hohem Datenverkehr, in denen [Lighttpd](#lighttpd) darunter leidet.

    **[Lighttpd](#lighttpd)**

    - Speichernutzung = **Niedrig** | Multithreaded = **Optional** - Einige Nachteile

    Es ist extrem leicht und wird allgemein als die "beste" Webserver-Leistung unter Linux für SBCs (Single Board Computers) angesehen. Es wird für Benutzer empfohlen, die einen geringen Webserver-Traffic und/oder persönlichen Gebrauch erwarten.

    Obwohl die DietPi-Installation von Lighttpd auf Single-Threading eingestellt ist, lassen Sie sich davon nicht abschrecken, in Szenarien mit geringer Nutzung (<10 Benutzer) wird es immer noch [Nginx](#nginx) und [Apache](#apache) übertreffen. Die Aktivierung von Multithreading ist in der Paketbeschreibung [Lighttpd](#lighttpd) beschrieben.

    !!! Hinweis "DietPi - Webserver Präferenz"

        Auf dem DietPi-Webserver-Einstellungsbildschirm können Sie Ihren bevorzugten Webserver für die Verwendung in DietPi-Installationen auswählen. Überprüfen Sie mehr die **Web-Einstellungen** in der [Erweiterten Konfiguration](../../dietpi_tools/#quick-selections).

    !!! Information ""

        Für weitere Details siehe [Der Kampf der Webserver Apache vs. Nginx vs. Lighttpd 2](https://detechter.com/the-battle-of-the-web-servers-apache-vs-Nginx-vs-lighttpd -2/).

=== "Welche DATENBANK WÄHLEN?"

    **[MariaDB](../databases/#mariadb)**
    Es ist ein Open-Source-RDBMS (Relational Database Management System). Es ist anwendungskompatibel zu MySQL, dh es kann als *drop-in*-Ersatz für MySQL verwendet werden. Es hat mehr Funktionen, weniger Fehler und eine bessere Leistung im Vergleich zu MySQL.

    **[SQLite](../databases/#sqlite)**
    Es ist ein RDBMS, das auch zu MySQL kompatibel ist. Es bietet eine breitere Sprachunterstützung (dh mehr Bindungen an Programmiersprachen) im Vergleich zu [MariaDB](../databases/#mariadb). [SQLite](../databases/#sqlite) hat einen sehr geringen Platzbedarf. Als Nachteile hat es keine Mehrbenutzerfähigkeiten und einige SQL-Funktionen fehlen.

***

### Wie installiert man ?

DietPi enthält die Option, den Webstack Ihres Favoriten auszuwählen. Grundsätzlich wählt man den Webstack bzw. Webserver haben Sie zwei Möglichkeiten innerhalb von `dietpi-software`:

    - Auswahl über ***Softwareoptimiert*** bzw
    - Auswahl über ***Webserver-Präferenz***

Letzteres wird nur bei der ersten Hintergrundinstallation des Webservers verwendet.

=== "Auswahl über Software optimiert"

    ![DietPi-Software Menü Softwareliste](../assets/images/dietpi-software-webstack-selection.png){: width="680" height="162" loading="lazy"}

    Mit dieser Option wählen Sie den kompletten Webstack zur Installation aus. Wählen Sie einfach den Webstack aus, den Sie installieren möchten, und führen Sie die Installation über die *Install*-Ausführung innerhalb von `dietpi-software` durch.

    !!! Hinweis ""
        Sofern Sie nicht _speziell_ einen Webstack benötigen, wird empfohlen, dass Sie DietPi erlauben, den Standard-Webstack automatisch zu installieren. Dies gewährleistet die Kompatibilität und Stabilität Ihres Systems.

=== "Auswahl über Webserver-Präferenz"

    ![DietPi-Software-Webserver-Einstellungsmenü](../assets/images/dietpi-software-webserver-preference.png){: width="500" height="309" loading="lazy"}

    Mit dieser Option wählen Sie nur den Webserver für die Verwendung in DietPi-Installationen aus.
    Wenn Sie eine Software zur Installation auswählen, die einen Webserver erfordert (z. B. Pi-hole, Nextcloud, Webmin, installiert über *Software Optimized*), installiert, konfiguriert und optimiert DietPi automatisch die von Ihnen gewählte Webserver-Präferenz. DietPi installiert auch [MariaDB](../databases/#mariadb) / [SQLite](../databases/#sqlite) nach Bedarf, abhängig von Ihrer Softwareauswahl. Grundsätzlich müssen Sie nie wieder einen Webserver-Stack manuell auswählen/installieren. DietPi erledigt das alles für Sie.

    ???+ info "Kein Webserverwechsel falls bereits installiert"
        Diese Einstellung „Webserver Preference*“ kann NICHT geändert werden, wenn ein vorhandener Webserver auf dem System installiert ist.

***

YouTube-Video-Tutorial: *DietPi-Webserver-Tutorial | Hosten Sie eine Website von Home | Himbeer-Pi*.

<iframe src="https://www.youtube-nocookie.com/embed/nB-i959ZGzQ?rel=0" frameborder="0" allow="fullscreen" width="560" height="315" loading=" faul"></iframe>

***

### LAMP-Webstack

LAMP-Stack ist eine beliebte Open-Source-Webplattform, die häufig zum Ausführen dynamischer Websites und Server verwendet wird. Es wird von vielen als Plattform der Wahl für die Entwicklung und Bereitstellung von Hochleistungs-Webanwendungen angesehen, die eine solide und zuverlässige Grundlage erfordern.

![LAMP-Stack-Komponentenlogos](../assets/images/dietpi-software-webstack-lamp.jpg){: width="702" height="369" loading="lazy"}

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`
    - Lokales Verzeichnis = `/var/www`

    **Zugriff auf die PHP-Infoseite:**

    - URL = `http://<Ihre.IP>/phpinfo.php`

    **Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

    Überprüfen Sie für die Datenbank die Details von **[MariaDB](../databases/#mariadb)**.

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    ??? note "Alternativer Weg: Manuelles Aktivieren von HTTP/SSL durch Installieren eines selbstsignierten SSL-Zertifikats"

        !!! warning "Nur empfohlen, falls **Let's encrypt** keine praktikable Option ist."

        **Schritt 1. Schlüssel erstellen**

        ```sh
        mkdir -p /etc/apache2/ssl
        openssl req -x509 -nodes -days 1000 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
        ```

        **Schritt 2. SSL-Konfiguration aktivieren und Apache neu starten**

        ```sh
        chmod 600 /etc/apache2/ssl/*
        cat << '_EOF_' > /etc/apache2/sites-enabled/default-ssl.conf
        <IfModule mod_ssl.c>
            <VirtualHost _default_:443>
                    ServerAdmin webmaster@localhost
                    ServerName example.com:443
                    DocumentRoot /var/www

                    LogLevel error
                    ErrorLog ${APACHE_LOG_DIR}/error.log
                    #CustomLog ${APACHE_LOG_DIR}/access.log combined

                    SSLEngine on

                    SSLCertificateFile /etc/apache2/ssl/apache.crt
                    SSLCertificateKeyFile /etc/apache2/ssl/apache.key

                    <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                    SSLOptions +StdEnvVars
                    </FilesMatch>
                    <Directory /usr/lib/cgi-bin>
                                    SSLOptions +StdEnvVars
                    </Directory>
                </VirtualHost>
            </IfModule>
        _EOF_
        a2ensite ssl
        systemctl restart apache2
        ```

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

***

### LASP-Webstack

LASP ist eine Variation des beliebten Open-Source-[LAMP-Webstacks](#lamp-web-stack), der [SQLite](../databases/#sqlite) anstelle von [MariaDB](../databases/#mariadb) bereitstellt. .

[SQLite](../databases/#sqlite) ist eine eingebettete relationale Datenbank-Engine. Es ist beliebt und könnte zusammen mit [Apache](#apache) und PHP ein guter Kandidat für Einplatinencomputer sein.

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`
    - Lokales Verzeichnis = `/var/www`

    **Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    ??? note "Alternativer Weg: Manuelles Aktivieren von HTTP/SSL durch Installieren eines selbstsignierten SSL-Zertifikats"

        !!! warning "Nur empfohlen, falls **Let's encrypt** keine praktikable Option ist."

        **Schritt 1. Schlüssel erstellen**

        ```sh
        mkdir -p /etc/apache2/ssl
        openssl req -x509 -nodes -days 1000 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
        ```

    **Schritt 2. SSL-Konfiguration aktivieren und Apache neu starten**

        ```sh
        chmod 600 /etc/apache2/ssl/*
        cat << '_EOF_' > /etc/apache2/sites-enabled/default-ssl.conf
        <IfModule mod_ssl.c>
            <VirtualHost _default_:443>
                    ServerAdmin webmaster@localhost
                    ServerName example.com:443
                    DocumentRoot /var/www

                    LogLevel error
                    ErrorLog ${APACHE_LOG_DIR}/error.log
                    #CustomLog ${APACHE_LOG_DIR}/access.log combined

                    SSLEngine on

                    SSLCertificateFile /etc/apache2/ssl/apache.crt
                    SSLCertificateKeyFile /etc/apache2/ssl/apache.key

                    <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                    SSLOptions +StdEnvVars
                    </FilesMatch>
                    <Directory /usr/lib/cgi-bin>
                                    SSLOptions +StdEnvVars
                    </Directory>
                </VirtualHost>
            </IfModule>
        _EOF_
        a2ensite ssl
        systemctl restart apache2
        ```

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

***

### LEMP-Webstack

LEMP ist eine Variation des beliebten Open-Source-[LAMP-Webstacks](#lamp-web-stack), der [Nginx](#nginx) anstelle des [Apache](#apache)-Webservers bereitstellt.

**Nginx** ist eine beliebte Wahl, dank seiner leichten Nutzung von Ressourcen und seiner Flexibilität, selbst mit minimaler Ausrüstung einfach zu skalieren.

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`

    **Zugriff auf die PHP-Infoseite:**

    - URL = `http://<Ihre.IP>/phpinfo.php`

    **Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

    Überprüfen Sie für die Datenbank die Details von **[MariaDB](../databases/#mariadb)**.

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    ??? note "Alternativer Weg: Manuelles Aktivieren von HTTP/SSL durch Installieren eines selbstsignierten SSL-Zertifikats"

        !!! warning "Nur empfohlen, falls **Let's encrypt** keine praktikable Option ist."

        **Schritt 1. Schlüssel erstellen**

        ```sh
        mkdir -p /etc/apache2/ssl
        openssl req -x509 -nodes -days 1000 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
        ```

        **Schritt 2. SSL-Konfiguration aktivieren und Apache neu starten**

        ```sh
        chmod 600 /etc/apache2/ssl/*
        cat << '_EOF_' > /etc/apache2/sites-enabled/default-ssl.conf
        <IfModule mod_ssl.c>
            <VirtualHost _default_:443>
                    ServerAdmin webmaster@localhost
                    ServerName example.com:443
                    DocumentRoot /var/www

                    LogLevel error
                    ErrorLog ${APACHE_LOG_DIR}/error.log
                    #CustomLog ${APACHE_LOG_DIR}/access.log combined

                    SSLEngine on

                    SSLCertificateFile /etc/apache2/ssl/apache.crt
                    SSLCertificateKeyFile /etc/apache2/ssl/apache.key

                    <FilesMatch "\.(cgi|shtml|phtml|php)$">
                                    SSLOptions +StdEnvVars
                    </FilesMatch>
                    <Directory /usr/lib/cgi-bin>
                                    SSLOptions +StdEnvVars
                    </Directory>
                </VirtualHost>
            </IfModule>
        _EOF_
        a2ensite ssl
        systemctl restart apache2
        ```

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

***

### LESP-Webstack

LESP ist eine Variation des beliebten Open-Source-[LAMP-Webstacks](#lamp-web-stack), der [Nginx](#nginx) anstelle des [Apache](#apache)-Webservers und [SQLite](.. /databases/#sqlite) anstelle von MariaDB.

**[Nginx](#nginx)** ist eine beliebte Wahl, dank seiner geringen Ressourcennutzung und seiner Flexibilität, selbst mit minimaler Ausrüstung einfach zu skalieren.

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`

    **Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

***

### LLMP-Webstack

LLMP ist eine Variation des beliebten Open-Source-[LAMP-Webstacks](#lamp-web-stack), der [Lighttpd](#lighttpd) anstelle des [Apache](#apache)-Webservers bereitstellt.

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`
    - Lokales Verzeichnis = `/var/www`

    **Zugriff auf die PHP-Infoseite:**

    - URL = `http://<Ihre.IP>/phpinfo.php`

    **Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

    Überprüfen Sie für die Datenbank die Details von **[MariaDB](../databases/#mariadb)**.

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

***

### LLSP-Webstack

LLSP ist eine Variante des beliebten Open-Source-[LAMP-Webstacks](#lamp-web-stack), der **[Lighttpd](#lighttpd)** anstelle von [Apache](#apache)-Webserver und **[ SQLite](../databases/#sqlite)** statt [MariaDB](../databases/#mariadb).

=== "Schnellstart"

    **Website aufrufen:**

    - URL = `http://<your.IP>` oder `http://<your.host.name>`
    - Lokales Verzeichnis = `/var/www`

**Zugriff auf die PHP-Infoseite:**

    - URL = `http://<Ihre.IP>/phpinfo.php`

**Informationen zum Speichercache abrufen:**

    - APCu = `http://<Ihre.IP>/apc.php`
    - OPcache = `http://<your.IP>/opcache.php`

    Überprüfen Sie für die Datenbank die Details von **[MariaDB](../databases/#mariadb)**.

=== "Gesicherter Zugriff - HTTPS/SSL"

    **Let's Encrypt** wird dringend empfohlen - [sehen Sie hier, wie es installiert wird](../../dietpi_tools/#dietpi-letsencrypt). Dadurch wird die Erstellung und Einrichtung Ihres kostenlosen SSL-Zertifikats automatisiert.

    Webseite aufrufen:

    - URL = `https://<your.IP>` oder `https://<your.host.name>`

=== "Einzelinstallation"

    Der Web Development Stack kann auch einzeln installiert werden. Diese Option bietet mehr Flexibilität und bietet die Möglichkeit zur Auswahl:

    - **Webserver**

    Abhängig von Ihren Anforderungen können Sie den Webserver auswählen, der Ihren Anforderungen am besten entspricht. Falls **[Lighttpd](#lighttpd)** nicht die richtige Wahl ist, können Sie mit **Apache Web Server**, **[Nginx](#nginx)** oder **Tomcat Webserver** fortfahren.

    - Datenbank

    Sie können **[MariaDB](../databases/#mariadb)** oder andere verfügbare Datenbanken wie **[InfluxDB](../databases/#influxdb)**, **[Redis](. ./databases/#redis)**, **[SQLite](../databases/#sqlite)**.

## Webserver

###Apache

Apache ist Open Source und der am häufigsten verwendete Webserver auf Linux-Systemen.

![Apache2-Logo](../assets/images/dietpi-software-webstack-apache2.jpg){: width="200" height="109" loading="lazy"}

Webserver werden zum Bereitstellen von Webseiten verwendet, die von Clientcomputern angefordert werden. Clients fordern und zeigen Webseiten normalerweise mit Webbrowser-Anwendungen wie Firefox, Opera, Chromium, Microsoft Edge, Internet Explorer usw. an.

Apache ist ein Projekt der Apache Software Foundation. Das Ziel ist die Bereitstellung eines sicheren, effizienten und erweiterbaren Servers, der HTTP-Dienste synchron mit den aktuellen HTTP-Standards bereitstellt.

=== "Protokollierung"

    Die Protokollierung erfolgt standardmäßig im Journal, und Sie können die Details anzeigen, indem Sie den nächsten Befehl ausführen:

    ```sh
    journalctl -u apache2
    ```

=== "Servername"

    Die Direktive „ServerName“ wird mit der lokalen IP aktualisiert. Dies hilft, die zugehörigen Startwarnungen stummzuschalten.
    
    **Anmerkungen:**
    
    - Dies kann zu Zugriffs- und CORS-Fehlern [^6] führen, wenn Anwendungen nach dem Servernamen suchen. In einem solchen Fall bieten Anwendungen im Allgemeinen eine Möglichkeit, eine Liste zulässiger Hostnamen zu definieren.
    
    - Ohne einen festgelegten Servernamen wendet der Webserver normalerweise einfach den HTTP_HOST-Header an, wodurch jede zugehörige Prüfung umgangen wird. Apache scheint dann laut der protokollierten Warnung 127.0.1.1 zu verwenden.

***

Offizielle Dokumentation: <https://httpd.apache.org/docs>

### Nginx

**Nginx** [Engine x] ist ein HTTP- und Reverse-Proxy-Server, ein Mail-Proxy-Server und ein generischer TCP/UDP-Proxy-Server. Es wurde 2004 veröffentlicht, um das Problem des erhöhten Webverkehrs anzugehen. Es hat sich einen ausgezeichneten Ruf erworben und wird auf den Top-Millionen verkehrsreichsten Websites verwendet – einige der Erfolgsgeschichten sind: Dropbox, Netflix, Wordpress.com, FastMail.FM.[^1]

![Nginx-Logo](../assets/images/dietpi-software-webstack-nginx.gif){: width="200" height="85" loading="lazy"}

Die Innovation von Nginx gegenüber früheren Servern wie Apache bestand darin, eine asynchrone, ereignisgesteuerte Architektur zu verwenden. Nginx ist blitzschnell und äußerst effizient in Bezug auf die Hardwareauslastung, sodass Server mehr Geschwindigkeit aus ihrer begrenzten CPU und ihrem begrenzten RAM herausholen können. Infolgedessen ist es eine der schnellsten Webserveroptionen zum Bereitstellen statischer Inhalte.

***

Offizielle Dokumentation: <https://www.nginx.com>

### Lighttpd

**Lighttpd** ist ein Webserver für die Betriebssysteme UNIX/Linux und Windows. Es ist eine Alternative zum Apache-Webserver. Es wird auch Lighty genannt.

![Lighttpd-Logo](../assets/images/dietpi-software-webstack-lighttpd.svg){: width="200" height="163" loading="lazy"}

Quelle: Fair use, <https://en.wikipedia.org/w/index.php?curid=10881730>.

Es wurde entwickelt, um sicher, schnell, standardkonform und flexibel zu sein und gleichzeitig für geschwindigkeitskritische Umgebungen optimiert zu sein. Sein geringer Speicherbedarf im Vergleich zu anderen Webservern, die geringe CPU-Last und seine Geschwindigkeitsziele machen Lighttpd zu einem perfekten Kandidaten für SBCs.

=== "Schnellzugriff"

    Überprüfen Sie nach der Installation, ob der Lighttpd-Dienst auf „http://<your.IP>“ ausgeführt wird.

=== "Auf mehrere CPUs skalieren"

    Multithreading wird von Lighttpd unterstützt und kann in der Konfigurationsdatei `/etc/lighttpd/lighttpd.conf` aktiviert werden. Ändern Sie den Wert von "4" in Ihre Gesamtkernzahl:

    ```
    server.max-worker = 4
    ```

    Starten Sie dann die Dienste neu:

    ```sh
    systemctl restart lighttpd
    ```

***

Offizielle Dokumentation: <https://www.lightpd.net>

### Tomcat

Was ist **Apache Tomcat**? Im Wesentlichen handelt es sich um ein Open-Source-Java-Servlet und einen Java Server Page-Container, mit dem Entwickler eine Reihe von Java-Unternehmensanwendungen implementieren können. Tomcat führt auch eine HTTP-Webserverumgebung aus, in der Java-Code ausgeführt werden kann.

![Tomcat-Logo](../assets/images/dietpi-software-webstack-tomcat.svg){: width="200" height="133" loading="lazy"}

Quelle: [The Apache Software Foundation](https://svn.apache.org/viewvc/jakarta/site/xdocs/images/logos/tomcat.eps), [Apache License 2.0](https://commons.wikimedia. org/w/index.php?curid=11302180).

=== "Installieren"

    Beginnend mit DietPi 7.3 wurde „Tomcat 8“ aus der DietPi-Softwareliste entfernt. Der Grund ist, dass `Tomcat 8` nur bis Debian Stretch verfügbar ist. Ab Debian Buster und neueren Versionen wird nur noch Tomcat 9 unterstützt.
    
    Um Tomcat 9 zu installieren, führen Sie den nächsten Befehl in der Konsole aus:

    ```sh
    apt install tomcat9
    ```

=== "Schnellzugriff"

    Das Webinterface ist über Port **8080** erreichbar:

    - URL = `http://<Ihre.IP>:8080`

***

Offizielle Dokumentation: <https://tomcat.apache.org>

## Webentwicklung - Programmierung & Frameworks

###PHP

![PHP-Logo](../assets/images/dietpi-software-webstack-php.svg){: width="200" height="108" loading="lazy"}

Quelle: [Colin Viebrock](https://www.php.net/download-logos.php), [CC BY-SA 4.0](https://commons.wikimedia.org/w/index.php?curid= 9632398).

PHP wurde erstmals von Rasmus Lerdorf eingeführt und ist eine allgemeine serverseitige Open-Source-Skriptsprache, die sich inzwischen zu einem De-facto-Codierungsstandard in der Webentwicklungsbranche entwickelt hat.

=== "Schnellstart"

    - Es gibt viele Tutorials - hier ist die offizielle [_Erste Schritte_](https://www.php.net/manual/en/getting-started.php) aus der PHP-Dokumentation.

***

Website: <https://www.php.net>
Offizielle Dokumentation: <https://www.php.net/manual/en/index.php>

### Flasche

Flask ist ein leichtgewichtiges Framework für Webanwendungen. Es wurde entwickelt, um den Einstieg schnell und einfach zu machen, mit der Fähigkeit, auf komplexe Anwendungen zu skalieren, und es hat sich zu einem der beliebtesten Frameworks für Python-Webanwendungen entwickelt.

=== "Schnellstart"

    Um **Flask** verwenden zu können, muss zuerst der Python Package Manager installiert werden - [siehe Python 3](../programming/#python-3). Führen Sie dann den nächsten Befehl aus.

    ```sh
    pip3 install -U Flask
    ```

***

Website: <https://palletsprojects.com/p/flask>
Offizielle Dokumentation: <https://flask.palletsprojects.com/en/1.1.x>
PyPI-Paketseite: <https://pypi.org/project/Flask>

### Node.js {: #nodejs }

Node.js ist eine JavaScript-Laufzeitumgebung, die auf der V8-JavaScript-Engine von Chrome basiert.

![Node.js](../assets/images/dietpi-software-nodejs.jpg)

Quelle: Von [nodejs.org](https://nodejs.org), [Markenrichtlinie](https://nodejs.org/en/about/trademark/)

Durch die Verwendung des Event-Callback/Non-Blocking-Ansatzes bietet Node.js ein Single-Threaded-Event-IO-Modell, das die Orchestrierung parallel laufender Aufgaben ermöglicht. Es unterstützt mehrere Verbindungen, ohne dass ein großer Speicherbedarf erforderlich ist. Amazon, Netflix, eBay, Reddit, LinkedIn, Tumblr und PayPal verwenden Node.js.[^5]

=== "Node.js-Version"

    Beginnend mit Version 7.2 fügte DietPi Unterstützung für [Node.js inoffizielle Builds von inofficial-builds.nodejs.org](https://unofficial-builds.nodejs.org/download/release/) hinzu. Auf diese Weise können Sie die Vorteile der Verwendung der neuesten Node.js-Version nutzen.
    
    _Warum das?_ Wir glauben, dass es wichtig und sicherer ist, die neueste Version zu verwenden. Zum Zeitpunkt des Schreibens der Dokumentation hat der neueste offizielle ARMv6-Build für Node.js die Version 11 und der neueste _inoffizielle Build_, der von Node.js herausgegeben wurde, ist v15.14.

***

Website: <https://nodejs.org/>
Offizielle Dokumentation: <https://nodejs.org/api/>

[^1]:
    Erfahren Sie mehr über die Erfolgsgeschichten von Nginx unter: <https://nginx.org/en/>
[^2]:
    [„Dead Database Walking: MySQLs Schöpfer darüber, warum die Zukunft MariaDB gehört – MariaDB, Open Source, mysql, Oracle“](https://www2.computerworld.com.au/article/457551/dead_database_walking_mysql_creator_why_future_belongs_mariadb/). Computerwelt. Abgerufen am 22. November 2020.
[^3]:
    [Am weitesten verbreitete und verwendete Datenbank-Engine] (https://www.sqlite.org/mostdeployed.html). Abgerufen am 12. Dezember 2020
[^4]:
    [NGINX vs. Apache: Unsere Sicht auf eine jahrzehntealte Frage](https://www.nginx.com/blog/nginx-vs-apache-our-view/). Abgerufen am 12. Dezember 2020

[^5]: <https://hostingtribunal.com/blog/node-js-stats/#gref>. Abgerufen am 29. Mai 2021

[^6]: [CORS-Fehler Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors). Abgerufen am 05. Dezember 2021

[Zurück zur **Liste der optimierten Software**](../../software/)
