# ![](https://www.lpice.eu/fileadmin/_processed_/csm_LPIC-DevOpsToolsEngineer_43de3c4735.jpg) myE701 - Exam 701: DevOps Tools Engineer 

Beispiel für einen Aufbau einer Dokumention des Lern- und Entwicklungsprozesses mit Ausgesuchten Unterkapiteln aus dem LPI E701 Exam

## Einrichtung forken dieses GitHub Repository für Dokumentation (Kapitel kann in der Kopie gelöscht werden)

Als erster Schritt muss ein GitHub-Account eingerichtet werden. Dieser dient uns später als "Cloud-Speicher" unserer Dokumentation und weiteren Dateien.

Folgende Arbeiten müssen gemacht werden:

**Account erstellen**

1. Auf www.github.com ein Benutzerkonto erstellen (Angabe von Username, E-Mail und Passwort)
2. E-Mail zur Verifizierung des Kontos bestätigen und anschliessend auf GitHub anmelden

**Forken dieses Repositories**

1. Auf Repository [myE701](https://github.com/w901-fr19-mi/myE701) wechseln.
2. Klicken Sie oben rechts auf der Seite auf `Fork` .

![](https://help.github.com/assets/images/help/repository/fork_button.jpg)

Das ist es! Jetzt haben Sie einen `Fork` (Kopie) des Original myE010 Repository und können dessen Inhalte verändern.

Weitere Möglichkeiten siehe [Modul M300 - 10 Toolumgebung](https://github.com/mc-b/M300/tree/master/10-Toolumgebung)

## Dokumentation (Kapitel kann in der Kopie gelöscht werden)

Die Dokumentation erfolgt im Markdownformat, dem Standard Wiki Format von github. Dies geht am Einfachsten direkt auf github.com.

Eine Markdown Übersicht / Syntax etc. finden Sie auf:
* [Markdown Syntax inkl. Online Demo](http://markdown-syntax.de/Was-ist-Markdown/)
* [Dokumentation aus dem Modul M300](https://github.com/mc-b/M300/blob/master/80-Ergaenzungen/vcs/03-Markdown.md) 

## Installation (Kapitel kann in der Kopie gelöscht werden)

Hier lohnt es sich Vagrant zu verwenden. Damit kann gleichzeitig eine VM (Ubuntu 16.x) mit Docker und Kubernetes aufgesetzt werden oder mittels des Projektes [lernkube](https://github.com/mc-b/lernkube) ein Kubernetes Master. 

**Vagrant (lernkube) Installation**

Zuerst muss folgende SW Installiert werden:
* [Git/Bash](https://git-scm.com/downloads)
* [Vagrant](https://www.vagrantup.com/) 
* [VirtualBox](https://www.virtualbox.org/)

Wechseln Sie auf die Kommandozeile (*bash* oder *PowerShell*) und klonen des Projekt `lernkube` und erstellen die VM(s):

	git clone https://github.com/mc-b/lernkube
	cd lernkube
	cp templates/DUK.yaml config.yaml
	vagrant plugin install vagrant-disksize
	vagrant up

Während der Installation werden im Verzeichnis `lernkube` mehrere `.bat` Dateien und die Client Programme `docker`, `kubectl`, `helm` etc. erzeugt.

Die Bezeichnungen deren Funktion kann mittels `kubeps.bat` (*PowerShell*) oder `source kubeenv` (*Bash*) angezeigt werden. Die Scripts setzen gleichzeitig die Umgebungsvariablen, damit vom Notebook Docker und Kubernetes (`kubectl`) an die VM weitergereicht werden können.

Beispiele:

	docker images # zeigt alle Container Images an
	kubectl get all # zeigt alle Kubernetes Ressourcen an.
	
**Alternative Installationen** 

Alternativ kann [Docker for Windows/Mac](https://www.docker.com/products/docker-desktop) oder [Minikube](https://github.com/kubernetes/minikube) verwendet werden. Diese Umgebungen sind aber nicht Cluster fähig und erfordern [Feintuning](https://github.com/mc-b/lernkube/tree/master/docker4windows/).

Oder die gleiche Umgebung wie mit lernkube auf den Cloud Plattformen von Amazon und Microsoft eingerichtet werden.

* [Amazon AWS Cloud](https://github.com/mc-b/lernkube/tree/master/aws/) - hat noch Probleme mit Datenspeicherung und LoadBalancer.
* [Microsoft Azure Cloud](https://github.com/mc-b/lernkube/tree/master/azure/)	 

**Weitere nützliche Programme**

* [Windows SSH Client, putty](https://putty.org)
* [Grafischer Windows SFTP Client, Bitvise SSH Client](https://www.bitvise.com/ssh-client-download)
* [Visual Studio Code](https://code.visualstudio.com/)

## Fahrplan
***


| Datum | behandelte Unterrichtsinhalte: | Gewichtung |
| -------- | ------ | -------- |
| 15.05.19 | Installation SW, Einrichten Linux VM<br>1.1 Linux Evolution and Popular Operating Systems<br>1.3 Open Source Software and Licensing | 2 + 2 |
| 15.05.19 | Installation SW, Einrichten Linux VM(s)<br>[701.1 Modern Software Development, 1. Teil](https://github.com/w901-fr19-mi/E701#7011-modern-software-development) | 6 |
| 22.05.19 | [701.1 Modern Software Development, 2. Teil](https://github.com/w901-fr19-mi/E701#7011-modern-software-development) | 4 |
| 29.05.19 | [701.3 Source Code Management](https://github.com/w901-fr19-mi/E701#7013-source-code-management) | 5 | 
| 05.06.19 | 702.1 Container Usage, 1. Teil | 7 |
| 12.06.19 | 702.1 Container Usage, 2. Teil | (7) |
| 19.06.19 | 702.2 Container Deployment and Orchestration | 5 |
| 26.06.19 | LB1 Theoretische Prüfung und Abschluss LB2 | - |
| 03.07.19 | Sommersporttage | - |
|          | Total Punkte | 27 (34) !

Kapitel aus E701 wurden in der Gruppe mit .... erarbeitet. Davon sind mindestens 14 Punkte selbständig erarbeitet worden. 

## Dokumention des Lern- und Entwicklungsprozesses
***

### Kapitel: 702.1 Container Usage (Status: In Arbeit)

**Weight**: 7 (7)

**Beschreibung** Gegenüberstellung welche Linux Technologien für Container verwendet werden.

**Tagesziele**, z.B. Erstellung einer Tabelle Linux - Container. 

**Vorgehen**, z.B. Studieren Background Linux Namespaces vs. Container, UnionFS vs. Container Layer, Unix Prozesse (Jobs) vs. Docker run/start/stop

**Beispiele und Arbeitsergebnisse**

| Linux          | Container      | Beschreibung      |
| -------------- | -------------- | ----------------- |
| Namespaces     | laufender Container | beim Starten des Containers wird in eine andere Linux Namespace gewechselt |
| UnionFS        | Image Layer         | Container Verwenden UnionFileSysteme um .... |
| Unix Prozesse  | run/start/stop      | docker run/start/stop Befehle ähneln dem .... Subsystem |

**Fazit und Aussicht**, z.B. Die Durcharbeitung von ... gab mir ein besseres Verständnis über die Funktionsweise von Containern.

## Links

* [Exam 701: DevOps Tools Engineer](https://www.lpi.org/our-certifications/exam-701-objectives) 
* [E701 Dokumentation](https://github.com/w901-fr19-mi/E701)
* [myE701 Original Repository](https://github.com/w901-fr19-mi/myE701) 

