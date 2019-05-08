# Modul 300 LB02

## Eigene Lernumgebung ist eingerichtet (K1 + K2)

### Verwendete Tools

GitHub Desktop

Typora

Docker

VMware Workstation14

Visual Studio Code

SSH Client

### Persönlicher Wissensstand

#### Containerisierung / Docker

Bis anhin habe ich nur im ÜK mal von Containern gehört, das es sie gibt und eine abgespeckte variante von VM's sind. Mit Container gearbeitet habe ich jedoch noch nie zuvor. Somit war mir Docker ebenfalls nicht bekannt.

#### Microservices

Das man Dienste in ganz viel kleine Dienste in verschiedenen Container aufteilt war mir neu. Doch die Idee dahinter finde ich sehr Interessant. Sobald es irgendwo einen Fehler gibt kann man den Fehler gezielt lösen indem man den Container des Mirco Services neu startet.

### Wichtige Lernschritte

Zum Thema Docker war der wichtigste Lernschritt für mich herauszufinden wie Docker aufgebaut ist und wie es funktioniert/ vorgeht. Hierzu habe ich ein kurzes Tutorial geschaut, welches sie uns auf die Lernumgebung gestellt haben. Dies gab mir einen guten Überblick wie Docker arbeitet.

## Bestehende Docker Container kombinieren (K3)

### Docker Projekte:

Ich habe 2 kleinere Docker Projekte erstellt wo ich meine Erfahrungen  gemacht habe.

Erstere ist ein Container mit einem Apache Webserver drauf welcher eine PHP Seite zeigt welche live Aangepasst wird.

Das zweite Projekt besteht aus drei Containern,einem Apache Webserver, einer PHP Applikation und einer MySQL Datenbank welche miteinander Kommunizieren. Der Webserver nimmt die anfrage entgegen und gibt sie an die PHP Applikation weiter. Diese überprüft dann ob die Verbindung zur Datenbank funktioniert und gibt das Resultat an den Webserver zurück.  Somit zeigt die Webseite an ob die Connection zwischen den Containern vorhanden ist oder nicht.



### Netzwerkplan:

![Netzwerkplan_LB02](C:\Users\sppm0061\Module\Modul 300\LB02\Netzwerkplan_LB02.png)



### Volumens zur persistenten Datenablage

#### Statisch

Ich erstelle im Dockerfile eine persistente Datenablage um Dateien in meine Computer rein zu kopieren. Dies mach ich indem ich neben meinem Dockerfile ein Ordner erstelle welchen ich src/ nenne. Hier hinterlege ich nun alle Dateien die ich später im Container verwende. Die Ablage muss ich nur noch im Dockerfile festlegen dies mache ich mit folgendem Befehl:

```
COPY src/ /var/www/html
```

COPY: Kopiert den Inhalt des Ordners welcher sich auf meinem Host befindet (src/), in den Ordner in meinem Container (/var/www/html).

#### Live

Allenfalls kann dieses Verzeichnis fortlaufend Live abgerufen werden was z. B. bei einer Webseite sehr nützlich sein kann . Durch dies können Änderungen einer Webseite gleich angesehen werden ohne das der Container neu gestartet werden muss. Hierzu muss jedoch das Verzeichnis welches überprüft werden soll beim "docker run" Befehl angegeben werden.

```
docker run -p 80:80 -v /home/sigi/Desktop/Docker/src/:/var/www/html/ siggy2
```



### Docker Befehle

| Befehl                                | Anwendung                                                    | Beispiel                    |
| ------------------------------------- | ------------------------------------------------------------ | --------------------------- |
| docker build                          | Generiert aus einem Dockerfile ein Image. "-t" ist für das benennen des Image. Der "." steht dafür das das Dockerfile im aktuellen Verzeichnis liegt. | docker build -t sali .      |
| docker run                            | Startet aus einem Image ein Container.                       | docker run -p 80:80 sali    |
| docker ps                             | Zeigt alle Container, aktiv wie auch beendete.               | docker ps -all              |
| docker stop                           | Beendet aktiven Container.                                   | docker stop 40b34           |
| docker rm                             | Löscht beendeten Container.                                  | docker rm  40b34            |
| docker pull                           | Lädt beliebiges Image herunter.                              | docker pull ubuntu:14.04    |
| docker rmi                            | Löscht bestimmtes Image.                                     | docker rmi siggy            |
| docker exec -i -t container_name bash | Shell in einem Container öffnen.                             | docker exec -i -t x345 bash |



## Sicherheitsaspekte implementieren (K4)

### Aspekte der Container Absicherung

#### Festgelegter Port

Zur Absicherung habe ich einen spezifischen Port festgelegt auf den die Container hört. Dies habe ich mit folgendem Befehl gemacht:

```
EXPOSE 80
```

Dieser Container hört nun auf den Port 80.

#### Backup

Zur Guten Absicherung eines Container gehört z. B. auch das Backupen von einem Datenbank Container, welcher möglicherweise auch wichtige Daten beinhalten kann. Hierzu können Snapshots gezogen werden oder auch Full Backups gemacht werden.

#### Ressourcen einschränken

##### Memory einschränken

Die Memory Ressourcen der VM habe ich eingeschränkt das diese nicht mehr beziehen kann als sie sollte. Dies lässt sich beim "docker run" Befehl ergänzen.

```
docker run --memory="1g"
```



##### CPU einschränken

Die CPU Ressourcen der VM habe ich eingeschränkt das diese nicht mehr beziehen kann als sie sollte. Dies lässt sich beim "docker run" Befehl ergänzen.

```
docker run --cpus="1.5
```



#### Trennung der einzelnen Services

Durch das Trennen der einzelnen Services werden diese nicht voneinander beeinflusst und so Crasht zum Beispiel nur ein teil der Applikation und nicht das ganze System. Somit habe ich in meinem Projekt den Webserver, den PHP Server und die Datenbank voneinander getrennt.

### Sicherheitsmassnahmen sind Dokumentiert

In meiner Umgebung ist ein bestimmter Port festgelegt. (Port 80)

Ausserdem wurden alle Services voneinander getrennt, wodurch diese sich nicht gegenseitig beeinflussen können.

Das kleinere Projekt kann ich ausserdem auch mit eingeschränkten Ressourcen starten.

## Zusätzliche Bewertungspunkte (K5)

### Vergleich Vorwissen - Wissenszuwachs

#### Containerisierung / Docker

Da mein Vorwissen zu Containern praktisch nicht vorhanden war, habe ich in diesem Punkt riesigen Wissenszuwachs bekommen. Ich konnte mal eine andere frische Seite sehen von "virtuellen Maschinen" wo man nicht ständig das OS aufsetzten muss und dies auch noch Ressourcen benötigt. Um grosse Projekte / Netzwerke zu realisieren ist dies sicher eine der besten Lösungen, welche mir nun nicht mehr ganz so fremd ist.

#### Microservice

Da mein Vorwissen zu Microservices und deren praktischen Einsetzung nicht vorhanden war, habe ich in diesem Punkt riesigen Wissenszuwachs bekommen. Ich habe mir einige gross Projekte angeschaut wie man Docker z. B als ein Exchange Ersatz einsetzten kann, was ich ziemlich beeindruckend fand. Leider waren diese Projekte etwas zu gross und zu komplex mit meinem Docker wissen um dies in diesem Modul umzusetzen. Trotzdem habe ich viel dazu gelernt und fand es spannend mal etwas neues zu sehen wie man alle Services voneinander abtrennt um Fehler zu vermeiden.

### Reflexion

Ich hatte einige spezielle Probleme mit Docker, da ich Docker nicht  auf meinem Windows Computer einrichten konnte. Schlussendlich habe ich alles auf einer Ubuntu VM gemacht, welche auch einige Probleme mit sich brachte da ich kein Linux Experte bin und ich normalerweise auf Windows arbeite. Somit hatte ich plötzlich Berechtigungsprobleme welche sonst keiner meiner Mitschüler hatte.  Auch einfache Tutorials wurden so für mich zur Herausforderung. Schlussendlich konnte ich trotz meinen Problemen, doch zwei kleinere Umgebungen erschaffen, welche funktionierten. Fazit für mich ist das die Idee hinter Docker zwar enorm gut ist, ich jedoch Vagrant bevorzugen würde da ich dies auf meinem Windows Notebook ohne Probleme managen konnte.

## zusätzliche systemtechnische Bewertungspunkte (K6)

### Continuous Integration

Ich habe in meinem ersten Docker Projekt, realisiert das Änderungen am PHP File für meinen Webserver gleich übernommen werden und somit die Seite immer top aktuell ist.  