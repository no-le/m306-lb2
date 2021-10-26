Werkstattauftrag W06 Pi-NAS
===========================================================================

Inhaltsverzeichnis:
-------------------

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

**4. Installationsanleitung (Didaktisch reduzierte Anleitung. Lernende sollen eine
     eigene Lösungswege realisieren)**

---
  

---

**5. Qualitätskontrolle (Prüfen der Funktionalität mit Ablauf von Kommandos
	und entsprechenden Outputs)**
---	
---

**6. Error-Handling** 
---
- Bei der Installation der Samba-Packete hatten wir das Problem, dass wir zuerst die neusten Updates installieren mussten. Bei der Eingabe des Commands: "Sudo apt-get update" hatten wir das Problem, dass eine Fehlermeldung erschien. In der stand, dass man das Depot mit dem Suite Wert von : "stable" in "oldstable" ändern mussten.
---
**7. Quellen**
---

<a href=https://exerror.com/repository-http-deb-debian-org-debian-buster-updates-inrelease-changed-its-suite-value-from-stable-updates-to-oldstable-updates>Samba Pakete Debugging</a> 
---

**8. OpenSource Lizenz**


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/ch/88x31.png" /></a><br />Dieses Werk ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/ch/">Creative Commons Namensnennung - Nicht-kommerziell - Weitergabe unter gleichen Bedingungen 3.0 Schweiz Lizenz</a>

 

- - -
