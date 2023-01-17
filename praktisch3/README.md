# Samba

## Samba installieren

Bevor man etwas auf Linux macht oder installiert, führen Sie zuerst diese zwei Kommandos aus:
1. `sudo apt update`
2. `sudo apt upgrade`

3. Sobald diese abgeschlossen sind, können wir Samba installieren `sudo apt install samba -y`
4. Um zu überprüfen, ob Samba funktioniert, können wir diese beiden Kommandos ausführen:
`samba -V` `systemctl status smbd`
![testsamba](images/testsamba.png)

## Shared Directory erstellen

1. Erstellen Sie nun ein Verzeichnis `sudo mkdir -p /home/sharing`
2. Um zu testen, ob das Verzeichnis erstellt wurde, führen Sie ein `ls /home` aus
3. Mit diesem Kommando wird das Verzeichnis keiner Gruppe zugeordnet `sudo chown nobody:nogroup /home/sharing`
4. Und mit diesem Kommando geben wir jedem Benutzer, der Zugriff auf das Verzeichnis hat, Schreib-, Les- und Ausführungsrechte `chmod -R 777 /home/sharing`

5. Um das öffentliche Verzeichnis einzurichten, müssen wir `sudo vim /etc/samba/smb.conf` oder `sudo nano /etc/samba/smb.conf` ausführen und dort unsere Konfiguration ergänzen. <br><br>

6. Hier müssen wir unseren Adapter angeben. <br>
![veraenderungen1](images/veraenderung1.png)

7. Mit diesem Eintrag ganz unten in der Datei, geben wir dem Samba Server genug Informationen, um einen File Server zu erstellen.
![veraenderungen2](images/veraenderung2.png) <br>

8. `sudo smbpasswd -a arlind`
9. `sudo systemctl restart smbd`

Sobald das erledigt ist, gehen wir zu unserem Client und können ein Netzlaufwerk einbinden und benutzen.

![einbinden](images/einbinden.png)
![sambaclient](images/sambaclient.png)
