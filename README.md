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
**4.1.1 Zuerst muss sichergestellt werden, dass die aktuelle Version des PI’s installiert ist. Wenn nicht, sollten diese umgehend installiert werden. Nun sollten die benötigten Packete installiert werden, diese sind in der Grafik aufgelistet. **

samba samba-common smbclientcifs-util

---
**4.1.2 Darauffolgend kann der Status abgefragt werden. Die Services:« smbd» und « nmbd» sollten getestet werden. Beide sollte «active (running)» zurückgeben.   **

![grafik](https://user-images.githubusercontent.com/89446419/139814807-4e64c3ab-98f4-48a3-9590-e0d1d4dc691e.png)

![grafik](https://user-images.githubusercontent.com/89446419/139814826-66d64b31-9777-4014-a8ec-cc84d58cdb0f.png)


---
**4.1.3 Nun muss die Konfigurations Datei an einen neuen Ort gespeichert werden.**

![grafik](https://user-images.githubusercontent.com/89446419/139814862-7ecc3274-622a-488c-a12d-2d1286f68d61.png)

---

**4.1.4 Nun sollte ein Ordner erstellt werden, welcher dann der Freigabe Ordner ist. Dieser wird dann auf dem anderen Client angezeigt.**




---
**4.1.5 Nun müssen wir die Konfigurationsdatei anpassen und ein paar Zeilen für die Freigabe hinzufügen. Mit einem gewünschten Editor das File öffnen.



**In die Konfigurationsdatei zugreifen und folgende Zeilen Hinzufügen:**

	[sambashare]
    	comment = Samba on Ubuntu
    	path = /home/username/sambashare
    	read only = no
    	browsable = yes

---
**4.1.6 Um die Änderungen zu speichern muss der Service neugestartet werden.**

	sudo service smbd restart

---
**4.2 Test:**
---

**Im Windows Explorer auf dem Notebook muss man jetzt über den Pfad mit der IP-Adresse und der festgelegten Freigabe die man in der Konfigurationsdatei
festgelegt hat, zugreifen.**

	BSP: \\172.16.17.137\Pi-Nas\
	
![grafik](https://user-images.githubusercontent.com/89446419/139815002-d48b941c-9ecc-4e5f-bcaa-42e58a106861.png)

---
**4.3 USB-Stick mounten**
---
**4.3.1 Zuerst müssen wir die benötigten Treiber für NTFS-Festplatten herunterladen.**

	sudo apt-get -y install ntfs-3g hfsutils hfsprogs exfat-fuse

---

**4.3.2 Mit folgendem Befehl müssen wir den device Pfad des USB-Stick herausfinden:**

	sudo blkid -o list -w /dev/null

---

**4.3.3 Zum Schluss muss man den USB-Stick über einen Befehl mounten. Hier muss man beachten, dass man am Schluss den richtigen USB-Stick Pfad und den korrekten Pfad
	eingibt, den man mounten will.**


	sudo mount -t ntfs-3g -o uid=1000,gid=1000 /dev/sda1 /home/pi/sambashare/

---
**Tipps:** 

_/dev/sda1/ = USB-Stick Pfad_

_/home/pi/sambashare = Freigegebenen Pfad_

_Sollte die Fehlermeldung erscheinen, dass der Datenträger schon gemountet wurde, muss man den zuerst unmounten._
 

_Wenn die Fehlermeldung erscheint, dass man im mount Befehl einen Value eintragen muss, sollte man zusätzlich auch beachten, dass die uid, und gid ID im
Command korrekt ist. Um herauszufinden, welche uid und gid der Benutzer hat, muss man den Befehl: "id" eingeben._



---
**5. Qualitätskontrolle**
---
Um die Funktonalität des Sambas Dienstes zu testen, kann man folgenden Command eingeben:

	sudo service smdb status:
![grafik](https://user-images.githubusercontent.com/89446419/138848861-c8373b4b-ef10-4f69-888c-fb35f206a59f.png)
 
 	testparm
![grafik](https://user-images.githubusercontent.com/89446419/138849314-77a37703-1458-4c62-9a9d-a0e9bca6275b.png)

---

**6. Error-Handling** 
---
- Bei der Installation der Samba-Packete hatten wir das Problem, dass wir zuerst die neusten Updates installieren mussten. Bei der Eingabe des Commands: "Sudo apt-get update" hatten wir das Problem, dass eine Fehlermeldung erschien. In der stand, dass man das Depot mit dem Suite Wert von : "stable" in "oldstable" ändern mussten.

- Beim Mounten des USB-Stick, hatten wir das Problem, dass der Fehler kam, dass man einen Value unter uid, und gid ID eintragen muss. Nach einbischen Googlen, wussten wir wo man diese zwei Werte findet.
---
**7. Quellen**
---

<a href=https://exerror.com/repository-http-deb-debian-org-debian-buster-updates-inrelease-changed-its-suite-value-from-stable-updates-to-oldstable-updates>Samba Pakete Debugging</a> 

<a href=https://ittweak.de/raspberry-pi-nas-server-datei-server-einrichten-mit-samba>USB-Stick mounten</a> 

<a href=https://shorturl.at/dgsuE>uid und gid ID herausfinden</a> 


---

**8. OpenSource Lizenz**
---

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/ch/88x31.png" /></a><br />Dieses Werk ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/">Creative Commons Namensnennung - Nicht-kommerziell - Weitergabe unter gleichen Bedingungen 3.0 Schweiz Lizenz</a>

 

- - -
