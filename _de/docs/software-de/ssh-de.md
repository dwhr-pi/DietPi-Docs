# SSH-Serverauswahl

## &Uuml;berblick

- [**Dropbear - Leichtgewichtiger SSH-Server**](#dropbear)
- [**OpenSSH - SSH-Server mit vielen Funktionen und SFTP/SCP-Unterst&uuml;tzung**](#openssh)

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

## Fallb&auml;r

Dropbear ist ein leichtgewichtiger SSH-Server, der standardm&auml;&szlig;ig auf DietPi-Systemen installiert ist.
Hinweis: Sie k&ouml;nnen Ihren SSH-Server jederzeit mit der *DietPi-Software* austauschen oder wechseln.

![Dropbear-Logo](../assets/images/dietpi-software-sshserver-dropbear.jpg){: width="150" height="121" loading="lazy"}

=== "Zugriff auf die Weboberfl&auml;che"

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

OpenSSH bietet einen funktionsreichen SSH-Server mit SFTP/SCP-Unterst&uuml;tzung.
Hinweis: Sie k&ouml;nnen Ihren SSH-Server jederzeit mit der *DietPi-Software* austauschen oder wechseln.

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

    Mit WinSCP k&ouml;nnen Sie Dateien und Ordner auf Ihr DietPi-Ger&auml;t &uuml;bertragen ([WinSCP-Downloadseite](https://winscp.net/eng/download.php)).

***

Website: <https://www.openssh.com>
Wikipedia: <https://wikipedia.org/wiki/OpenSSH>

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
