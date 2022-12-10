# Systemsicherheit

## Überblick

- [**Let's Encrypt - HTTPS/SSL aktivieren**](#lets-encrypt)
- [**Fail2Ban - Schützt Ihr System vor Brute-Force-Angriffen**](#fail2ban)

??? Information "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschlie&szlig;end `Installieren`.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## Lassen Sie uns verschlüsseln

Let’s Encrypt ist ein Anbieter von kostenlosen SSL-Zertifikaten. Certbot ist der offizielle Client, um SSL-Zertifikate von Let’s Encrypt auf Ihren Webserver anzuwenden. Dies erm&ouml;glicht Ihnen den `https://` (verschlüsselt und authentifiziert) Zugriff auf Ihre Websites.

### Anforderungen

Um Certbot zu verwenden, ben&ouml;tigen Sie:

- Ein funktionierender Apache-, Nginx- oder Lighttpd-Webserver
- Eine URL/Domain (zB: `mysite.org`). No-IP kann für eine URL/Domain verwendet werden, die auf Ihr Gerät verweist.
- Die Ports 80 und 443 (TCP) müssen an Ihr Gerät weitergeleitet werden. Dies wird normalerweise in Ihrem Router eingestellt.

???+ wichtig "Port 80 für Certbot-Erneuerung offen halten"
    Selbst wenn Sie nur HTTPS auf Port 443 verwenden, erfordert Let's Encrypt, dass Port 80 für Zertifikatserneuerungen ge&ouml;ffnet bleibt (in der Weiterleitungsfunktion Ihres Routers).

![Screenshot der DietPi-LetsEncrypt-Oberfläche](../assets/images/dietpi-software-security-certbot.png){: width="400" height="183" loading="lazy"}

### Erstellen Sie Ihr Zertifikat und wenden Sie es an

Sobald Certbot von `dietpi-software` installiert wurde, führen Sie `dietpi-letsencrypt` aus, um Ihr SSL-Zertifikat zu konfigurieren, zu erstellen und anzuwenden:

```sh
dietpi-letsencrypt
```

Geben Sie einfach die erforderlichen Details und Einstellungen ein und wählen Sie dann `Anwenden`.
Let's Encrypt ist so einfach!

***

Webseite: <https://letsencrypt.org>

## Fail2Ban

Fail2Ban schützt Ihr System vor Brute-Force-Angriffen, indem es die Quell-IP-Adresse sperrt.
Wir haben die Erkennung für SSH-Server (OpenSSH und Dropbear) aktiviert, Fail2Ban unterstützt jedoch auch zusätzliche Software.

![Fail2Ban-Logo](../assets/images/dietpi-software-security-fail2ban1.jpg){: width="200" height="157" loading="lazy"}

![Fail2Ban-Beispielkonsolenprotokollausgabe](../assets/images/dietpi-software-security-fail2ban2.jpg){: width="550" height="360" loading="lazy"}

Quelle: [`Lostcontrol` des Fail2ban-Wikis](https://fail2ban.org/wiki/index.php/File:Fail2ban-screenshot.jpg), [GPL](https://commons.wikimedia.org/w/ index.php?curid=19776087)

Eine IP-Adresse wird standardmä&szlig;ig nach 3 fehlgeschlagenen SSH-Anmeldeversuchen gesperrt. Fail2Ban wird die Quell-IP-Adresse für 10 Minuten sperren.

=== "Status der Blockierungsaktivität prüfen"

    Der Status kann mit diesen Befehlen überprüft werden:

    ```sh
    fail2ban-client status sshd
    fail2ban-client status dropbear
    ```

=== "Unterstützung für zusätzliche Programme aktivieren"

    Fail2Ban unterstützt Brute-Force-Schutz für andere Software (z. B. Apache, ProFTPD usw.).
    Sie k&ouml;nnen diese Funktionen aktivieren/deaktivieren, indem Sie die Datei */etc/fail2ban/jail.conf* ändern und `enable = true` unter dem Namen *[software]* setzen.

***

Website: <https://fail2ban.org/wiki/index.php/Main_Page>

[Zurück zur **Liste der optimierten Software**](../../software/)
