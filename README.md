Werkstattauftrag W06 Pi-NAS
===========================================================================

**Inhaltsverzeichnis:**
-------------------
---
**1. Autoren, Versionierung des Dokumentes**
   - Noah Lennemann, noah.lennemann@edu.tbz.ch
   - Leon Rezek, leon.rezek@edu.tbz.ch
   - Version 1.1

---
   
**2. Einführung** 
---
   - _**Beschreibung: Welche Funktionen wird der Service erfuellen**_
---
Pi NAS
- Pi-Nas ist ein Netzwerkspeicher der mit den Samba Packages installiert wurde, der im eigenen Netzwerk den Geräte Speicher zur Verfügung stellt. Über einen Freigegebenen Netzwerkpfad hat der Benutzer die Möglichkeit Dateien herunterzuladen und hochzuladen. 
---
   - _**Vorgesehener Zeitaufwand für die Realisierung**_
---
Die Umsetzung des Projekts dauert ungefähr 2 Lektionen
   
---
   - _**Stolpersteine**_
---
---
**3. Benötigte Hard- und Software**
---
   - Hardware

1 x Raspberry PI mindestens PI 4 <br>
1 x Monitor (ist einfacher als verschiedene Viewer bsp. VNC) <br>
1 x SD Karte 8 GB <br>
1 x Netzwerkkabel ca. 1 Meter <br>

---
   - Software

1 x Putty oder VNC Viewer
1 x Samba
	
---
**4. Installationsanleitung**
---
Nach dem klassischen sudo apt update und sudo apt upgrade, kommen wir dazu, Samba zu installieren. Dies machen wir mit dem untenstehenden Command. Die Installationsabfrage bestätigen wir mit "J".

![grafik](https://user-images.githubusercontent.com/89446419/139811389-690345b4-06a5-4ceb-b7d0-6720bae1cd3b.png)

Danach wird mit dem unten folgenden Command getestet, ob alles in Ordnung ist und der Server läuft.

![grafik](https://user-images.githubusercontent.com/89446419/139811405-f43ae8ad-f039-403a-8cd2-a79b88e0731e.png)

![grafik](https://user-images.githubusercontent.com/89446419/139811441-53971b6d-30a0-4a3f-bfac-997d2e586a31.png)


Die Konfigurationsdatei müssen wir später noch anpassen. Sichern tuen wir wie folgt: 

![grafik](https://user-images.githubusercontent.com/89446419/139811463-a9219352-77a9-4aa7-951c-6f7bdc1d1c3e.png)


Im nächsten Schritt muss man ein Ordner erstellen auf dem Pi, der Freigegeben werden sollte:

![grafik](https://user-images.githubusercontent.com/89446419/139811706-61560540-48e2-4fcd-a266-a37877ee4bb4.png)


Nun müssen wir die Konfigurationsdatei anpassen und ein paar Zeilen für die Freigabe hinzufügen. In diesem Fall müssen sie über den Command: 

![grafik](https://user-images.githubusercontent.com/89446419/139811756-48a844c9-7913-46df-91e5-c7047df4572b.png)

In die Konfigurationsdatei zugreifen und folgende Zeilen Hinzufügen:

[sambashare]
    comment = Samba on Ubuntu
    path = /home/username/sambashare
    read only = no
    browsable = yes


Am Schluss muss man den Service restarten und fertig.

sudo service smbd restart

Test:

Im Windows Explorer auf dem Notebook muss man jetzt über den Pfad mit der IP-Adresse und der festgelegten Freigabe die man in der Konfigurationsdatei festgelegt hat, zugreifen.

BSP: \\172.16.17.137\Pi-Nas\

![grafik](https://user-images.githubusercontent.com/89446419/139811937-dd474ed3-2446-4a41-a649-27ff500b917e.png)



**USB-Stick mounten**

Zuerst müssen wir die benötigten Treiber für NTFS-Festplatten herunterladen.

sudo apt-get -y install ntfs-3g hfsutils hfsprogs exfat-fuse

Mit folgendem Befehl müssen wir den device Pfad des USB-Stick herausfinden:

sudo blkid -o list -w /dev/null

Zum Schluss muss man den USB-Stick über einen Befehl mounten. Hier muss man beachten, dass man am Schluss den richtigen USB-Stick Pfad und den korrekten Pfad eingibt, den man mounten will.

![grafik](https://user-images.githubusercontent.com/89446419/139812021-63f054ed-412d-4f20-9ac3-24de453e3336.png)

sudo mount -t ntfs-3g -o uid=1000,gid=1000 /dev/sda1 /home/pi/sambashare/


Tipps: 

/dev/sda1/ = USB-Stick Pfad

/home/pi/sambashare = Freigegebenen Pfad

Sollte die Meldung erscheinen, dass die Fehlermeldung kommt, dass der Datenträger schon gemountet wurde, muss man den zuerst unmounten.
 

Wenn die Fehlermeldung erscheint, dass man im mount Befehl, einen Value eintragen muss, sollte man zusätzlich auch beachten, dass die uid, und gid ID im Command korrekt ist. Um herauszufinden, welche uid und gid der Benutzer hat, muss man den Befehl: "id" eingeben.
![grafik](https://user-images.githubusercontent.com/89446419/139811290-ae4015af-0891-41f9-befd-13b72d47d840.png)



---
**5. Qualitätskontrolle**
---
- Um die Funktonalität des Sambas Dienstes zu testen, kann man folgenden Command eingeben:

- sudo service smdb status:
- ![grafik](https://user-images.githubusercontent.com/89446419/138848861-c8373b4b-ef10-4f69-888c-fb35f206a59f.png)
 
- testparm
- ![grafik](https://user-images.githubusercontent.com/89446419/138849314-77a37703-1458-4c62-9a9d-a0e9bca6275b.png)

---

**6. Error-Handling** 
---
- Bei der Installation der Samba-Packete hatten wir das Problem, dass wir zuerst die neusten Updates installieren mussten. Bei der Eingabe des Commands: "Sudo apt-get update" hatten wir das Problem, dass eine Fehlermeldung erschien. In der stand, dass man das Depot mit dem Suite Wert von : "stable" in "oldstable" ändern mussten.
---
**7. Quellen**
---

<a href=https://exerror.com/repository-http-deb-debian-org-debian-buster-updates-inrelease-changed-its-suite-value-from-stable-updates-to-oldstable-updates>Samba Pakete Debugging</a> 

<a href=https://ittweak.de/raspberry-pi-nas-server-datei-server-einrichten-mit-samba>USB-Stick mounten</a> 


---

**8. OpenSource Lizenz**


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/ch/88x31.png" /></a><br />Dieses Werk ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/">Creative Commons Namensnennung - Nicht-kommerziell - Weitergabe unter gleichen Bedingungen 3.0 Schweiz Lizenz</a>

 

- - -
