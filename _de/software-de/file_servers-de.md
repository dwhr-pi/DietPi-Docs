# Dateiserver

## &Uuml;berblick

- [**ProFTPD - Einfacher, effizienter, leichtgewichtiger FTP-Dateiserver**](#proftpd)
- [**Samba - Dateiserver mit vielen Funktionen**](#samba)
- [**vsftpd - FTP-Dateiserver mit vielen Funktionen**](#vsftpd)
- [**NFS - Netzwerk-Dateisystemserver**](#nfs)

??? info "Wie f&uuml;hre ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgef&uuml;hrten **DietPi-optimierten Softwareelemente** zu installieren, f&uuml;hren Sie es &uuml;ber die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    W&auml;hlen Sie **Software durchsuchen** und w&auml;hlen Sie einen oder mehrere Artikel aus. W&auml;hlen Sie abschlie&szlig;end `Installieren`.
    DietPi f&uuml;hrt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Men&uuml;-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)

## ProFTPD

ProFTPD erm&ouml;glicht Ihnen den schnellen und effizienten Zugriff auf Dateien/Musik/Downloads usw. auf Ihrem DietPi-System mit minimalem Overhead.

![DietPi-Dateiserver-Software ProFTPD](../assets/images/dietpi-software-fileservers-proftpd.png)

=== "Zugriff mit Windows"

    Der Zugriff auf ProFTPD mit **Windows** erfolgt wie folgt:

    - Gehen Sie zu Arbeitsplatz (Windows Explorer).
    - Geben Sie oben in der Adressleiste "ftp://dietpi:dietpi@192.168.0.100" ein und dr&uuml;cken Sie die Eingabetaste.

    &Auml;ndern Sie 192.168.0.100 in die IP-Adresse Ihres DietPi-Systems.

=== "Zugriff mit einem FTP-Client"

    Der Zugriff auf ProFTPD mit einem **FTP-Client** erfolgt wie folgt:

    - Benutzername = `dietpi`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort. Standard ist `dietpi`.
    - Adresse = Ihre IP-Adresse (zB: 192.168.0.100)
    - Port = 21

=== "Zielverzeichnis"

    Das Zielverzeichnis kann ge&auml;ndert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis (innerhalb der Konfigurationsdatei `/etc/proftpd/proftpd.conf`) ersetzt wird:

    ```sh
    systemctl stop proftpd
    sed -i '/DefaultRoot /c\DefaultRoot /Path/To/Directory' /etc/proftpd/proftpd.conf
    systemctl start proftpd
    ```

=== "Jailing"

    Jailing bedeutet, Benutzer in ihren Home-Ordnern zu sperren.

    *Jailing* kann in der Konfigurationsdatei `/etc/proftpd/proftpd.conf` &uuml;ber aktiviert werden

    ```sh
    systemctl stop proftpd
    sed -i '/DefaultRoot /c\DefaultRoot ~' /etc/proftpd/proftpd.conf
    systemctl start proftpd
    ```

***

Wikipedia: <https://wikipedia.org/wiki/ProFTPD>

## Samba

Mit dem Samba-Server k&ouml;nnen Sie Dateien auf Ihrem DietPi-System basierend auf dem bekannten SMB-Netzwerkprotokoll problemlos freigeben.

![DietPi-Dateiserver-Software Samba](../assets/images/dietpi-software-fileservers-samba.png)

=== "Zugriff auf Samba"

    Der Zugriff auf den Samba-Dateiserver wird wie folgt erreicht:

    - Adresse = `\\192.168.0.100\dietpi`
    - Benutzername = `dietpi`
    - Passwort = `<Ihr globales Anwendungspasswort>` (Standard: `dietpi`)

=== "Samba-Passwort &auml;ndern"

    Das Samba-Passwort kann mit ge&auml;ndert werden

    ```sh
    smbpasswd -a dietpi
    ```

=== "G&uuml;ltigen Benutzer hinzuf&uuml;gen/&auml;ndern"

    F&uuml;hren Sie die folgenden Schritte aus, um den g&uuml;ltigen Benutzer hinzuzuf&uuml;gen/zu &auml;ndern:

    - Bearbeiten Sie `/etc/samba/smb.conf`
    - Suche den Eintrag `[dietpi]`, &auml;ndere `valid users = username_i_require`
    - F&uuml;gen Sie den Benutzer mit `smbpasswd -a username_i_require` zu Samba hinzu
    - Dienste mit `systemctl restart nmbd smbd` neu starten

    Sie k&ouml;nnen sich jetzt mit dem oben eingegebenen Benutzernamen und Passwort mit dem Samba-Server verbinden.

=== "Zielverzeichnis"

    Das Zielverzeichnis kann ge&auml;ndert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis ersetzt wird (innerhalb der Konfigurationsdatei `/etc/samba/smb.conf`):

    ```sh
    sed -i '/path = /c\path = /Path/To/Directory' /etc/samba/smb.conf
    systemctl restart nmbd smbd
    ```

***

Wikipedia: <https://wikipedia.org/wiki/Samba_(software)>

YouTube-Video-Tutorial: `Raspberry Pi als Datei-Server - einfache Installation eines Fileservers Samba unter DietPi`.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/XB2F_Gyjw0s" frameborder="0" allow="accelerometer; Autoplay; Zwischenablage schreiben; verschl&uuml;sselte Medien ; Gyroskop; Bild-in-Bild" allowfullscreen></iframe>

## vsftpd

Sehr sicherer FTP-Dateiserver mit funktionsreichen Sicherheitsoptionen.

![DietPi-Dateiserver-Software vsftpd](../assets/images/dietpi-software-fileservers-vsftpd.png)

=== "Zugriff mit Windows"

    Der Zugriff auf vsftpd mit **Windows** erfolgt wie folgt:

    - Gehen Sie zu Arbeitsplatz (Windows Explorer).
    - Geben Sie oben in der Adressleiste "ftp://dietpi:dietpi@192.168.0.100" ein und dr&uuml;cken Sie die Eingabetaste.

    &Auml;ndern Sie `192.168.0.100` in die IP-Adresse Ihres DietPi-Systems.

=== "Zugriff mit einem FTP-Client"

    Der Zugriff auf vsftpd mit einem **FTP-Client** erfolgt wie folgt:

    - Benutzername = `dietpi`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort. Standard ist `dietpi`.
    - Adresse = Ihre IP-Adresse (zB: 192.168.0.100)
    - Port = 21

=== "Zielverzeichnis"

    Das Zielverzeichnis kann ge&auml;ndert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis ersetzt wird (innerhalb der Konfigurationsdatei `/etc/vsftpd.conf`):

    ```sh
    sed -i '/local_root=/c\local_root=/Path/To/Directory' /etc/vsftpd.conf
    systemctl restart vsftpd
    ```

***

Wikipedia: <https://wikipedia.org/wiki/Vsftpd>

##NFS

Netzwerk-Dateisystemserver.

![DietPi-Dateiserver-Software NFS](../assets/images/dietpi-software-fileservers-nfs.png)

=== "Zugriff auf eine NFS-Freigabe"

    Der Zugriff auf die NFS-Freigabe mit einem **NFS-Client** wird wie folgt erreicht:

    - Adresse = IP-Adresse Ihres DietPi-Systems (zB: 192.168.0.100)
    - Port	= 2049

=== "Zugangskonfiguration"

    Die Konfiguration des NFS-Zugriffs erfolgt &uuml;ber **Dateien exportieren**.
    Sie k&ouml;nnen die Datei `/etc/exports` bearbeiten sowie weitere Exportdateien im Verzeichnis `/etc/exports.d` hinzuf&uuml;gen.

**Erkl&auml;rungen zum Exportdateiformat** sind im Internet verf&uuml;gbar oder k&ouml;nnen in den Manpages nachgelesen werden (verwenden Sie `man exports`, dazu muss das Paket **man** installiert sein).

    Nach &Auml;nderung der Zugangskonfiguration k&ouml;nnen die Exportinformationen per Befehl neu ausgelesen werden

    ```
    exportfs -ra
    ```

    Alternativ k&ouml;nnen Sie den Dienst neu starten (`systemctl restart nfs-kernel-server`).

    Die aktuelle Zugangskonfiguration kann mit dem Befehl angezeigt werden

    ```
    exportfs
    ```

    Auf der Client-Seite k&ouml;nnen Sie die mountbaren Exporte mit dem Befehl abfragen

    ```
    showmount -e <NFS_SERVER>
    ```

=== "Standardkonfiguration / Sicherheit erh&ouml;hen"

    Standardm&auml;&szlig;ig exportiert die DietPi NFS-Installation das Verzeichnis `/mnt/dietpi_userdata` f&uuml;r alle. Dies wird in `/etc/exports.d/dietpi.exports` konfiguriert. Sie k&ouml;nnen diese Datei bearbeiten, um den Zugriff einzuschr&auml;nken.

    Beispielsweise k&ouml;nnten Sie den Zugriff auf die NFS-Freigabe einschr&auml;nken, indem Sie einen IP-Adressbereich festlegen:

    - Bearbeiten Sie die folgende Datei: `/etc/exports.d/dietpi.exports`
    - Benutzern den Zugriff nur mit einem IP-Adressbereich von 192.168.0.1-255 zu erm&ouml;glichen

        ```
        /mnt/dietpi_userdata 192.168.0.*(rw,async,no_root_squash,fsid=0,crossmnt,no_subtree_check)
        ```

    - Aktivieren Sie die neue Konfiguration (`systemctl restart nfs-kernel-server` oder `exportfs -ra`)

***

Wikipedia: <https://wikipedia.org/wiki/Network_File_System>

[Zur&uuml;ck zur **Liste der optimierten Software**](../../software/)
