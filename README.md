# ![](https://www.lpice.eu/fileadmin/_processed_/csm_LPIC-DevOpsToolsEngineer_43de3c4735.jpg) myE701 - Exam 701: DevOps Tools Engineer 

Beispiel für einen Aufbau einer Dokumention des Lern- und Entwicklungsprozesses mit Ausgesuchten Unterkapiteln aus dem LPI E701 Exam
## Important Links
* [Module Overview](https://github.com/w901-fr19-mi/W901)
* [DevOps forked instructions](https://github.com/fxshell/E701---DevOps)
* [W901 BSCW](https://bscw.tbz.ch/bscw/bscw.cgi/26211645)
* [Docker in 12 minutes](https://www.youtube.com/watch?v=YFl2mCHdv24)
* [Docker compose in 12 minutes](https://www.youtube.com/watch?v=Qw9zlE3t8Ko)
* [docker-compose explained](https://www.youtube.com/watch?v=HUpIoF_conA)

<details> 
<summary> 
	
### How To: Dokumentation, Install etc. </summary>
	
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
</details>

## Fahrplan

| Datum | behandelte Unterrichtsinhalte: | Gewichtung |
| -------- | ------ | -------- |
| 15.05.19 | Linux Evolution and Popular Operating Systems | 2 |
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

# Dokumention des Lern- und Entwicklungsprozesses
## Kapitel 1: Linux Basics recap (Status: In Arbeit)
[Linux Evolution and popular operating Systems](https://github.com/w901-fr19-mi/E010#11-linux-evolution-and-popular-operating-systems)

**Weight**: 2

**Beschreibung** Linux Überblick: Was ist Linux, was für Distro gibt es, was sind die Unterschiede, wie ist es Aufgebaut?

**Tagesziele** Überblick über das Modul erhalten, [Linux Essentials](https://www.tuxcademy.org/download/de/lxes/lxes-de-manual.pdf) überfliegen und interessante Passagen recherchieren/lösen & sowie gestellte Fragen beantworten
***
### Beispiele und Arbeitsergebnisse

#### Beef zwischen Torvaldis & Tannenbaum
Zu einer Zeit in der Computer schon Fuss gefasst hatten aber es immernoch ständig Änderungen gab beeften sich der Gründer von Linux (Linus Torvaldis) und der Gründer der Distibution Minix (Andrew S. Tanenbaum) öffentlich darüber welche Architektur (Monolithischer Kernel oder Microkernel) besser ist.

Da heute keiner Minix kennt und Linux das grösste Betriebsystem ist, ist die Antwort naheliegend.
***
#### Monolithic Kernel

*This article is an answer from Stackoverflow and only describes monolithic in contect with __operation systems__.*

*[Monolithischer Kernel](https://stackoverflow.com/questions/1806585/why-is-linux-called-a-monolithic-kernel)*
A monolithic kernel is a kernel where all services (file system, VFS, device drivers, etc) as well as core functionality (scheduling, memory allocation, etc.) are a tight knit group sharing the same space. This directly opposes a microkernel.

A microkernel prefers an approach where core functionality is isolated from system services and device drivers (which are basically just system services). For instance, VFS (virtual file system) and block device file systems (i.e. minixfs) are separate processes that run outside of the kernel's space, using IPC to communicate with the kernel, other services and user processes. In short, if it's a module in Linux, it's a service in a microkernel, indicating an isolated process.

Do not confuse the term modular kernel to be anything but monolithic. Some monolithic kernels can be compiled to be modular (e.g Linux), what matters is that the module is inserted to and runs from the same space that handles core functionality (kernel space).

The advantage to a microkernel is that any failed service can be easily restarted, for instance, there is no kernel halt if the root file system throws an abort. This can also be seen as a disadvantage, though, because it can hide pretty critical bugs (or make them seem not-so-critical, because the problem seems to continuously fix itself). It's seen as a big advantage in scenarios where you simply can't conveniently fix something once it has been deployed.

The disadvantage to a microkernel is that asynchronous IPC messaging can become very difficult to debug, especially if fibrils are implemented. Additionally, just tracking down a FS/write issue means examining the user space process, the block device service, VFS service, file system service and (possibly) the PCI service. If you get a blank on that, its time to look at the IPC service. This is often easier in a monolithic kernel. GNU Hurd suffers from these debugging problems (reference). I'm not even going to go into checkpointing when dealing with complex message queues. Microkernels are not for the faint of heart.

The shortest path to a working, stable kernel is the monolithic approach. Either approach can offer a POSIX interface, where the design of the kernel becomes of little interest to someone simply wanting to write code to run on any given design.
![Monolithischer Kernel](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/OS-structure2.svg/1200px-OS-structure2.svg.png "Monolithischer Kernel")


**Fazit und Aussicht** Ich habe schon einiges Über den Aufbau des Linux Kernels gelernt. Die Zeit war aber relativ knapp und ich werde Privat noch Zeit investieren müssen um mehr zu verstehen.

***
## Kapitel: 2 What is all this ?! (Status: In Arbeit)

**Weight**: Personal value

**Beschreibung** Short explaination of ~~all~~ most services used in combination with Kubernetes.

**Tagesziele**, Since I have to read and understand each of the services I can not estimate how long I am going to take for each service. I'll try to do all of them.

**Vorgehen**, Read guides about Docker, keep them as link and conclude the most valuable information as markdown sheet.
***
### Beispiele und Arbeitsergebnisse

#### Ansible

TEXT
TEXT TEXT
**Links:** 
+ [Microservices benefits ands challanges](https://www.cio.com/article/3201193/7-reasons-to-switch-to-microservices-and-5-reasons-you-might-not-succeed.html)
+ second one

**Fazit und Aussicht**, z.B. Die Durcharbeitung von ... gab mir ein besseres Verständnis über die Funktionsweise von Containern.

## Kapitel: 702.1 Container Usage (Status: In Arbeit)

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

## 


* [Exam 701: DevOps Tools Engineer](https://www.lpi.org/our-certifications/exam-701-objectives) 
* [E701 Dokumentation](https://github.com/w901-fr19-mi/E701)
* [myE701 Original Repository](https://github.com/w901-fr19-mi/myE701) 

