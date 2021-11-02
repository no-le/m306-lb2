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
