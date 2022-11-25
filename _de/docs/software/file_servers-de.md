# Dateiserver

## Überblick

- [**ProFTPD - Einfacher, effizienter, leichtgewichtiger FTP-Dateiserver**](#proftpd)
- [**Samba - Dateiserver mit vielen Funktionen**](#samba)
- [**vsftpd - FTP-Dateiserver mit vielen Funktionen**](#vsftpd)
- [**NFS - Netzwerk-Dateisystemserver**](#nfs)

??? info "Wie führe ich **DietPi-Software** aus und installiere **optimierte Software**-Elemente?"
    Um eines der unten aufgeführten **DietPi-optimierten Softwareelemente** zu installieren, führen Sie es über die Befehlszeile aus:

    ```sh
    dietpi-software
    ```

    Wählen Sie **Software durchsuchen** und wählen Sie einen oder mehrere Artikel aus. Wählen Sie abschließend „Installieren“.
    DietPi führt alle notwendigen Schritte aus, um diese Softwareelemente zu installieren und zu starten.

    ![DietPi-Software-Menü-Screenshot](../assets/images/dietpi-software.jpg){: width="643" height="365" loading="lazy"}

    Um alle DietPi-Konfigurationsoptionen anzuzeigen, lesen Sie den Abschnitt [DietPi Tools](../../dietpi_tools/).

[Zurück zur **Liste der optimierten Software**](../../software/)

## ProFTPD

ProFTPD ermöglicht Ihnen den schnellen und effizienten Zugriff auf Dateien/Musik/Downloads usw. auf Ihrem DietPi-System mit minimalem Overhead.

![DietPi-Dateiserver-Software ProFTPD](../assets/images/dietpi-software-fileservers-proftpd.png)

=== "Zugriff mit Windows"

    Der Zugriff auf ProFTPD mit **Windows** erfolgt wie folgt:

    - Gehen Sie zu Arbeitsplatz (Windows Explorer).
    - Geben Sie oben in der Adressleiste "ftp://dietpi:dietpi@192.168.0.100" ein und drücken Sie die Eingabetaste.

    Ändern Sie 192.168.0.100 in die IP-Adresse Ihres DietPi-Systems.

=== "Zugriff mit einem FTP-Client"

    Der Zugriff auf ProFTPD mit einem **FTP-Client** erfolgt wie folgt:

    - Benutzername = `dietpi`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort. Standard ist „dietpi“.
    - Adresse = Ihre IP-Adresse (zB: 192.168.0.100)
    - Port = 21

=== "Zielverzeichnis"

    Das Zielverzeichnis kann geändert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis (innerhalb der Konfigurationsdatei `/etc/proftpd/proftpd.conf`) ersetzt wird:

    ```sh
    systemctl stop proftpd
    sed -i '/DefaultRoot /c\DefaultRoot /Path/To/Directory' /etc/proftpd/proftpd.conf
    systemctl start proftpd
    ```

=== "Jailing"

    Jailing bedeutet, Benutzer in ihren Home-Ordnern zu sperren.

    *Jailing* kann in der Konfigurationsdatei `/etc/proftpd/proftpd.conf` über aktiviert werden

    ```sh
    systemctl stop proftpd
    sed -i '/DefaultRoot /c\DefaultRoot ~' /etc/proftpd/proftpd.conf
    systemctl start proftpd
    ```

***

Wikipedia: <https://wikipedia.org/wiki/ProFTPD>

## Samba

Mit dem Samba-Server können Sie Dateien auf Ihrem DietPi-System basierend auf dem bekannten SMB-Netzwerkprotokoll problemlos freigeben.

![DietPi-Dateiserver-Software Samba](../assets/images/dietpi-software-fileservers-samba.png)

=== "Zugriff auf Samba"

    Der Zugriff auf den Samba-Dateiserver wird wie folgt erreicht:

    - Adresse = `\\192.168.0.100\dietpi`
    - Benutzername = `dietpi`
    - Passwort = `<Ihr globales Anwendungspasswort>` (Standard: `dietpi`)

=== "Samba-Passwort ändern"

    Das Samba-Passwort kann mit geändert werden

    ```sh
    smbpasswd -a dietpi
    ```

=== "Gültigen Benutzer hinzufügen/ändern"

    Führen Sie die folgenden Schritte aus, um den gültigen Benutzer hinzuzufügen/zu ändern:

    - Bearbeiten Sie `/etc/samba/smb.conf`
    - Suche den Eintrag `[dietpi]`, ändere `valid users = username_i_require`
    - Fügen Sie den Benutzer mit `smbpasswd -a username_i_require` zu Samba hinzu
    - Dienste mit `systemctl restart nmbd smbd` neu starten

    Sie können sich jetzt mit dem oben eingegebenen Benutzernamen und Passwort mit dem Samba-Server verbinden.

=== "Zielverzeichnis"

    Das Zielverzeichnis kann geändert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis ersetzt wird (innerhalb der Konfigurationsdatei `/etc/samba/smb.conf`):

    ```sh
    sed -i '/path = /c\path = /Path/To/Directory' /etc/samba/smb.conf
    systemctl restart nmbd smbd
    ```

***

Wikipedia: <https://wikipedia.org/wiki/Samba_(software)>

YouTube-Video-Tutorial: `Raspberry Pi als Datei-Server - einfache Installation eines Fileservers Samba unter DietPi`.

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/XB2F_Gyjw0s" frameborder="0" allow="accelerometer; Autoplay; Zwischenablage schreiben; verschlüsselte Medien ; Gyroskop; Bild-in-Bild" allowfullscreen></iframe>

## vsftpd

Sehr sicherer FTP-Dateiserver mit funktionsreichen Sicherheitsoptionen.

![DietPi-Dateiserver-Software vsftpd](../assets/images/dietpi-software-fileservers-vsftpd.png)

=== "Zugriff mit Windows"

    Der Zugriff auf vsftpd mit **Windows** erfolgt wie folgt:

    - Gehen Sie zu Arbeitsplatz (Windows Explorer).
    - Geben Sie oben in der Adressleiste "ftp://dietpi:dietpi@192.168.0.100" ein und drücken Sie die Eingabetaste.

    Ändern Sie „192.168.0.100“ in die IP-Adresse Ihres DietPi-Systems.

=== "Zugriff mit einem FTP-Client"

    Der Zugriff auf vsftpd mit einem **FTP-Client** erfolgt wie folgt:

    - Benutzername = `dietpi`
    - Passwort = Dasselbe wie Ihr Root-Login-Passwort. Standard ist `dietpi`.
    - Adresse = Ihre IP-Adresse (zB: 192.168.0.100)
    - Port = 21

=== "Zielverzeichnis"

    Das Zielverzeichnis kann geändert werden, indem **/Path/To/Directory** durch Ihr Zielverzeichnis ersetzt wird (innerhalb der Konfigurationsdatei `/etc/vsftpd.conf`):

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

    Die Konfiguration des NFS-Zugriffs erfolgt über **Dateien exportieren**.
    Sie können die Datei „/etc/exports“ bearbeiten sowie weitere Exportdateien im Verzeichnis „/etc/exports.d“ hinzufügen.

**Erklärungen zum Exportdateiformat** sind im Internet verfügbar oder können in den Manpages nachgelesen werden (verwenden Sie `man exports`, dazu muss das Paket **man** installiert sein).

    Nach Änderung der Zugangskonfiguration können die Exportinformationen per Befehl neu ausgelesen werden

    ```
    exportfs -ra
    ```

    Alternativ können Sie den Dienst neu starten (`systemctl restart nfs-kernel-server`).

    Die aktuelle Zugangskonfiguration kann mit dem Befehl angezeigt werden

    ```
    exportfs
    ```

    Auf der Client-Seite können Sie die mountbaren Exporte mit dem Befehl abfragen

    ```
    showmount -e <NFS_SERVER>
    ```

=== "Standardkonfiguration / Sicherheit erhöhen"

    Standardmäßig exportiert die DietPi NFS-Installation das Verzeichnis `/mnt/dietpi_userdata` für alle. Dies wird in `/etc/exports.d/dietpi.exports` konfiguriert. Sie können diese Datei bearbeiten, um den Zugriff einzuschränken.

    Beispielsweise könnten Sie den Zugriff auf die NFS-Freigabe einschränken, indem Sie einen IP-Adressbereich festlegen:

    - Bearbeiten Sie die folgende Datei: `/etc/exports.d/dietpi.exports`
    - Benutzern den Zugriff nur mit einem IP-Adressbereich von 192.168.0.1-255 zu ermöglichen

        ```
        /mnt/dietpi_userdata 192.168.0.*(rw,async,no_root_squash,fsid=0,crossmnt,no_subtree_check)
        ```

    - Aktivieren Sie die neue Konfiguration (`systemctl restart nfs-kernel-server` oder `exportfs -ra`)

***

Wikipedia: <https://wikipedia.org/wiki/Network_File_System>

[Zurück zur **Liste der optimierten Software**](../../software/)
