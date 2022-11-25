# SSH-Serverauswahl

## Überblick

- [**Dropbear - Leichtgewichtiger SSH-Server**](#dropbear)
- [**OpenSSH - SSH-Server mit vielen Funktionen und SFTP/SCP-Unterstützung**](#openssh)

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

## Fallbär

Dropbear ist ein leichtgewichtiger SSH-Server, der standardmäßig auf DietPi-Systemen installiert ist.
Hinweis: Sie können Ihren SSH-Server jederzeit mit der *DietPi-Software* austauschen oder wechseln.

![Dropbear-Logo](../assets/images/dietpi-software-sshserver-dropbear.jpg){: width="150" height="121" loading="lazy"}

=== "Zugriff auf die Weboberfläche"

    Der SSH-Server kann direkt von Unix mit dem `ssh`-Kommandozeilenprogramm oder anderen SSH-Client-Programmen verbunden werden:

    - Adresse = Ihre IP-Adresse (zB: *192.168.0.100*)
    - Port = *22*
    - Benutzername = `root`
    - Passwort = `dietpi`

=== "Windows-SSH-Client"

Unter Windows werden [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) und [KiTTY](https://www.9bis.net/kitty/) empfohlen SSH-Clients.

***

Website: <https://matt.ucc.asn.au/dropbear/dropbear.html>
Wikipedia: <https://wikipedia.org/wiki/Dropbear_(Software)>

## OpenSSH

OpenSSH bietet einen funktionsreichen SSH-Server mit SFTP/SCP-Unterstützung.
Hinweis: Sie können Ihren SSH-Server jederzeit mit der *DietPi-Software* austauschen oder wechseln.

![OpenSSH-Logo](../assets/images/dietpi-software-sshserver-openssh.gif){: width="300" height="99" loading="lazy"}

=== "Zugriff auf den SSH-Server"

    Der SSH-Server kann direkt von Unix mit dem `ssh`-Kommandozeilenprogramm oder anderen SSH-Client-Programmen verbunden werden:

    - Adresse = Ihre IP-Adresse (zB: *192.168.0.100*)
    - Benutzername = `root`
    - Passwort = `dietpi`
    - Port = *22*

=== "Windows-SSH-Client"

    Unter Windows werden [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) und [KiTTY](https://www.9bis.net/kitty/) empfohlen SSH-Clients.

=== "Windows SFTP/SCP-Client"

    Mit WinSCP können Sie Dateien und Ordner auf Ihr DietPi-Gerät übertragen ([WinSCP-Downloadseite](https://winscp.net/eng/download.php)).

***

Website: <https://www.openssh.com>
Wikipedia: <https://wikipedia.org/wiki/OpenSSH>

[Zurück zur **Liste der optimierten Software**](../../software/)
