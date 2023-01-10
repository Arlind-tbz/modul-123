# DHCP Server einrichten in Linux
## Vorbereitung

1. Ubuntu Server in VMware Workstation installieren.
2. sudo apt-get update
3. sudo apt-get upgrade
4. sudo apt install open-vm-tools
Sobald man dies hat, sollte man neu starten mit `Sudo reboot` <br>
![Sudo apt-get update](images/Bild1.png) <br>
![Sudo apt-get upgrade](images/Bild2.png) <br>
![sudo apt install open-vm-tools](images/Bild3.png) <br>

Wir brauchen 2 verschiedene Netzwerk Interfaces. 1x Host only und 1x NAT <br>
![Netzwerk Adapter](images/Bild4.png)
## Konfiguration DHCP

1. Wir installieren den DHCP-Dienst mit `sudo apt install isc-dhcp-server` runter.
2. und danach gehen wir zum Pfad mit den DHCP-Konfigurationen mit `cd /etc/dhcp/`.
3. Damit falls wir fehler machen unsere originale Datei zurückbringen können müssen wir `cp dhcpd.conf dhcpd.conf.cp`.
4. Jetzt editieren wir die dhcpd.conf Datei mit `sudo nano dhcpd.conf`.
5. In Dieser Datei müssen wir das # von #Authorative; entfernen. <br>
![authorative](images/Bild5.png)
6. Und die IP-Range anpassen und auch wieder die Comments entfernen. <br>
![IP-Range](images/Bild6.png)
7. Jetzt müssen wir den Netzwerk Adapter überprüfen und sich den Host only Adapter merken. In meinem Fall ens37. <br>
![ens37](images/Bild8.png)
8. Jetzt müssen wir diesen Adapter in `/etc/default/isc-dhcp-server` einfügen mit `sudo nano /etc/default/isc-dhcp-server` <br>
![ipv4fix](images/Bild10.png)

## Fixe IP-Adresse konfigurieren
1. Die IP Konfiguration ist im Pfad `/etc/netplan/`
2. Und hier erstellen wir eine Datei, bei der wir unsere Einstellungen speichern mit `sudo touch 01-netcfg.yaml`
3. Diese Datei müssen wir jetzt auch editieren mit `sudo nano 01-netcfg.yaml` <br>
![netcfg](images/Bild11.png) <br>
Sobald wir dies haben, haben wir eine fixe IP-Adresse auf dem Adapter ens37.
## Testen

1. Zuerst schauen wir ob der Client überhaupt funktioniert mit `1.	sudo service isc-dhcp-server start` und `1.	sudo service isc-dhcp-server status`
2. Danach können wir eine Windows VM öffnen und diesen mit dem Custom Netzwerk verbinden.
3. In der Windows VM müssen wir jetzt cmd öffnen.
4. In cmd geben wir jetzt den Command `ipconfig /renew` <br>
Jetzt sollten wir unsere IP-Adresse erneuern, und dies sollte es durch den DHCP-Dienst machen. <br>
![cmd](images/Bild12.png)
5. Der letzte Test ist es in der Ubuntu Server VM den Command `dhcp-lease-list` einzugeben, und wenn es einen Eintrag gibt, funktioniert der Dienst. <br>
![dhcp-lease-list](images/Bild13.png)
