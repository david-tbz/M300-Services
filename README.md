# M300-Services
Modul 300: Plattformübergreifende Dienste in ein Netzwerk integrieren

## Inhaltsverzeichnis
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [M300-Services](#m300-services)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- LB2
- [K1](#k1)
  - [VirtualBox](#virtualbox)
    - [VM manuell erstellen](#vm-manuell-erstellen)
    - [Apache Server installieren](#apache-server-installieren)
  - [Vagrant](#vagrant)
  - [SSH-Key](#ssh-key)
  - [Git-Client](#git-client)
  - [VS-Code](#VS-Code)
- [K2](#k2)
  - [GitHub Account](#github-account)
- [K3](#k3)
  - [Testen](#testen)
    - [Apache](#apache)
    - [Users and Groups](#users-and-groups)
- [K4](#k4)
  - [Firewall](#firewall)
  - [Reverse-Proxy](#reverse-proxy)
- [K5](#k5)
  - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
  
- LB3
- [K1](#k1)
  - [VirtualBox](#virtualbox)
    - [VM manuell erstellen](#vm-manuell-erstellen)
    - [Apache Server installieren](#apache-server-installieren)
  - [Vagrant](#vagrant)
  - [SSH-Key](#ssh-key)
  - [Git-Client](#git-client)
- [K2](#k2)
  - [GitHub Account](#github-account)
- [K3](#k3)
  - [Testen](#testen)
    - [Apache](#apache)
    - [Users and Groups](#users-and-groups)
- [K4](#k4)
  - [Firewall](#firewall)
  - [Reverse-Proxy](#reverse-proxy)
- [K5](#k5)
  - [Vergleich Vorwissen - Wissenszuwachs](#vergleich-vorwissen---wissenszuwachs)
_

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
4. Danach habe ich im Webbrowser geprüft, ob der Standard-Content des Webservers unter "http://127.0.0.01:3001" (localhost) erreichbar ist.
 ```Shell
 $ config.vm.network "forwarded_port", guest:80, host:3001, auto_correct: true # Hier wird der Zugriff auf Port 80 auf 3001 weitergeleitet
 ```
5. Später habe ich im Ordner `var/www/html`die Index-Datei abgeändert und das Resultat überprüft.
   
6. Abschliessend habe ich die VM wieder gelöscht:
    ```Shell
      $ vagrant destroy -f
    ```
## SSH-Key 
> [⇧ *Nach oben*](#inhaltsverzeichnis)

*Zuerst musste ich Lokal einen SSH-Key erstellen:*

1.  Folgenden Befehl mit der Account-E-Mail von GitHub in Bash einfügen:
    ```Shell
      $  ssh-keygen -t rsa -b 4096 -C "david.jeremic@edu.tbz.ch"
    ```
2. Neuer SSH-Key wird erstellt:
    ```Shell
      Generating public/private rsa key pair.
    ```
3. Bei der Abfrage, unter welchem Namen der Schlüssel gespeichert werden soll, die Enter-Taste drücken (für Standard):
    ```Shell
      Enter a file in which to save the key (~/.ssh/id_rsa): [Press enter]
    ```
4. Nun habe ich ein Passwort für den Key festgelegt:
    ```Shell
      Enter passphrase (empty for no passphrase): ********
      Enter same passphrase again: ********* # Dieses Passwort wurde beim erstellen vom Lokalen Repository und beim Pull abgefragt
    ```
*Danach kann ich den SSH-Key dem Client hinzufügen:*
1. Auf www.github.com im Benutzerkonto *Settings* aufrufen
2.  Unter den Menübereichen auf der linken Seite zum Abschnitt *SSH und GPG keys* wechseln
3.  Auf *New SSH key* klicken
4.  Im Formular unter *Title* die Bezeichnung MB SSH-Key vergeben
5.  Den Key von der Datei *C:\Users\David Jeremic\.ssh\id_rsa.pub* einfügen und auf *Add SSH key* klicken

*SSH Zugriff auf VM*

Um Zugriff via SSH auf die VM aufzubauen, muss man bloss einen kurzen Befehl eingeben.
```shell
vagrant ssh
```

## Git-Client

Damit ich vom Lokalen PC arbeiten kann, musste ich den sogenannten "Git Client", auf Windows "Git/Bash" installieren. 

*Client installieren*
Ich habe Client-Installation auf [dieser](https://git-scm.com/downloads) Seite heruntergeladen und GUI-basiert installiert.


*Danach habe ich den Client konfiguriert:*
1. Terminal öffnen --> Nach der Installation automatisch gestartet
2. Git konfigurieren mit Informationen des GitHub-Accounts: --> Erst nach dem ein Account erstellt worden ist (siehe K2)
    ```Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
    ``` 

*Damit ich das readme-File lokal bearbeiten kann, habe ich das Repository heruntergeladen und aktualisiert.*

1. Terminal öffnen
2. Ordner für Repository erstellen:
    ```Shell
      $ cd /c/Users/David Jeremic/Documents/M300
      $ mkdir MeinLokalesRepository
     ```
3. Repository mit SSH klonen:
    ```Shell
      $ git clone git@github.com:david-tbz/M300-Services.git

      Cloning into 'M300-Services'...
    ``` 
4. Repository aktualisieren und Status anzeigen:
    ```Shell
      $ cd M300-Services
      $ git pull # Da ich denn SSH Key schon hinzugefügt habe, musste ich noch das Passwort angeben

      Already up to date.
    ```
## VS-Code

Visual Studio Code habe ich wie in der ANleitung konfiguriert. Da ich das settings.json file nicht finden konnte. Habe ich die Änderungen manuell in den Settings eingegeben. Nachdem konnte ich erfolgreich das Readme.md file bearbeiten.
K2
======
## GitHub Account

*Ich habe folgendermassen einen Github Account erstellt:*
1. Die Seite [GitHub.com](https://github.com) öffnen
2. Auf *Sign up* drücken
3. Username, E-mail und Passwort eingeben sowie Aufgabe zum verifizieren lösen
4. Auf *Create an Account* drücken
5. Die Aktivierungsmail bestätigen

## Persönlicher Wissensstand

### Containerisierung

Die Containerisierung erlaubt einzelne Bestandteile einer Applikation in "Containern" zu arbeiten. Dies erhöht die Flexibilität einer Applikation. Es können mehrere Container laufen. Der Vorteil ist, dass die Container sehr wenig Platz brauchen, da sie nicht ein Betriebssystem brauchen und sich die Infrastruktur mit dem Kernel teilen.

Ein anderer Vorteil ist, dass ein bestehendes Dockerfile auf jedem System gleich arbeiten wird und man so viel Zeit und Geld sparen kann. Der Nachteil ist, das man mehr Kenntnisse braucht.

### Docker

Docker ist eine Software die Containerisierung anbietet. Docker verwendet Docker-Images um Docker-Container zu starten.
Die Firma Docker nam sich als Basis für ihre Arbeiten die bestehende Linux-Containertechnologie und erweiterte sie, damit sie eine vollständige und Produktionsfähige Lösung haben.

|Docker-Komponent|Bedeutung|
|:--------------:|:-------:|
|Registry        | darin werden Images abgelegt und verteilt        |
|Docker Deamon   | Erstellen, ausführen und Überwachen von Container|
|Docker Client   | Steuert Container via Shell |
|Images          | Gebuildete Umgebung, Ausführbar als Contiainer |
|Container       | Ausgeführte Images |
 
### Microservices

Microservices sind kleine unabhängige Services, die eine Aufgabe erledigen. Sie sind leicht ersetzbar.

### Im Betrieb

Ich habe diese Woche im Betrieb nachgefragt, ob wir Containerisierung verwenden. Da wir eine grosse Firma sind, habe ich schon vermutet, dass wir diese Technologie auch verwenden. Wie erwartet verwendet mein Betrieb auch Containerisierung, jedoch nur mit wenigen Applikationen. Ich persönlich war noch nicht in Kontakt mit Containern in meiner Firma.

 K3
======
 
## Testen

### Apache

Um zu testen ob Apache richtig installiert wurde, habe ich die Website mit http://127.0.0.1:3001 aufgerufen. Nachdem habe ich noch die Index-Datei geändert und nochmal getestet.

### Users and Groups
- Mit diesem Befehl habe ich alle Benutzer in der VM angezeigt und habe dann gesehen, das meine beiden User erstellt worden sind.
   ```Shell
   $ cut -d: -f1 /etc/passwd
   ```
    
- Mit diesem Befehl zeige ich die Gruppen in der VM an und sehe dann, ob die neue Group erstellt wurde.
   ```Shell
    $ cut -d: -f1 /etc/group
    ```
-  Die beiden Befehle oben kann man in einen zusammenfassen, indem man den User mit der dazugehörigen Group anzeigt:
    ```Shell
    cut -d: -f1 /etc/passwd | xargs groups
    ```

- Um zu testen, ob das Passwort geändert wurde, habe ich mich mit einem zuvor erstellten User eingeloggt.
    Shell
    su user01
    password: ****

### Ports
- Mit diesem Befehl habe ich kontrolliert, ob die Ports offen sind.
   ``` Shell
   $ netstat -an |grep LISTEN 
   ```

K4
======

In diesem Punkt geht es um die Sicherheit. Im Vagrantfile kann man die Befehle unter der Konfiguration der VM einfügen.
Diese werden dann beim Aufsetzen der VM automatisch ausgeführt. Das hat den Vorteil, dass man somit identische VM's erstellen kann, da jede Prozedur die exakt gleiche ist.

## Firewall

  *Ich habe beim aufsetzen automatisch Firewall Regeln erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    ````Shell
      sudo apt-get install ufw
      sudo ufw allow 80/tcp
      sudo ufw allow 22/tcp 
      sudo ufw allow out 22/tcp 
      sudo ufw enable
     ```
     
 Dazu findet man unter [diesem Link](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-18-04)
weitere Möglichkeiten zum Einstellen.

## Reverse-Proxy
*Ich habe beim aufsetzen automatisch einen Reverse-Proxy installiert, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*
1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    ```Shell
    sudo apt-get -y install libapache2-mod-proxy-html
    sudo apt-get -y install libxml2-dev

    sudo a2enmod proxy
    sudo a2enmod proxy_html #Mit diesem Befehl aktiviert man den Proxy
    sudo a2enmod proxy_http #Mit diesem Befehl aktiviert man den Proxy
   ```  

## Benutzer und Rechtevergabe

*Ich habe beim aufsetzen automatisch User mit Passwort erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    ```Shell
      sudo groupadd testtest
      sudo useradd testuser1 -g testtest -m -s /bin/bash 
      sudo useradd testuser2 -g testtest -m -s /bin/bash 
      sudo chpasswd <<<testuser1:abcd1234	
      sudo chpasswd <<<testuser2:abcd1234
    ```
    
## SSH

*Ich habe beim aufsetzen automatisch ein SSH Zugang erstellt, indem ich die nötigen Zeilen ins Vagrantfile eingefügt habe:*

1. Vagrantfile öffnen
2. Folgende Zeilen einfügen:
    ```Shell
      sudo apt-get -y install openssh-server
   ``` 

K5
======

## Vergleich Vorwissen - Wissenszuwachs

*Bereits bekannt*

- Virtualisierung mit VIrtualisierungssoftware wie zum Beispiel VirtualBox kannte ich schon von vorherigen Modulen und Ük's. 
- Github war mir schon bekannt, jedoch verwendete ich es nie wirklich

*Dazugelernt*

- Ich habe gelernt wie man mit Vagrant schnell und einfach neue identische Maschinen ersellen kann.
- Ich habe ausserdem noch gelernt, wie man Github selber verwendet und wie man aud verschiedene Arten Inhalt bearbeiten kann.

*Schlussfolgerung*

Ich habe in dieser LB wirklich viel neues gelernt. Mir hat das ausprobieren mit Vagrant auch Spass gemacht zudem ist es auch nützlich. Die Methode mit Vagrant VM's zu ersellen war mir bis vor kurzem unbekannt, da wir im Geschäft mit vSphere arbeiten. 

Reflexion

Diese Arbeit war sehr interessant und es machte Spass an dem zu arbeiten. Ich kamm am Anfang nicht so gut voran, dies konnte ich aber schnell lösen indem ich mit den anderen Lehrlingen sprach. Ich kamm ab dann gut voran und konnte schnell lernen. Manchmal bekamm ich anderen Output als in den Beispielen ersichtlich, jedoch konnte ich mit ein wenig logisch denken konnte ich die Unterschiede leicht erklären. Ich freue mich die Arbeit mit LB3 weiterzuführen.


LB3
======

## K3
Ich habe Docker auf einer Ubuntu VM installiert. Ich habe folgende Schritte beachtet
    ```Shell
      curl -fsSL https://get.docker.com -o get-docker.sh
      sudo sh get-docker.sh
    ```
Nachdem konnte ich mit diesem Befehl Docker testen:
 ```Shell
      docker run hello-world
 ```
 Damit ich mehrere Dienste verknüpfen kann, wie z.B. Wordpress mit der DB instllierte ich noch docker-compose mit diesem Befehl.
 
 ```Shell
 sudo apt-get install docker-compose
```

Als ich das erledigt habe, erstellte ich mir auf dem Schreibtisch einen Folder namens Wordpress und in diesem Folder ein Compose-File.yaml

```Shell

sudo nano composefile.yaml
version: '3'

services:
  # Database
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - wpsite
  # phpmyadmin
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - '8080:80'
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: password 
    networks:
      - wpsite
  # Wordpress
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - '8000:80'
    restart: always
    volumes: ['./:/var/www/html']
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    networks:
      - wpsite
networks:
  wpsite:
volumes:
  db_data:
  
```
Um die Container zu starten gibt man den Befehl ein:

```Shell

docker-compose up -d
```

Nachdem sollte unter localhost:8000 die Wordpress seite angezeigt werden und auf localhost:8080 die Php-Seite.


## Wichtige Befehle:

### Docker-Befehle
- Zum Starten von neues Contianer: `docker run`    
- Überblick über die aktuellen Container: `docker ps`
- Liste der lokalen Images: `docker images`       
- Entfernen von Container: `docker rm`         
- Löschen von angegebenen Images: `docker rmi`     
- Starten von gestoppten Container: `docker start`       
- Container Stoppen: `docker stop`     
- Logs von Container ausgeben: `docker logs`
- Informationen zum lafuenden Prozessen in einem angegebenen Container: `docker top`

### Befehle in einem Docker-file
Dockerfile ist eine Textdatei, die genutzt wird, um ein Docker-image zu erstellen.   
Hier sind wichtige Anweisungen im Dockerfile:
- Welches Base-Image von [hub.docker.com](hub.docker.com): `FROM` 
- Kopiert Dateien aus dem Build Context oder URL: `ADD`
- Führt Anweisung aus, wenn Contianer gestartet wurde: `CMD`
- Dateien aus Build Context in das Images zu kopieren: `COPY`
- Legt eine ausführbare Datei fest, die beim Start des Containers laufen soll: `ENTRYPOINT`
- Umgebundvariabeln im Image: `ENV`
- Erklärt Docker, dass der Container einen Prozess enthlt, der an dem oder den angegebenen Ports lauscht: `EXPOSE`
- Docker Engine chekt regelmässig den Status der Anwendung im Container: `HEALTHCHECK`
- Führt Anweisung im Container aus und bestätigt Ergebnis: `RUN`
- Ermöglicht es direkt bash oder PS Befehle zu nutzten: `SHELL`
- Setzt den Benutzer der in `RUN, CMD, oder ENTRYPOINT` genutzt werden soll: `USER`
- Daklariert angegebene Datei oder Varzechnis als Volume: `VOLUME`
- Arbeitsverzeichnis für `RUN, CMD, ENTRYPOINT, ADD oder COPY` Anweisungen: `WORKDIR


K5
=====

ICh habe in diesem Modul sehr viel gelernt. DIe arbeit mit Docker hat spass gemacht. Ich habe gemerkt, dass ich in alten Modulen mit dieser Technologie sehr viel Zeit sparen könnte. Alles was ich gelernt habe ist neu für mich.
