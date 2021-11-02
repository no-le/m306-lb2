Werkstattauftrag W06 Pi-NAS
===========================================================================

**Inhaltsverzeichnis:**
-------------------
---
**1. Autoren, Versionierung des Dokumentes**
   - Noah Lennemann, noah.lennemann@edu.tbz.ch
   - Leon Rezek, leon.rezek@edu.tbz.ch
   - Version 1.2

---
   
**2. Einführung** 
---
   - _**Beschreibung: Welche Funktionen wird der Service erfuellen**_
---
Pi NAS
- Pi-Nas ist ein Netzwerkspeicher der mit den Samba Packages installiert wurde, der im eigenen Netzwerk den Geräten Speicher zur Verfügung stellt. Über einen Freigegebenen Netzwerkpfad hat man die Möglichkeit Dateien herunterzuladen und hochzuladen. Zudem ist das Ziel, dass der Freigegebene Ordner über einen USB-Stick gemountet wird. 
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


Danach wird mit dem unten folgenden Command getestet, ob alles in Ordnung ist und der Server läuft.




Die Konfigurationsdatei müssen wir später noch anpassen. Sichern tuen wir wie folgt: 




Im nächsten Schritt muss man ein Ordner erstellen auf dem Pi, der Freigegeben werden sollte:



Nun müssen wir die Konfigurationsdatei anpassen und ein paar Zeilen für die Freigabe hinzufügen. In diesem Fall müssen sie über den Command: 


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




**USB-Stick mounten**

Zuerst müssen wir die benötigten Treiber für NTFS-Festplatten herunterladen.

sudo apt-get -y install ntfs-3g hfsutils hfsprogs exfat-fuse

Mit folgendem Befehl müssen wir den device Pfad des USB-Stick herausfinden:

sudo blkid -o list -w /dev/null

Zum Schluss muss man den USB-Stick über einen Befehl mounten. Hier muss man beachten, dass man am Schluss den richtigen USB-Stick Pfad und den korrekten Pfad eingibt, den man mounten will.



sudo mount -t ntfs-3g -o uid=1000,gid=1000 /dev/sda1 /home/pi/sambashare/


Tipps: 

/dev/sda1/ = USB-Stick Pfad

/home/pi/sambashare = Freigegebenen Pfad

Sollte die Meldung erscheinen, dass die Fehlermeldung kommt, dass der Datenträger schon gemountet wurde, muss man den zuerst unmounten.
 

Wenn die Fehlermeldung erscheint, dass man im mount Befehl, einen Value eintragen muss, sollte man zusätzlich auch beachten, dass die uid, und gid ID im Command korrekt ist. Um herauszufinden, welche uid und gid der Benutzer hat, muss man den Befehl: "id" eingeben.



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
