# DNS/DHCP Server einrichten in Windows

## Vorbereitung

### Windows Server 2019 Englisch installieren

1. Custom
2. Workstation 16.2.x
3. I will install the operating system later
4. Microsoft Windows, Windows Server 2019
5. C:\VirtualMachines\Modul123\WindowsServer
6. UEFI
7. 2 Prozessor, 2 Cores
8. 4 GiB RAM
9. NAT
10. LSI Logic SAS
11. NVMe
12. Create Virtual Disk
13. 60 GB, single file
14. WindowsServer.vmdk
15. Windows Server CD hinzufügen

#### Normale Windows Server installation

1. Language: English
2. Time and Currency Format: Swiss German
3. Keyboard Layout: US-International
4. I don't have a product key
5. Windows Server 2019 Standard (Desktop Experience)
6. Accept License Agreement
7. Custom
8. Ganze Disk auswählen
9. Nachdem Restart solltest du jetzt ein Passwort eingeben, in meinem Fall: Arlind123!


#### DHCP Server einrichten in Windows Server

1. VMware Tools installieren, wie in Windows 10 und neustarten.


##### Fixe IP Verteilen und Hostnamen angeben.
2. Fixe IP in Adapter Optionen einstellen
  - 192.168.100.4
  - 255.255.255.0
  - kein Gateway
  - 192.168.100.4
  - 8.8.8.8

3. In "View Advanced system settings" den Hostnamen einsellen: in meinem Fall WinServer
