# Modul 300 LB02

## Eigene Lernumgebung ist eingerichtet

### Persönlicher Wissensstand

#### Containerisierung / Docker

Bis anhin habe ich nur im ÜK mal von Containern gehört, das es sie gibt und eine abgespeckte variante von VM's sind. Mit Container gearbeitet habe ich jedoch noch nie zuvor. Somit ist war mir Docker ebenfalls nicht bekannt.

#### Microservices

Das man Dienste in ganz viel kleine Dienste in verschiedenen Container aufteilt war mir neu. Doch die Idee dahinter finde ich sehr Interessant. Sobald es irgendwo einen Fehler gibt kann man den Fehler gezielt lösen indem man den Container des Mirco Services neu startet.

### Wichtige Lernschritte

Zum Thema Docker war der wichtigste Lernschritt für mich herauszufinden wie Docker aufgebaut ist und wie es funktioniert/ vorgeht. Hierzu habe ich ein kurzes Tutorial geschaut, welches sie uns auf die Lernumgebung gestellt haben. Dies gab mir einen guten Überblick wie Docker arbeitet.

## Bestehende Docker Container kombinieren

### Docker Befehle



| Befehl       | Anwendung                                                    | Beispiel                 |
| ------------ | ------------------------------------------------------------ | ------------------------ |
| docker build | Generiert aus einem Dockerfile ein Image. "-t" ist für das benennen des Image. Der "." steht dafür das das Dockerfile im aktuellen Verzeichnis liegt. | docker build -t sali .   |
| docker run   | Startet aus einem Image ein Container.                       | docker run -p 80:80 sali |
| docker ps    | Zeigt alle Container, aktiv wie auch beendete.               | docker ps -all           |
| docker stop  | Beendet aktiven Container.                                   | docker stop 40b34        |
| docker rm    | Löscht beendeten Container.                                  | docker rm  40b34         |
| docker pull  | Lädt beliebiges Image herunter.                              | docker pull ubuntu:14.04 |
| docker rmi   | Löscht bestimmtes Image.                                     | docker rmi ubuntu:14.04  |
|              |                                                              |                          |



## Sicherheitsaspekte implementieren

