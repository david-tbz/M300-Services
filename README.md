# M300-Services
Modul 300: Plattformübergreifende Dienste in ein Netzwerk integrieren


K1
======

## VirtualBox

Als erstes habe ich die Toolumgebung installiert. Für die Basis verwendete ich VirtualBox. Dies ist auch für die nächsten Schritte wichtig.

1. Ich habe VirtualBox schon installiert gehabt. Also habe ich auf [dieser Webseite](https://www.virtualbox.org) die neuste Version von VirtualBox heruntergeladen und GUI basiert installiert.
2. Damit man eine VM erstellen kann, braucht man eine ISO-Datei. In meinem Fall die ISO-Datei von Ubuntu. Ich hatte schon eine neue ISO-Datei vom letzten Modul. Falls das nicht der Fall wäre könnte man auf [dieser Webseite](https://www.ubuntu.com/#download) eine herunterladen.

### VM manuell erstellen

1. VirtualBox öffnen
2. Auf "Neu" drücken und denn Prozess für eine Neue VM starten
3. Als nächstes muss man folgende Attribute angeben:
   *  Name:           `M300_Ubuntu`
   *  Typ:            `Linux` --> Wird automatisch erkannt
   *  Version:        `Ubuntu (64-bit)` --> Wird automatisch erkannt
   *  Speichergrösse: `2048 MB`
   *  Platte:         `[X] Festplatte erzeugen`
4. Nun auf `Erzeugen` klicken
5. Im nächsten Fenster, folgende Informationen eintragen: --> Hier verliert man viel Zeit
   *  Dateipfad:                       `Standard`
   *  Dateigrösse:                     `10.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
6. Nun erneut auf `Erzeugen` klicken, dann im Hauptmenü die VM anwählen (blau markiert) und den Punkt `Ändern` aufrufen
7. Im Abschnitt `Massenspeicher` den SATA-Controller anwählen und auf das CD+Symbol klicken
8. Unter `Medium auswählen` das zuvor heruntergeladene Systemabbild (ISO-Datei) anwählen
9. Alle Änderungen speichern und die VM starten
10. Nun den Installationsanweisungen der OS-Installation folgen. --> Dauert wieder eine lange Zeit

### Apache Server installieren

1. Paketliste neu einlesen und Pakete aktualisieren:
   ```Shell 
   $  sudo apt-get update   #Paketlisten des Paketmanagement-Systems "APT" neu einlesen
   
   $  sudo apt-get update   #Installierte Pakete wenn möglich auf verbesserte Versionen aktualisieren

   $  sudo reboot           #System-Neustart durchführen
   ```
2. Apache Server installieren
  ```Shell 
   $ sudo apt-get install apache2 # Apache2 Webserver installieren
   
   $ sudo reboot #System-Neustart durchführen
  ```
3. Als nächstes habe ich überprüft, ob die Standard-Seite von Apache unter "http://127.0.0.01:80" ersichtlich ist. 
  
## Vagrant

Vagrant ist eine Möglichkeit voreingestellte VMs automatisch zu erstellen. Dazu sind mehrere Sachen Notwendig um es auf einem Windows-System laufen zu lassen. Als erstes braucht man Vagrant, dies kann man auf [dieser Webseite](https://www.vagrantup.com/ "vagrantup.com") herunterladen. Dann braucht man noch VirtualBox um die VM in diesem Programm laufen zu lassen und noch ein Terminal für Windows, in meinem Fall Git/Bash.

1. Vagrant herunterladen und GUi-Basiert installieren.
2. Terminal öffnen (Git/bash)
3. Einen Ordner für die VM erstellen:
    ```Shell
      $ cd /c/Users/David Jeremic/Desktop/M300 # In das gewünschte Verzeichnis wechseln
      $ mkdir myserver # Ordner erstellen
      $ cd myserver # in den Ordner wechseln
    ``` 
 4. VM erstellen und starten
     ```Shell
      $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
      $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
    ``` 
    Nun ist die VM gestartet. Dies kann man in VirtualBox überprüfen, indem man einfach in der Seitenleiste schaut ob dort eine VM erstellt worden ist.
 5. Nun kann man sich mit ssh auf die VM verbinden
     ```Shell
      $ vagrant ssh                       #SSH-Verbindung zur VM aufbauen
     ```
     Voraussetzung ist, dass man im richtigen Verzeichnis ist.
     
 Dies ist eine leere Virtuelle Maschine. Man kann die Vagrantfiles bearbeiten und Bash-Kommandos in die Files hinzufügen. So kann man zum Beispiel einen Apache Server direkt mit installieren oder auch direkt Firewall-Rules erstellen.
 
 1. Terminal öffnen
 2. Zum Verzeichnis mit dem bearbeiteten File wechseln.
     ```Shell
     $ cd /c/Users/David Jeremic/Desktop/M300/myserver2
     ```
 3. VM erstellen und aufstarten
    ```Shell
      $ vagrant up
    ``` 
4. Danach habe ich im Webbrowser geprüft, ob der Standard-Content des Webservers unter "http://127.0.0.01:8080" (localhost) erreichbar ist.
 ```Shell
 $ config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true # Hier wird der Zugriff auf Port 80 auf 8080 weitergeleitet
 ```
5. Später habe ich im Ordner `var/www/html`die Index-Datei abgeändert und das Resultat überprüft.
   
6. Abschliessend habe ich die VM wieder gelöscht:
    ```Shell
      $ vagrant destroy -f
    ```   
 
 
