# myE701 - Exam 701: DevOps Tools Engineer 

Beispiel für einen Aufbau einer Dokumention des Lern- und Entwicklungsprozesses mit Ausgesuchten Unterkapiteln aus dem LPI E701 Exam
## Important Links
* [Module Overview](https://github.com/w901-fr19-mi/W901)
* [DevOps forked instructions](https://github.com/fxshell/E701---DevOps)
* [W901 BSCW](https://bscw.tbz.ch/bscw/bscw.cgi/26211645)
* [Docker in 12 minutes](https://www.youtube.com/watch?v=YFl2mCHdv24)
* [Docker compose in 12 minutes](https://www.youtube.com/watch?v=Qw9zlE3t8Ko)
* [docker-compose explained](https://www.youtube.com/watch?v=HUpIoF_conA)

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



# Dokumention des Lern- und Entwicklungsprozesses
<details>
<summary> Kapitel 1: Linux Basics recap (Status: In Arbeit)
[Linux Evolution and popular operating Systems](https://github.com/w901-fr19-mi/E010#11-linux-evolution-and-popular-operating-systems) </summary>

**Weight**: 2

**Beschreibung** Linux Überblick: Was ist Linux, was für Distro gibt es, was sind die Unterschiede, wie ist es Aufgebaut?

**Tagesziele** Überblick über das Modul erhalten, [Linux Essentials](https://www.tuxcademy.org/download/de/lxes/lxes-de-manual.pdf) überfliegen und interessante Passagen recherchieren/lösen & sowie gestellte Fragen beantworten

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

# Kapitel: 701.1 Modern Software Development (Status: Abgeschlossen)

**Weight**: 6 + 4 Bonsupunkte für die Erstellung eines Microservices inkl Unit-Tests.

**Beschreibung**, Gegenüberstellung wie ein Microservice ... handhabt:
* Data persistence
* Sessions
* Status information
* Transactions
* Concurrency
* Security
* Performance
* Availablility
* Scaling
* Load balancing
* Messaging
* Monitoring
* APIs

**Tagesziele**, Aufstellung der oben genannten Stichworte. 

**Vorgehen**, Informationen über die oben gennanten Stichworte sammeln, den bezug zu Microservices herausfinden und schlussendlich in einer Aufstellung beschreiben.

**Beispiele und Arbeitsergebnisse**

## Data persistence
### Database Per Service
In diesem Muster verwaltet jeder Mikrodienst seine eigenen Daten. Dies impliziert, dass kein anderer Mikrodienst direkt auf diese Daten zugreifen kann. Die Kommunikation oder der Datenaustausch kann nur über eine Reihe gut definierter APIs erfolgen.

### Shared Database
Eine gemeinsam genutzte Datenbank kann eine sinnvolle Option sein, wenn die Herausforderungen im Zusammenhang mit Database Per Service für Ihr Team zu schwierig werden.
Dieser Ansatz versucht, die gleichen Probleme zu lösen. Dies geschieht jedoch durch einen wesentlich nachgiebigeren Ansatz, indem eine gemeinsam genutzte Datenbank verwendet wird, auf die mehrere Mikrodienste zugreifen.
Meistens ist dies ein sichereres Muster für Entwickler, da sie in der Lage sind,auf bestehende Weise zu arbeiten. Bekannte ACID-Transaktionen werden verwendet,um die Konsistenz zu gewährleisten.
Durch diesen Ansatz werden jedoch die meisten Vorteile von Microservices zunichte gemacht. Teamübergreifende Entwickler müssen die Schemaänderungen an Tabellen koordinieren. Es kann auch zu Laufzeitkonflikten kommen, wenn mehrere Dienste versuchen, auf dieselben Datenbankressourcen zuzugreifen.
Insgesamt kann dieser Ansatz langfristig mehr schaden als nützen.

### Saga Pattern
Das Saga-Muster ist die Lösung für die Implementierung von Geschäftstransaktionen, die sich über mehrere Microservices erstrecken.
Eine  Saga  ist im Grunde eine Folge lokaler Transaktionen. Für jede innerhalb einer Saga durchgeführte Transaktion veröffentlicht der Dienst, der die Transaktion durchführt, ein Ereignis. Die nachfolgende Transaktion wird basierend auf der Ausgabe der vorherigen Transaktion ausgelöst. Und wenn eine der Transaktionen in dieser Kette fehlschlägt, führt die Saga eine Reihe von Ausgleichstransaktionen aus, um die Auswirkungen aller vorherigen Transaktionen rückgängig zu machen.

### API Composition
Dieses Muster ist eine direkte Lösung für das Problem der Implementierung komplexer Abfragen in einer Microservices-Architektur.
In diesem Muster ruft ein API Composer andere Microservices in der erforderlichen Reihenfolge auf. Nach dem Abrufen der Ergebnisse werden die Daten im Arbeitsspeicher verknüpft, bevor sie dem Verbraucher zur Verfügung gestellt werden.
Wie offensichtlich ist der Nachteil dieses Musters die Verwendung ineffizienter speicherinterner Verknüpfungen für potenziell große Datasets.

### CQRS - Command Query Responsibility Segragation
CQRS (Command Query Responsibility Segregation) ist ein Versuch, die Probleme mit dem API Composition Pattern zu umgehen.
Eine Anwendung überwacht Domänenereignisse von anderen Microservices und aktualisiert die Ansicht oder die Abfragedatenbank. Sie können komplexe Aggregationsabfragen aus dieser Datenbank bedienen. Sie können die Leistung optimieren und die Abfrage-Microservices entsprechend skalieren.
Der Nachteil dabei ist eine zunehmende Komplexität. Plötzlich sollte Ihr Microservice Ereignisse verarbeiten. Dies kann zu Latenzproblemen führen, bei denen die Ansichtsdatenbank möglicherweise konsistent ist und nicht immer konsistent. Es kann auch die Codeduplizierung erhöhen.

### Event Sourcing
Die Ereignisbeschaffung versucht hauptsächlich, das Problem der atomaren Aktualisierung der Datenbank und der Veröffentlichung eines Ereignisses zu lösen.
Bei der Ereignisbeschaffung speichern Sie den Status der Entität oder des Aggregats als Folge von Statusänderungsereignissen. Ein neues Ereignis wird jedes Mal erstellt, wenn ein Update oder eine Einfügung vorliegt. Der Ereignisspeicher wird zum Speichern der Ereignisse verwendet.


## Sessions
### Sticky sessions
Dadurch wird sichergestellt, dass alle Anforderungen eines bestimmten Benutzers an denselben Server gesendet werden, der die erste Anforderung für diesen Benutzer bearbeitet hat. Auf diese Weise wird sichergestellt, dass die Sitzungsdaten für einen bestimmten Benutzer immer korrekt sind. Diese Lösung hängt jedoch vom Load Balancer ab und kann nur das horizontal erweiterte Cluster-Szenario erfüllen. Wenn der Load Balancer jedoch aus irgendeinem Grund plötzlich gezwungen wird, Benutzer auf einen anderen Server zu verschieben, gehen alle Sitzungsdaten des Benutzers verloren.

### Session replication
Bedeutet, dass jede Instanz alle Sitzungsdaten speichert und über das Netzwerk synchronisiert. Das Synchronisieren von Sitzungsdaten verursacht einen Mehraufwand für die Netzwerkbandbreite. Solange sich die Sitzungsdaten ändern, müssen die Daten mit allen anderen Computern synchronisiert werden. Je mehr Instanzen, desto mehr Netzwerkbandbreite bringt die Synchronisation.

### Centralized session storage
Bedeutet, dass beim Zugriff eines Benutzers auf einen Mikrodienst Benutzerdaten aus dem gemeinsamen Sitzungsspeicher abgerufen werden können, um sicherzustellen, dass alle Mikrodienste dieselben Sitzungsdaten lesen können. In einigen Szenarien ist dieses Schema sehr gut und der Anmeldestatus des Benutzers ist undurchsichtig. Es ist auch eine hochverfügbare und skalierbare Lösung. Der Nachteil dieser Lösung ist jedoch, dass der gemeinsame Sitzungsspeicher einen bestimmten Schutzmechanismus erfordert und daher auf sichere Weise zugänglich sein muss.


## Status information / Monitoring
### Application Metrics
Diese Metriken beziehen sich speziell auf Ihre Anwendung. Wenn Ihre Anwendung Benutzerregistrierungen akzeptiert, kann eine Standardmetrik sein, wie viele in der letzten Stunde erfolgreich abgeschlossen wurden. Ein Steuervorbereitungssystem kann kontextspezifische Ereignisse wie die Formularvalidierung aufzeichnen. Diese Daten auf oberster Ebene sind für Entwicklungsteams und die Organisation hilfreich, um das Funktionsverhalten des Systems zu verstehen. Wenn die Validierung von Formularen mit maximalem Volumen in der Regel 1.000 Mal pro Stunde erfolgt und dieser Durchsatz in den letzten zwei Stunden plötzlich auf 500 sinkt, kann diese Anomalie ein Hinweis auf ein Problem sein.

### Platform Metircs
Diese Metriken geben Aufschluss über die Hauptmerkmale Ihrer Infrastruktur. Beispiele beinhalten:
Die durchschnittliche Gesamtausführungszeit für jede der zehn am häufigsten ausgeführten Datenbankabfragen.
Die durchschnittliche Ausführungszeit der schnellsten 10 Prozent;
Die durchschnittliche Ausführungszeit der langsamsten 10 Prozent.
Die Anzahl der Anfragen pro Minute, die ein Dienst erhält.
Die durchschnittliche Antwortzeit für jeden Service-Endpunkt.
Das Erfolgs / Fehler-Verhältnis für jeden Dienst.
Zusammen bieten diese Metriken ein Dashboard, mit dem die Leistung und das Verhalten von Systemen auf niedriger Ebene erfasst werden können. Im Idealfall werden Sie durch diese Metriken auf Leistungseinbußen aufmerksam gemacht, die sich wahrscheinlich auf den Gesamtdurchsatz auswirken oder zu einem systemweiten Ausfall führen. Es ist wichtig, Low-Level-Daten auf diese Weise zu verwenden, um größere Fehler vorherzusagen und zu verhindern, bevor sie auftreten.
Die Raygun APM-Plattform bietet ein Dashboard, mit dem diese und andere Arten von Metriken in Bezug auf die Gesamtsystemleistung visualisiert werden können.

### System Events
Äußere Kräfte wirken ständig auf Systeme. Am häufigsten und möglicherweise am störendsten sind neue Bereitstellungen. Das Betriebspersonal weiß, dass eine starke Korrelation zwischen neuen Code-Bereitstellungen und Systemfehlern besteht. Angesichts dieser Realität ist es sinnvoll, ein Protokoll dieser Bereitstellungen in die Zeitreihendaten aufzunehmen, die von den Anwendungen zusammen mit den übrigen Metriken aufgezeichnet werden. Skalierungsereignisse, Konfigurationsaktualisierungen und andere betriebliche Änderungen sind ebenfalls relevant und sollten aufgezeichnet werden. Das Aufzeichnen dieser Ereignisse ermöglicht es auch, sie mit dem Systemverhalten zu korrelieren.

### Überwachungs-Tools
**Raygun APM** : Die APM-Plattform von Raygun ist ein weiteres Beispiel für ein komplettes System, das sowohl Instrumentierungs- als auch Erfassungsprozesse sowie ein Dashboard zur Visualisierung von Messdaten bietet. Raygun APM unterstützt .NET. Java- und Ruby-Unterstützung sind in Entwicklung.<br>

**Zipkin** : Zipkin ist ein Open-Source-Verfolgungssystem, das speziell für die Verfolgung von Anrufen zwischen Mikrodiensten entwickelt wurde. Es ist besonders nützlich für die Analyse von Latenzproblemen. Zipkin enthält sowohl Instrumentenbibliotheken als auch die Collector-Prozesse, die Ablaufverfolgungsdaten erfassen und speichern.<br>

**Apache Kafka** : Kafka ist ein Streams-Verarbeitungssystem. Es verwendet eine Publish / Subscribe-Methode zum Lesen und Schreiben von Daten in einen logischen Stream, dessen Konzept einem Messaging-System wie RabbitMQ ähnelt. Kafka kann mit anderen Tools wie Zipkin kombiniert werden, um eine robuste Lösung für die Übertragung und Speicherung von Messdaten bereitzustellen.<br>

**Grafana** : Die mit all diesen Tools gesammelten Daten sind nur dann sehr nützlich, wenn sie interpretiert und analysiert werden können. Zu diesem Zweck ist Grafana ein webbasiertes Visualisierungstool, mit dem visuelle Dashboards erstellt werden.<br>

**Prometheus** : Prometheus ist eine Open-Source-Überwachungslösung, die ursprünglich von SoundCloud entwickelt wurde. Es wird häufig zum Speichern und Abfragen von „Zeitreihendaten“ verwendet. Hierbei handelt es sich um Daten, die Aktionen im Zeitverlauf beschreiben. Prometheus wird häufig mit anderen Tools, insbesondere Grafana, kombiniert, um die Zeitreihendaten zu visualisieren und Dashboards bereitzustellen.


## Transactions
Ohne Transaktionen können keine Echtzeitanwendung verwendet werden kann. Bei der Transaktion kann es sich um Geldtransfer, E-Mail-Versand, Auftragserteilung,Rechnungszahlung usw. handeln. Vereinfacht ausgedrückt, handelt es sich bei einer Transaktion um eine Arbeitseinheit, die in jeder Geschäftsanwendung ausgeführt wird, in der Daten in einem bestimmten Zustand erhalten bleiben, jedoch um jede Einheit von Die Arbeit sollte vollständig festgeschrieben oder rückgängig gemacht werden, um die Datenintegrität sicherzustellen.

### Monolithic vs. Microservices
Monolithische Anwendungen bleiben beim Umgang mit Transaktionen in erster Linie bei den ACID-Eigenschaften. Der größte Vorteil für die monolithische Anwendung im Transaktionsmanagement ist ein einziger und gemeinsamer Datenbankserver. Transaktionen können auf Datenbankebene initiiert und basierend auf dem Endergebnis der Transaktion festgeschrieben oder rückgängig gemacht werden. Diese Art des Initiierens einer Transaktion, Durchführen von Vorgängen und Beibehalten oder Nichtbeibehalten von Daten ist viel einfacher zu entwickeln. Dieser Vorteil wird jedoch zu einer ernsthaften Herausforderung bei der Ausführung von Großserienanwendungen. Eine einfache Sperre einer kritischen Tabelle kann zu katastrophalen Ergebnissen führen, z. B. zur Nichtverfügbarkeit der gesamten Anwendung.
In den Richtlinien von Microservices wird dringend empfohlen, das Single Repository Principle (SRP) zu verwenden. Dies bedeutet, dass jeder Mikrodienst seine eigene Datenbank verwaltet und kein anderer Dienst direkt auf die Datenbank des anderen Dienstes zugreifen sollte. Es gibt keine direkte und einfache Möglichkeit, ACID-Prinzipien über mehrere Datenbanken hinweg zu verwalten. Auf diese Weise liegt die eigentliche Herausforderung für das Transaktionsmanagement in Microservices.


## Concurrency
In Microservices kann eine logisch atomare Operation häufig mehrere Microservices umfassen. Sogar ein monolithisches System kann mehrere Datenbanken oder Messaging-Lösungen verwenden. Bei mehreren unabhängigen Datenspeicherungslösungen besteht das Risiko inkonsistenter Daten, wenn einer der verteilten Prozessteilnehmer ausfällt, z. B. wenn ein Kunde belastet wird, ohne eine Bestellung aufzugeben, oder der Kunde nicht benachrichtigt wird, dass die Bestellung erfolgreich war.<br>

Solange wir mehrere Speicherorte für die Daten haben (die sich nicht in einer einzigen Datenbank befinden), wird die Konsistenz nicht automatisch gelöst, und die Ingenieure müssen sich beim Entwerfen des Systems um die Konsistenz kümmern. Momentan gibt es meiner Meinung nach in der Branche noch keine allgemein bekannte Lösung für die atomare Aktualisierung von Daten in mehreren verschiedenen Datenquellen - und wir sollten wahrscheinlich nicht abwarten, bis eine verfügbar ist.

Ein Versuch, dieses Problem auf automatisierte und problemlose Weise zu lösen, ist das XA-Protokoll, das das Zwei-Phasen-Festschreibungsmuster (2PC) implementiert . In modernen High-Scale-Anwendungen (insbesondere in einer Cloud-Umgebung) scheint 2PC jedoch nicht so gut zu funktionieren. Um die Nachteile von 2PC zu beseitigen, müssen wir ACID gegen BASE eintauschen und uns je nach Anforderung auf unterschiedliche Weise um die Konsistenz kümmern.<br>

**Saga-Muster**
Die bekannteste Methode zur Behandlung von Konsistenzproblemen bei mehreren Mikrodiensten ist das Saga-Muster. Sie können Sagas als verteilte Koordination mehrerer Transaktionen auf Anwendungsebene behandeln. Je nach Anwendungsfall und Anforderungen optimieren Sie Ihre eigene Saga-Implementierung. Im Gegensatz dazu versucht das XA-Protokoll, alle Szenarien abzudecken. Das Saga-Muster ist auch nicht neu. Es war in der Vergangenheit bekannt und wurde in ESB- und SOA-Architekturen verwendet. Schließlich gelang der Übergang in die Welt der Mikrodienstleistungen. Jeder atomare Geschäftsvorgang, der mehrere Services umfasst, kann aus mehreren Transaktionen auf technischer Ebene bestehen. Die Schlüsselidee des Saga-Musters besteht darin, eine der einzelnen Transaktionen rückgängig machen zu können. Wie wir wissen, ist ein Rollback für bereits festgeschriebene Einzeltransaktionen nicht möglich. Dies wird jedoch durch Aufrufen einer Kompensationsaktion erreicht - durch Einführen einer "Abbrechen" -Operation.


## Security
### OAuth für die Benutzeridentitäts und Zugriffskontrolle
Die überwiegende Mehrheit der Anwendungen muss ein gewisses Maß an Zugriffskontrolle und Berechtigungsverwaltung durchführen . Was Sie hier vermeiden möchten, ist das Rad neu zu erfinden. OAuth / OAuth2 ist hinsichtlich der Benutzerautorisierung praktisch der Industriestandard. Obwohl das Erstellen eines eigenen benutzerdefinierten Autorisierungsprotokolls eine Option ist, wird es von vielen Anbietern nicht empfohlen, es sei denn, Sie haben starke und sehr spezifische Gründe dafür.
Während OAuth2  nicht perfekt ist , ist es ein weit verbreiteter Standard. Der Vorteil der Verwendung besteht darin, dass Sie sich auf Bibliotheken und Plattformen verlassen können, die Ihre Entwicklungsphase erheblich beschleunigen. Aus dem gleichen Grund haben bereits einige der größten Unternehmen und intelligentesten Ingenieure verschiedene Lösungen zur Verbesserung des Sicherheitsniveaus Ihres OAuth-basierten Autorisierungsdienstes entwickelt.

### "Defence in depth" um Dienste zu priorisieren
Es ist ein großer Fehler, wenn Sie davon ausgehen, dass eine Firewall in Ihrem Netzwerk zum Schutz Ihrer Software ausreicht. "Defence in depth" ist definiert als "ein Informationssicherungskonzept, bei dem mehrere Ebenen von Sicherheitskontrollen (Verteidigung) in einem Informationstechnologiesystem angeordnet sind."

Im Klartext müssen Sie lediglich die vertraulichsten Dienste identifizieren und ihnen eine Reihe von verschiedenen Sicherheitsebenen zuweisen, damit ein potenzieller Angreifer, der eine Ihrer Sicherheitsebenen ausnutzen kann, diese noch ermitteln muss Sie haben die Möglichkeit, alle anderen Abwehrmechanismen bei Ihren kritischen Services zu überwinden.

### Keine eigenen Krypto-Codes schreiben
Im Laufe der Jahre haben viele Menschen unglaublich viel Geld, Zeit und Ressourcen in den Bau von Bibliotheken investiert, die sich mit Ver- und Entschlüsselung befassen. Wenn Sie 10 intelligente und kompetente Sicherheitsleute anheuern, sie alle in einen Raum stellen und sie bitten würden, die bestmögliche Bibliothek für die Ver- und Entschlüsselung zu entwickeln, würden sie zweifellos so gut sein wie die besten Open-Source-Kryptobibliotheken, die es gibt sind schon da draußen.
Wenn es um Sicherheit geht, sollten Sie die meiste Zeit nicht versuchen, Ihre eigenen neuen Lösungen und Algorithmen zu entwickeln, es sei denn, Sie haben starke und spezifische Gründe dafür und Sie haben Leute, die qualifiziert genug sind, um etwas zu schaffen, das beinahe so gut ist wie das Open-Source-Tools sind bereits verfügbar (Tools, die von der Community intensiv getestet wurden).
In den meisten Fällen sollten Sie  NaCl / libsodium  zur Verschlüsselung verwenden. Es gibt es schon seit mehreren Jahren und es ist schnell, einfach zu bedienen und sicher. Die ursprüngliche Implementierung von NaCl ist in C geschrieben , unterstützt aber auch C ++ und Python . Und dank der libsodium-Fork sind verschiedene Adapter für andere Sprachen wie PHP , Javascript und Go  verfügbar.

### Automatische Sicherheitsupdates
Wenn Sie möchten, dass Ihre Microservices-Architektur gleichzeitig sicher und skalierbar ist, ist es eine gute Idee, in der frühen Entwicklungsphase einen Weg zu finden, um alle Ihre Software-Updates zu automatisieren oder zumindest unter Kontrolle zu halten.
Eine hohe Testabdeckung ist hier wichtiger denn je. Jedes Mal, wenn ein Teil Ihres Systems aktualisiert wird, möchten Sie sicherstellen, dass Sie Probleme früh genug und so detailliert wie möglich erkennen.
Stellen Sie sicher, dass Ihre Plattform größtenteils " atomar" ist. Das bedeutet, dass alles in Container eingeschlossen werden sollte,  sodass das Testen Ihrer Anwendung mit einer aktualisierten Bibliothek oder Sprachversion nur eine Frage des Umschließens eines anderen Containers ist. Sollte der Vorgang fehlschlagen, ist das Umkehren ziemlich einfach und kann vor allem automatisiert werden.

### Überwachung
Sie können es sich nicht leisten, ein verteiltes System ohne eine solide, fortschrittliche und zuverlässige Überwachungsplattform zu betreiben. Es gibt verschiedene Lösungen, aber die speziell für Microservices entwickelte Lösung, die es bisher gab, ist Prometheus.
Prometheus wurde ursprünglich von Ingenieuren bei SoundCloud entwickelt und ist eine Open-Source-Überwachungsplattform und Teil der Cloud Native Computing Foundation . Es wird von einigen der größten Akteure der Branche wie SoundCloud selbst, CoreOS und Digital Ocean unterstützt und übernommen.
Andere Überwachungslösungen umfassen InfluxDB , statsd und mehrere bekannte kommerzielle Plattformen.

### Sicherheitsscanner
Innerhalb Ihrer automatisierten Testsuite ist es sinnvoll, regelmäßige Schwachstellen- und Sicherheitsüberprüfungen für Ihre Container durchzuführen. Der Hauptdarsteller von Open Source in diesem Bereich scheint Clair von CoreOS zu sein. Docker Security Scanning und Twistlock sind einige kommerzielle Optionen.
Beachten Sie außerdem, dass das Container-Image selbst möglicherweise nur dann als vertrauenswürdig eingestuft wird, wenn seine Signatur überprüft wurde. rkt tut dies standardmäßig, während Docker vor einiger Zeit eine ähnliche Funktion einführte, nachdem mehrere Sicherheitslücken gefunden wurden.


## Performance
Effizienz ist von größter Bedeutung in der realen, groß angelegten Architektur verteilter Systeme, und Mikroservice-Ökosysteme bilden keine Ausnahme von dieser Regel. Es ist einfach, die Effizienz eines einzelnen Systems (wie bei einer monolithischen Anwendung) zu quantifizieren, aber die Bewertung der Effizienz und die Erzielung einer höheren Effizienz in einem großen Ökosystem von Mikrodiensten, in dem Aufgaben zwischen Hunderten (wenn nicht Tausenden) von kleinen Diensten aufgeteilt werden, ist unglaublich schwer. Es ist auch durch die Gesetze der Computerarchitektur und verteilter Systeme begrenzt, die die Effizienz großer, komplexer verteilter Systeme einschränken: Je verteilter Ihr System ist und je mehr Mikrodienste Sie in diesem System einsetzen, desto geringer ist die Wahrscheinlichkeit Unterschied wird die Effizienz eines Microservices auf dem gesamten System haben. Die Vereinheitlichung von Grundsätzen zur Steigerung der Gesamteffizienz wird zur Notwendigkeit.


## Availability
Ein Mikroservice muss ausfallsicher sein und häufig auf einem anderen Computer neu gestartet werden können, um die Verfügbarkeit zu gewährleisten. Diese Ausfallsicherheit hängt auch von dem Status ab, der für den Mikrodienst gespeichert wurde, von dem der Mikrodienst diesen Status wiederherstellen kann, und davon, ob der Mikrodienst erfolgreich neu gestartet werden kann. Mit anderen Worten, es muss eine Ausfallsicherheit in der Rechenkapazität (der Prozess kann jederzeit neu gestartet werden) sowie eine Ausfallsicherheit im Zustand oder in den Daten (kein Datenverlust, und die Daten bleiben konsistent) bestehen.Die Probleme der Ausfallsicherheit verschärfen sich in anderen Szenarien, z. B. wenn während eines Anwendungsupgrades Fehler auftreten. Der mit dem Bereitstellungssystem zusammenarbeitende Microservice muss bestimmen, ob weiterhin auf die neuere Version oder auf eine frühere Version zurückgegriffen werden kann, um einen konsistenten Status beizubehalten. Fragen, wie zum Beispiel, ob genügend Maschinen verfügbar sind, um weiter voranzukommen, und wie frühere Versionen des Microservices wiederhergestellt werden können, müssen berücksichtigt werden. Dazu muss der Mikrodienst Integritätsinformationen senden, damit die gesamte Anwendung und der Orchestrator diese Entscheidungen treffen können.


## Scaling
Der Skalierbarkeitswürfel beschreibt die Skalierbarkeit anhand eines Würfelmodells. Der "Skalierungswürfel" besteht aus einer X-Achse, einer Y-Achse und einer Z-Achse. Die traditionelle Methode zur Skalierung durch Ausführen mehrerer Kopien einer Anwendung, die auf mehrere Server verteilt ist, ist die X-Achse.<br>

Der allgemeine Ansatz von Microservices verläuft entlang der Y-Achse. Die Skalierung auf der Y-Achse unterteilt die Anwendung in ihre Komponenten und Dienste. Der Softwarearchitekt Chris Richardson erklärte diese Methode in einem Blogbeitrag: "Jeder Dienst ist für eine oder mehrere eng verwandte Funktionen verantwortlich. Es gibt verschiedene Möglichkeiten, die Anwendung in Dienste zu zerlegen. Ein Ansatz besteht darin, verbbasierte Zerlegung und Definition zu verwenden Services, die einen einzelnen Anwendungsfall implementieren, z. B. Checkout. Die andere Option besteht darin, die Anwendung nach Nomen zu zerlegen und Services zu erstellen, die für alle Vorgänge in Bezug auf eine bestimmte Entität verantwortlich sind, z -basierte Zersetzung."<br>

Das verlässt die Z-Achse. Die X-Achse ist eine traditionelle Skalierung des Lastausgleichs und die Y-Achse umfasst Microservices. Die Z-Achse verfolgt einen ähnlichen Ansatz wie die X-Achse: Sie führt identische Codekopien auf mehreren Servern aus. Was die Z-Achsen-Skalierung einzigartig macht, ist, dass sie auch eine Seite von der Y-Achse ausleiht, sodass jeder Server nur für eine Teilmenge der Anwendung und nicht für die gesamte Anwendung verantwortlich ist.<br>


## Load Balancing
### Server Side Load Blancing
In der Java EE-Architektur stellen wir unsere War- / Ear-Dateien auf mehreren Anwendungsservern bereit, erstellen dann einen Serverpool und stellen einen Load Balancer (Netscaler) davor, der eine öffentliche IP hat. Der Client stellt eine Anfrage unter Verwendung dieser öffentlichen IP, und Netscaler entscheidet, auf welchem ​​internen Anwendungsserver die Anfrage per Round-Robin- oder Sticky-Session-Algorithmus weitergeleitet wird. Wir nennen es Server Side Load Balancing.<br>

**Problem:**  Wenn ein oder mehrere Server nicht mehr reagieren, müssen Sie diese Server manuell aus dem Load Balancer entfernen, indem Sie die IP-Tabelle des Load Balancers aktualisieren.
Ein weiteres Problem besteht darin, dass wir eine Failover-Richtlinie implementieren müssen, um dem Client ein nahtloses Erlebnis zu bieten.
Microservices verwenden jedoch keinen serverseitigen Lastenausgleich. Sie verwenden clientseitigen Lastenausgleich.

### Client Side Load Balancing
Beim clientseitigen Lastausgleich wird ein Algorithmus wie Round-Robin oder zonenspezifisch beibehalten. über die es Instanzen von aufrufenden Diensten aufrufen kann. Der Vorteil ist, dass sich die Serviceregistrierung immer selbst aktualisiert. Wenn eine Instanz ausfällt, wird sie aus der Registrierung entfernt. Wenn der clientseitige Load Balancer mit dem Eureka-Server kommuniziert, aktualisiert er sich immer selbst, sodass im Gegensatz zum serverseitigen Load Balancing keine manuellen Eingriffe zum Entfernen einer Instanz erforderlich sind.
Ein weiterer Vorteil ist, dass Sie den Load-Balancing-Algorithmus programmgesteuert steuern können, da sich der Load-Balancer auf der Clientseite befindet. Ribbon bietet diese Möglichkeit, daher werden wir Ribbon für den clientseitigen Lastenausgleich verwenden.


## Messaging
Beim Übergang von einer monolithischen Anwendungsstruktur zu einer multi-unabhängigen Struktur stellen Sie sofort fest, dass das Aufrufen anderer Komponenten nicht auf ein System mit nur einem Prozess ausgerichtet ist. Innerhalb eines Single-Process-Systems rufen Sie normalerweise Komponenten mit verschiedenen Sprachmethoden oder über Dependency Injection auf, wie wir es bei Angular sehen. Da eine microservices-basierte Anwendung auf einer Vielzahl von Servern, Hosts und Prozessen ausgeführt werden kann, ist die Kommunikation auf HTTP (Hyper Text Transfer Protocol), TCP (Transmission Control Protocol) und AMQP (Advanced Message Queuing Protocol) ausgerichtet. Alle diese Protokolle sind für die IPC- oder Interprozesskommunikation konzipiert, da sie gemeinsam genutzte Daten verwalten. <br>

* Synchronous protocol
* Asynchronous protocol
* Single receiver
* Multiple receivers

### Synchronous Protocol
Synchronous Protocol ist in Chat-Funktionen, HTTP, Instant Messaging und Live-Funktionen integriert ist. Es handelt sich um eine Datenübertragung, die in regelmäßigen Abständen stattfindet und in der Regel von der Taktung des Mikroprozessors abhängt, da zwischen Sender und Empfänger ein Taktsignal bestehen muss. Es ist so zu sagen ein Protokoll, dass eine Primär- / Replikatkonfiguration erfordert, da ein Gerät die Kontrolle über ein anderes Gerät hat, um die Synchronität sicherzustellen.

### Asynchronous Portocol
Das Gegenteil von synchronem, asynchronem Protokoll arbeitet außerhalb der Beschränkungen eines Taktsignals und tritt zu jeder Zeit und in unregelmäßigen Intervallen auf. Wie oben erwähnt, ist das synchrone Protokoll mikroprozessorabhängig, was bedeutet, dass diese Protokolle häufig für die in einem Computer ablaufenden Prozesse verwendet werden. Bei asynchronen Prozessen sind sie aufgrund der fehlenden Abhängigkeit für Cloud-Umgebungen und Betriebssysteme weit verbreitet. Nach dem Senden von Informationen muss nicht auf eine Antwort des Empfängers gewartet werden.

### Single Receiver
Im Namen implizit bedeutet eine einzelne Empfängereinrichtung, dass jede Anforderung von einem Empfänger verarbeitet werden muss. Bei der Datenübertragung müssen Anforderungen daher gestaffelt sein, um empfangen zu werden, da sie nicht gleichzeitig empfangen werden können.

### Multiple Receivers
Mehrere Empfänger können mehrere Anforderungen verarbeiten, da jede Anforderung von null bis zu mehreren Empfängern verarbeitet werden kann. Beispielsweise werden in der Regel mehrere Empfänger in einem Saga-Muster verwendet, da es asynchron sein und gleichzeitig die Datenkonsistenz fördern muss.


## Monitoring
Anwendungen, die unter Verwendung der Mikroservice-Architektur entwickelt wurden, müssen aus denselben Gründen überwacht werden wie alle anderen Arten von verteilten Systemen: Das heißt, alle Systeme fallen schließlich aus.

* Überwachung von Containern und deren Inhalt
* Warungen zur Servicleistung, nicht zur Containerleistung
* Überwachung von Diensten welche felxibel und standortübergreifend sind
* Überwachung der APIs
* Überwachung über APIs


## APIs
API steht für Application Programming Interface, wobei das Schlüsselwort interface ist . APIs sind sozusagen die Türen , durch die Entwickler mit einer Anwendung interagieren können.
APIs gibt es seit den Anfängen des Computerbetriebs , die es Computern ermöglichen, Wiederholungsfunktionen aufzurufen, um das Aufblähen von Anwendungen zu verringern. Bei der Erörterung von APIs in der heutigen digitalen Wirtschaft geht es jedoch in der Regel um Web-APIs , die die B2B-Kommunikation erleichtern.
Allgemein gesagt, ermöglichen APIs Entwicklern, intern und extern eines von zwei Dingen auszuführen: Zugriff auf die Daten einer Anwendung oder Verwendung der Funktionen einer Anwendung . Letztendlich sind auf diese Weise die Elektronik, Anwendungen und Webseiten der Welt miteinander verbunden, um miteinander zu kommunizieren und zusammenzuarbeiten.

### Unterschiede zwischen APIs und Microservices¨
Microservice sind eine Architektur für Web - Anwendungen, bei denen die Funktionalität bis aufgeteilt in kleinem Web - Service.<br>

wohingegen<br>

APIs sind die Frameworks, über die Entwickler mit einer Webanwendung interagieren können.<br>
Der Reiz der APIs ist zweifach für die meisten Unternehmen, da APIs oft das Medium der Kommunikation zwischen Microservices sind, sondern auch , weil sie auch verwendet werden , kann eine Anwendung die Daten und Funktionalität an Dritte zu entlarven, was den Weg für leistungsstarke Integrationen.


**Fazit und Aussicht**, Die Durcharbeitung von 701.1 Modern Software Development gab mir ein besseres Verständnis darüber wie ein Microservices verschiedene Aufgaben handhabt und verwendet.

***

***
## Kapitel: 2 What is all this ?! (Status: In Arbeit)

**Weight**: Personal value

**Beschreibung** Short explaination of ~~all~~ most services used in combination with Kubernetes.

**Tagesziele**, Since I have to read and understand each of the services I can not estimate how long I am going to take for each service. I'll try to do all of them.

**Vorgehen**, Read guides about Docker, keep them as link and conclude the most valuable information as markdown sheet.

### Beispiele und Arbeitsergebnisse

#### Ansible
Ansible ist ein Open-Source Automatisierungs-Werkzeug zur Orchestrierung und allgemeinen Konfiguration und Administration von Computern. Es kombiniert Softwareverteilung, Ad-hoc-Kommando-Ausführung und Konfigurationsmanagement. Es verwaltet Netzwerkcomputer unter anderem über SSH und erfordert keinerlei zusätzliche Software auf dem zu verwaltenden System. Module nutzen zur Ausgabe JSON und können in jeder beliebigen Programmiersprache geschrieben sein. Das System nutzt YAML zur Formulierung wiederverwendbarer Beschreibungen von Systemen.

#### Kubeadm
Kubeadm is a tool built to provide kubeadm init and kubeadm join as best-practice “fast paths” for creating Kubernetes clusters.

kubeadm performs the actions necessary to get a minimum viable cluster up and running. By design, it cares only about bootstrapping, not about provisioning machines. Likewise, installing various nice-to-have addons, like the Kubernetes Dashboard, monitoring solutions, and cloud-specific addons, is not in scope.

Instead, we expect higher-level and more tailored tooling to be built on top of kubeadm, and ideally, using kubeadm as the basis of all deployments will make it easier to create conformant clusters.

More about [Kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/)

#### Kubectl
Kubectl is a command line interface for running commands against Kubernetes clusters. kubectl looks for a file named config in the $HOME/.kube directory. You can specify other kubeconfig files by setting the KUBECONFIG environment variable or by setting the --kubeconfig flag.

This overview covers kubectl syntax, describes the command operations, and provides common examples. For details about each command, including all the supported flags and subcommands, see the kubectl reference documentation. For installation instructions see installing kubectl.

More about [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)

#### Pods
A Pod is the basic execution unit of a Kubernetes application–the smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents processes running on your Cluster .

A Pod encapsulates an application’s container (or, in some cases, multiple containers), storage resources, a unique network IP, and options that govern how the container(s) should run. A Pod represents a unit of deployment: a single instance of an application in Kubernetes, which might consist of either a single container or a small number of containers that are tightly coupled and that share resources.

Docker is the most common container runtime used in a Kubernetes Pod, but Pods support other container runtimes as well.

More about [Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)

**Links:** 
+ [Microservices benefits ands challanges](https://www.cio.com/article/3201193/7-reasons-to-switch-to-microservices-and-5-reasons-you-might-not-succeed.html)
+ second one




**Common Commands

| Name                                 | Command                                                                |
|--------------------------------------|------------------------------------------------------------------------|
| Run curl test temporarily            | =kubectl run --rm mytest --image=yauritux/busybox-curl -it=            |
| Run wget test temporarily            | =kubectl run --rm mytest --image=busybox -it=                          |
| Run nginx deployment with 2 replicas | =kubectl run my-nginx --image=nginx --replicas=2 --port=80=            |
| Set namespace preference             | =kubectl config set-context <context_name> --namespace=<ns_name>=      |
| List pods with nodes info            | =kubectl get pod -o wide=                                              |
| List everything                      | =kubectl get all --all-namespaces=                                     |
| Get all services                     | =kubectl get service --all-namespaces=                                 |
| Show nodes with labels               | =kubectl get nodes --show-labels=                                      |
| Validate yaml file with dry run      | =kubectl create --dry-run --validate -f pod-dummy.yaml=                |
| Start a temporary pod for testing    | =kubectl run --rm -i -t --image=alpine test-$RANDOM -- sh=             |
| kubectl run shell command            | =kubectl exec -it mytest -- ls -l /etc/hosts=                          |
| Get system conf via configmap        | =kubectl -n kube-system get cm kubeadm-config -o yaml=                 |
| Get deployment yaml                  | =kubectl -n denny-websites get deployment mysql -o yaml=               |
| Explain resource                     | =kubectl explain pods=, =kubectl explain svc=                          |
| Watch pods                           | =kubectl get pods  -n wordpress --watch=                               |
| Query healthcheck endpoint           | =curl -L http://127.0.0.1:10250/healthz=                               |
| Open a bash terminal in a pod        | =kubectl exec -it storage sh=                                          |
| Check pod environment variables      | =kubectl exec redis-master-ft9ex env=                                  |
| Enable kubectl shell autocompletion  | =echo "source <(kubectl completion bash)" >>~/.bashrc=, and reload     |
| Use minikube dockerd in your laptop  | =eval $(minikube docker-env)=, No need to push docker hub any more     |
| Kubectl apply a folder of yaml files | =kubectl apply -R -f .=                                                |
| Get services sorted by name          | kubectl get services --sort-by=.metadata.name                          |
| Get pods sorted by restart count     | kubectl get pods --sort-by='.status.containerStatuses[0].restartCount' |


Check Performance

| Name | Command |
| --- | --- |
| Get node resource usage | =kubectl top node= |
| Get pod resource usage | =kubectl top pod= |
| Get resource usage for a given pod | =kubectl top <podname> --containers= |
| List resource utilization for all containers | =kubectl top pod --all-namespaces --containers=true= |

**Resources Deletion

| Name                                    | Command                                                  |
|-----------------------------------------|----------------------------------------------------------|
| Delete pod                              | =kubectl delete pod/<pod-name> -n <my-namespace>=        |
| Delete pod by force                     | =kubectl delete pod/<pod-name> --grace-period=0 --force= |
| Delete pods by labels                   | =kubectl delete pod -l env=test=                         |
| Delete deployments by labels            | =kubectl delete deployment -l app=wordpress=             |
| Delete all resources filtered by labels | =kubectl delete pods,services -l name=myLabel=           |
| Delete resources under a namespace      | =kubectl -n my-ns delete po,svc --all=                   |
| Delete persist volumes by labels        | =kubectl delete pvc -l app=wordpress=                    |
| Delete statefulset only (not pods)      | =kubectl delete sts/<stateful_set_name> --cascade=false= |

**Log & Conf Files

| Name                      | Comment                                                                   |
|---------------------------|---------------------------------------------------------------------------|
| Config folder             | =/etc/kubernetes/=                                                        |
| Certificate files         | =/etc/kubernetes/pki/=                                                    |
| Credentials to API server | =/etc/kubernetes/kubelet.conf=                                            |
| Superuser credentials     | =/etc/kubernetes/admin.conf=                                              |
| kubectl config file       | =~/.kube/config=                                                          |
| Kubernets working dir     | =/var/lib/kubelet/=                                                       |
| Docker working dir        | =/var/lib/docker/=, =/var/log/containers/=                                |
| Etcd working dir          | =/var/lib/etcd/=                                                          |
| Network cni               | =/etc/cni/net.d/=                                                         |
| Log files                 | =/var/log/pods/=                                                          |
| log in worker node        | =/var/log/kubelet.log=, =kubelet-proxy.log=                               |
| log in master node        | =kube-apiserver.log=, =kube-scheduler.log=, =kube-controller-manager.log= |
| Env                       | =/etc/systemd/system/kubelet.service.d/10-kubeadm.conf=                   |
| Env                       | export KUBECONFIG=/etc/kubernetes/admin.conf                              |

**Pod

| Name                         | Command                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------|
| List all pods                | =kubectl get pods=                                                                        |
| List pods for all namespace  | =kubectl get pods -all-namespaces=                                                        |
| List all critical pods       | =kubectl get -n kube-system pods -a=                                                      |
| List pods with more info     | =kubectl get pod -o wide=, =kubectl get pod/<pod-name> -o yaml=                           |
| Get pod info                 | =kubectl describe pod/srv-mysql-server=                                                   |
| List all pods with labels    | =kubectl get pods --show-labels=                                                          |
| List running pods            | kubectl get pods --field-selector=status.phase=Running                                    |
| Get Pod initContainer status | =kubectl get pod --template '{{.status.initContainerStatuses}}' <pod-name>=               |
| kubectl run command          | kubectl exec -it -n "$ns" "$podname" -- sh -c "echo $msg >>/dev/err.log"                  |
| Watch pods                   | =kubectl get pods  -n wordpress --watch=                                                  |
| Get pod by selector          | kubectl get pods --selector="app=syslog" -o jsonpath='{.items[*].metadata.name}'          |
| List pods and images         | kubectl get pods -o='custom-columns=PODS:.metadata.name,Images:.spec.containers[*].image' |
| List pods and containers     | -o='custom-columns=PODS:.metadata.name,CONTAINERS:.spec.containers[*].name'               |

**Label & Annontation
	
| Name                             | Command                                                           |
|----------------------------------|-------------------------------------------------------------------|
| Filter pods by label             | =kubectl get pods -l owner=denny=                                 |
| Manually add label to a pod      | =kubectl label pods dummy-input owner=denny=                      |
| Remove label                     | =kubectl label pods dummy-input owner-=                           |
| Manually add annonation to a pod | =kubectl annotate pods dummy-input my-url=https://dennyzhang.com= |

**Deployment & Scale

| Name                         | Command                                                                  |
|------------------------------|--------------------------------------------------------------------------|
| Scale out                    | =kubectl scale --replicas=3 deployment/nginx-app=                        |
| online rolling upgrade       | =kubectl rollout app-v1 app-v2 --image=img:v2=                           |
| Roll backup                  | =kubectl rollout app-v1 app-v2 --rollback=                               |
| List rollout                 | =kubectl get rs=                                                         |
| Check update status          | =kubectl rollout status deployment/nginx-app=                            |
| Check update history         | =kubectl rollout history deployment/nginx-app=                           |
| Pause/Resume                 | =kubectl rollout pause deployment/nginx-deployment=, =resume=            |
| Rollback to previous version | =kubectl rollout undo deployment/nginx-deployment=                       |
| Reference     | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]], [[https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment][Link: Pausing and Resuming a Deployment]] |

**Quota & Limits & Resource

| Name                          | Command                                                                 |
|-------------------------------|-------------------------------------------------------------------------|
| List Resource Quota           | =kubectl get resourcequota=                                             |
| List Limit Range              | =kubectl get limitrange=                                                |
| Customize resource definition | =kubectl set resources deployment nginx -c=nginx --limits=cpu=200m=     |
| Customize resource definition | =kubectl set resources deployment nginx -c=nginx --limits=memory=512Mi= |
| Reference                     | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                         |
**Service

| Name                            | Command                                                                           |
|---------------------------------|-----------------------------------------------------------------------------------|
| List all services               | =kubectl get services=                                                            |
| List service endpoints          | =kubectl get endpoints=                                                           |
| Get service detail              | =kubectl get service nginx-service -o yaml=                                       |
| Get service cluster ip          | kubectl get service nginx-service -o go-template='{{.spec.clusterIP}}'            |
| Get service cluster port        | kubectl get service nginx-service -o go-template='{{(index .spec.ports 0).port}}' |
| Expose deployment as lb service | =kubectl expose deployment/my-app --type=LoadBalancer --name=my-service=          |
| Expose service as lb service    | =kubectl expose service/wordpress-1-svc --type=LoadBalancer --name=ns1=           |
| Reference                       | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                                   |
**Secrets

| Name                        | Command                                                               |
|-----------------------------|-----------------------------------------------------------------------|
| List secrets                | =kubectl get secrets --all-namespaces=                                |
| Generate secret             | =echo -n 'mypasswd'=, then redirect to =base64 -decode=               |
| Create secret from cfg file | kubectl create secret generic db-user-pass --from-file=./username.txt |

**StatefulSet

| Name                               | Command                                                  |
|------------------------------------|----------------------------------------------------------|
| List statefulset                   | =kubectl get sts=                                        |
| Delete statefulset only (not pods) | =kubectl delete sts/<stateful_set_name> --cascade=false= |
| Scale statefulset                  | =kubectl scale sts/<stateful_set_name> --replicas=5=     |

**Volumes & Volume Claims

| Name                      | Command                                                      |
|---------------------------|--------------------------------------------------------------|
| List storage class        | =kubectl get storageclass=                                   |
| Check the mounted volumes | =kubectl exec storage ls /data=                              |
| Check persist volume      | =kubectl describe pv/pv0001=                                 |
| Copy local file to pod    | =kubectl cp /tmp/my <some-namespace>/<some-pod>:/tmp/server= |
| Copy pod file to local    | =kubectl cp <some-namespace>/<some-pod>:/tmp/server /tmp/my= |

**Events & Metrics
	
| Name                            | Command                                                    |
|---------------------------------|------------------------------------------------------------|
| View all events                 | =kubectl get events --all-namespaces=                      |
| List Events sorted by timestamp | kubectl get events --sort-by=.metadata.creationTimestamp   |

**Node Maintenance

| Name                                      | Command                       |
|-------------------------------------------|-------------------------------|
| Mark node as unschedulable                | =kubectl cordon $NDOE_NAME=   |
| Mark node as schedulable                  | =kubectl uncordon $NDOE_NAME= |
| Drain node in preparation for maintenance | =kubectl drain $NODE_NAME=    |

**Namespace & Security

| Name                          | Command                                                           |
|-------------------------------|-------------------------------------------------------------------|
| List authenticated contexts   | =kubectl config get-contexts=, =~/.kube/config=                   |
| Set namespace preference      | =kubectl config set-context <context_name> --namespace=<ns_name>= |
| Load context from config file | =kubectl get cs --kubeconfig kube_config.yml=                     |
| Switch context                | =kubectl config use-context <cluster-name>=                       |
| Delete the specified context  | =kubectl config delete-context <cluster-name>=                    |
| List all namespaces defined   | =kubectl get namespaces=                                          |
| List certificates             | =kubectl get csr=                                                 |

**Network
	
| Name                              | Command                                                  |
|-----------------------------------|----------------------------------------------------------|
| Temporarily add a port-forwarding | =kubectl port-forward redis-izl09 6379=                  |
| Add port-forwaring for deployment | =kubectl port-forward deployment/redis-master 6379:6379= |
| Add port-forwaring for replicaset | =kubectl port-forward rs/redis-master 6379:6379=         |
| Add port-forwaring for service    | =kubectl port-forward svc/redis-master 6379:6379=        |
| Get network policy                | =kubectl get NetworkPolicy=                              |

**Patch

| Name                          | Summary                                                               |
|-------------------------------|-----------------------------------------------------------------------|
| Patch service to loadbalancer | =kubectl patch svc $svc_name -p '{"spec": {"type": "LoadBalancer"}}'= |

**Extenstions

| Name                         | Summary                    |
|------------------------------|----------------------------|
| List api group               | =kubectl api-versions=     |
| List all CRD                 | =kubectl get crd=          |
| List storageclass            | =kubectl get storageclass= |
| List all supported resources | =kubectl api-resources=    |

**Components & Services
***Services on Master Nodes

| Name                    | Summary                                                                                                |
|-------------------------|--------------------------------------------------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-apiserver][kube-apiserver]]          | exposes the Kubernetes API from master nodes                                                           |
| [[https://coreos.com/etcd/][etcd]]                    | reliable data store for all k8s cluster data                                                           |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-scheduler][kube-scheduler]]          | schedule pods to run on selected nodes                                                                 |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-controller-manager][kube-controller-manager]] | node controller, replication controller, endpoints controller, and service account & token controllers |

***Services on Worker Nodes

| Name              | Summary                                                                                   |
|---------------------------------------------------------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubelet][kubelet]]           | makes sure that containers are running in a pod                                           |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-proxy][kube-proxy]]        | perform connection forwarding                                                             |
| [[https://github.com/docker/engine][Container Runtime]] | Kubernetes supported runtimes: Docker, rkt, runc and any [[https://github.com/opencontainers/runtime-spec][OCI runtime-spec]] implementation. |

***Addons: pods and services that implement cluster features

| Name                          | Summary                                                                   |
|-------------------------------|---------------------------------------------------------------------------|
| DNS                           | serves DNS records for Kubernetes services                                |
| Web UI                        | a general purpose, web-based UI for Kubernetes clusters                   |
| Container Resource Monitoring | collect, store and serve container metrics                                |
| Cluster-level Logging         | save container logs to a central log store with search/browsing interface |

***Tools

| Name                  | Summary                                                     |
|----------------------|--------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubectl][kubectl]]               | the command line util to talk to k8s cluster                |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubeadm][kubeadm]]               | the command to bootstrap the cluster                        |
| [[https://kubernetes.io/docs/reference/setup-tools/kubefed/kubefed/][kubefed]]               | the command line to control a Kubernetes Cluster Federation |
| Kubernetes Components | [[https://kubernetes.io/docs/concepts/overview/components/][Link: Kubernetes Components]]                                 |

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

