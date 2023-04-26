---
tags: Uni EST
VL-Date: 25.04.23
---
# Frage des Tages
Warum ist eine aussagekräftige Commit Message wichtig?

# Kollaborationsplattformen
Problem: In der Entwicklung eines Softwareprodukts arbeiten viele Menschen zusammen und es entstehen viele Zwischen- und Endprodukte (meist Artefakte genannt). Das Problem dabei ist, dass die Zusammenarbeit an diesen Artefakten und die Kommunikation zwischen diesen Menschen sehr kompliziert, aufwändig und fehlerträchtig werden kann. Dies ist natürlich ähnlich in anderen Gebieten ähnlich, aber vielleicht gerade im [[Software Engineering]] erreichen wir extreme Größen der Artefakte mit Softwaresystemen, die oft mehrere Millionen Zeilen Quellcode enthalten.

Lösung: Deshalb haben sich wahrscheinlich gerade im Kontext [[Software Engineering]] ausgereifte Kollaborationsplattformen entwickelt. Einiges davon ist aus dem Kontext der Entwicklung von verteilter Entwicklung von Open-Source-Software entstanden. Am prominentesten ist derzeit sicher die Plattform GitHub. Diese Plattformen (wie z.B. auch "GitLab", manchmal auch Social Coding Platform genannt) haben aber schon lange die reine Domäne der Open-Source-Software verlassen und stellen heute für quasi alle Software-Projekte die Basis da, in der die Artefakte (wie Code und Dokumentation) verwaltet werden, das Management von Fehlerberichten und Feature-Anforderungen durchzuführen, Zugriff auf diese Artefakte reguliert wird. Darüberhinaus sind gerade auch Kommunikationswerkzeuge gerade im Software-Engineering-Kontext entstanden. Ein prominenter Vertreter ist hier Slack, das eine einfache und schnelle Chat-Kommunikation bietet, die auch einfach zu Audio- und Videoanrufen erweitert werden kann. Schließlich bieten alle die Plattformen in verschiedener Form mit Bots Aktivitäten zu automatisieren.

## Konfigurarionsmanagement - Idee
Die Grundidee des Konfigurationsmanagement ist simpel: Die Konfigurationsmanagement hat ein Monopol auf die Bereitstellung von Software. Die Entwicklerinnen übergeben ihre Resultate nur an das Konfigurationsmanagement. Nur von dort erhalten alle anderen Stellen die Software. Alle Artefakte, die von den Entwicklerinnen erstellt und abgeliefert werden, werden eindeutig identifiziert, erfasst, archiviert und vor Änderungen geschützt. Überholte Versionen werden aufbewahrt, damit sie später rekonstruiert werden können (z.B. weil man zu einem alten Zustand zurückkehren will, weil ein Kunde mit dieser Version Probleme hat oder weil man feststellen will, wann ein bestimmter Effekt erstmals aufgetreten ist). Wenn sich die Entwicklung verzweigt hat, werden alle Varianten bereitgehalten. Konfigurationen werden für die Auslieferung zusammengestellt und präzise dokumentiert. An allen Artefakten, die dem Konfigurationsmanagement unterstehen, können Metriken erhoben werden.
### Definition
Konfigurationsmanagement ist die Gesamtheit der Verfahren, um die Konfigurationen eines Software-Systems zu identifizieren, zu verwalten, bei Bedarf bereitzustellen und ihre Änderungen zu überwachen und zu dokumentieren.

Dazu gehört auch die Möglichkeit, ältere Artefakte und Konfigurationen zu rekonstruieren. Das Konfigurationsmanagement schließt also die Versions- und Variantenverwaltung ein.

## Verzeichnisstruktur
|                    |                                                                            |
| ------------------ | -------------------------------------------------------------------------- |
| src/main/java      | Application/Library sources                                                |
| src/main/resources | Application/Library resources                                              |
| src/main/config    | Configuration files                                                        |
| src/main/scripts   | Application/Library scripts                                                |
| src/main/webapp    | Web application sources                                                    |
| src/test/java      | Test sources                                                               |
| src/test/resources | Test resources                                                             |
| target/            | Output of the build                                                        |
| LICENSE.txt        | Project's license                                                          |
| NOTICE.txt         | Notices and attributions required by libraries that the project depends on |
| README.text        | Project's read me                                                                           |

Sowohl für die kontinuierliche Integration als auch Konfigurations- und Versionsmanagement ist eine klare und standardisierte Verzeichnisstruktur unumgänglich. Es gibt dafür verschiedene Lösungen. Die Folie zeigt einen Ausschnitt aus dem Standardlayout, dass das Apache-Projekt Maven vorschlägt. Es ist insbesondere eine gute Idee, Testcode von Produktionscode zu trennen, da damit das Bauen und Ausliefern einfacher wird.

## Werkzeuge
Z.B.: git, cvs, subversion
Konfigurationsmanagement macht man heute werkzeugunterstützt. Es gibt eine lange Tradition solcher Werkzeuge im [[Software Engineering]]. Derzeit ist git mit Abstand das am weitesten verbreitete Werkzeug in diesem Gebiet. Die Werkzeuge erlauben verschiedenen Personen Zugriff auf einen oder mehrere Zweige der Entwicklung zu geben, neue Versionen einzubringen („einchecken“), Änderungen zu dokumentieren und Releases zu markieren.

## Änderungsmanagement
Im Änderungsmanagement (auch Issue Tracking) verfolgen wir Änderungsforderungen (auch Issues, Tickets, Bugs), die aus verschiedenen Quellen an ein Softwareprodukt gestellt werden. Dass können generelle Anforderungen sein, die direkt darin verwaltet werden, aber auch Fehlermeldungen von Anwender/innen oder auch Wünsche für neue Funktionalität (Feature Requests) werden hier gesammelt. Wichtig ist, dass es einen festgelegten Prozess gibt, wie mit diesen Änderungsforderungen umgegangen wird, sodass die Fehlermeldungen u.a. nicht unbeachtet bleiben. Dazu gehört, dass es Verantwortliche für die Bearbeitung sowie Entscheidungsbefugte gibt, die festlegen können, ob so eine Forderung umgesetzt wird.

## Kommunikationskanäle
Ein weiterer wichtiger Aspekt von Kollaborationsplattformen ist die Bereitstellung von Kommunikationskanälen. Ein Issue Tracker in GitHub ist schon ein solcher Kanal. Für die schnelle und effiziente Kommunikation hat sich aber in den letzten Jahren sehr stark die Nutzung von Chat-Systemen etabliert, wie z.B. Slack.
Slack hat verschiedene Channels, in denen man sich zu den jeweiligen Themen austauschen kann. Slack bietet insbesondere viele Integrationen, sodass man beispielsweise mit dem GitHub Issue Tracker direkt aus Slack interagieren kann.

# Git
2005 ging die Beziehung zwischen der Community, die den Linux Kernel entwickelte, und des kommerziell ausgerichteten Unternehmens, das BitKeeper entwickelte, kaputt. Die zuvor ausgesprochene Erlaubnis, BitKeeper kostenlos zu verwenden, wurde widerrufen. Dies war für die Linux-Entwickler-Community (und besonders für Linus Torvald, der Erfinder von Linux) der Auslöser dafür, ein eigenes Tool zu entwickeln, das auf den Erfahrungen mit BitKeeper basierte.

## Ziele
- Geschwindigkeit
- einfaches Design
- gute Unterstützung von nicht-linearer Entwicklung (tausende parallele Branches, d.h. verschiedener Verzweigungen der Versionen)
- vollständig verteilt
- fähig, große Projekte wie den Linux-Kernel effektiv zu verwalten (Geschwindigkeit und Datenumfang)
## Daten in Git
Git betrachtet seine Daten eher als eine Reihe von Snapshots eines Mini-Dateisystems. Jedes Mal, wenn Du committest (d.h. den gegenwärtigen Status Deines Projektes als eine Version in Git speicherst), sichert Git den Zustand sämtlicher Dateien in diesem Moment („[[Snapshot]]“) und speichert eine Referenz auf diesen [[Snapshot]]. Um dies möglichst effizient und schnell tun zu können, kopiert Git unveränderte Dateien nicht, sondern legt lediglich eine Verknüpfung zu der vorherigen Version der Datei an. Damit sind fast alle Operationen auf den Daten lokal. Ich kann auch ohne Verbindung zum Server vernünftig arbeiten.

## Checksummen zur Dateiverfolgung
In Git werden Änderungen in Checksummen umgerechnet, bevor sie gespeichert werden. Anschließend werden sie mit dieser Checksumme referenziert. Das macht es unmöglich, dass sich die Inhalte von Dateien oder Verzeichnissen ändern, ohne dass Git das mitbekommt. Git basiert auf dieser Funktionalität und sie ist ein integraler Teil von Gits Philosophie. Man kann Informationen deshalb z.B. nicht während der Übermittlung verlieren oder unwissentlich beschädigte Dateien verwenden, ohne dass Git in der Lage wäre, dies festzustellen. Der Mechanismus, den Git verwendet, um diese Checksummen zu erstellen, heißt SHA-1 Hash. Eine solche Checksumme ist eine 40 Zeichen lange Zeichenkette, die aus hexadezimalen Zeichen besteht und diese wird von Git aus den Inhalten einer Datei oder Verzeichnisstruktur kalkuliert.

## Die drei Zustände
![[Git drei Zustände.png|200]]

Git definiert drei Haupt-Zustände, in denen sich eine Datei befinden kann: committed, modified („geändert“) und staged („vorgemerkt“). „Committed“ bedeutet, dass die Daten in der lokalen Datenbank gesichert sind. „Modified“ bedeutet, dass die Datei geändert, diese Änderung aber noch nicht committed wurde. „Staged“ bedeutet, dass Du eine geänderte Datei in ihrem gegenwärtigen Zustand für den nächsten Commit vorgemerkt hast.

## Commit Message
- Short (50 chars or less) summary of changes
- More detailed explanatory text, if necessary. Wrap it to about 72 characters or so. In some contexts, the first line is treated as the subject of an email and the rest of the text as the body. The blank line separating the summary from the body is critical (unless you omit the body entirely); tools like rebase can get confused if you run the two together.
- Further paragraphs come after blank lines.
- Bullet points are okay, too
- Typically a hypen or asterisk is used for the bullet, preceded by a single space, with blank lines in between, but conventions vary here
Wenn man sich angewöhnt, aussagekräftige und hochwertige Commit-Meldungen zu schreiben, macht man sich selbst und anderen das Leben erheblich einfacher. Im allgemeinen sollte eine Commit-Meldung mit einer einzelnen Zeile anfangen, die nicht länger als 50 Zeichen sein sollte. Dann sollte eine leere Zeile folgen und schließlich eine ausführlichere Beschreibung der Änderungen.

## Git-Datenstrukturen
![[Git Datenstrukturen.png|300]]

Wenn Du in Git committest, speichert Git ein sogenanntes Commit-Objekt. Dieses enthält einen Zeiger zu dem Schnappschuss mit den Objekten der Staging-Area, dem Autor, den Commit-Metadaten und einem Zeiger zu den direkten Eltern des Commits. Ein initialer Commit hat keine Eltern-Commits, ein normaler Commit stammt von einem Eltern-Commit ab und ein Merge-Commit, welcher aus einer Zusammenführung von zwei oder mehr Branches resultiert, besitzt ebenso viele Eltern-Commits. Wenn Du einen Commit mit dem Kommando git commit erstellst, erzeugt Git für jedes Projektverzeichnis eine Prüfsumme und speichert diese als sogenanntes tree-Objekt im Git-Repository. Git erzeugt dann ein Commit-Objekt, das die Metadaten und den Zeiger zum tree-Objekt des Wurzelverzeichnis enthält, um bei Bedarf den Snapshot erneut erzeugen zu können. Dein Git-Repository enthält nun fünf Objekte: einen Blob für den Inhalt jeder der drei Dateien, einen Baum, der den Inhalt des Verzeichnisses auflistet und spezifiziert welcher Dateiname zu welchem Blob gehört, sowie einen Zeiger, der auf die Wurzel des Projektbaumes und die Metadaten des Commits verweist.

## Branching
Wenn Du erneut etwas änderst und wieder einen Commit machst, wird dieser einen Zeiger enthalten, der auf den Vorhergehenden verweist. Ein Branch in Git ist nichts anderes als ein simpler Zeiger auf einen dieser Commits. Der Standardname eines Git-Branches lautet master. Mit dem initialen Commit erhältst Du einen master-Branch, der auf Deinen letzten Commit zeigt. Mit jedem Commit bewegt er sich automatisch vorwärts. Was passiert, wenn Du einen neuen Branch erstellst? Nun, zunächst wird ein neuer Zeiger erstellt. Sagen wir, Du erstellst einen neuen Branch mit dem Namen testing. Das machst Du mit dem git branch Befehl. Woher weiß Git, welchen Branch Du momentan verwendest? Dafür gibt es einen speziellen Zeiger mit dem Namen HEAD.

### Beispiel-Workflow
1. Du arbeitest an einer Website
2. Du erstellst einen Branch für irgendeine neue Geschichte, an der Du arbeitest
3. Du arbeitest in dem Branch
In diesem Augenblick kommt ein Anruf, dass ein kritisches Problem aufgetreten ist und sofort gelöst werden muss. Du machst folgendes:
1. Schalte zurück zu Deinem "Produktiv"-Zweig
2. Du erstellst einen Branch für den Hotfix
3. Nach dem Testen führst Du den Hotfix-Branch mit dem "Produktiv"-Branch zusammen
4. Du schaltest wieder auf Deine alte Arbeit zurück und arbeitest weiter

## Merge
Angenommen Du entscheidest dich, dass Deine Arbeit an issue #53 getan ist und Du diese mit der master Branch zusammenführen möchtest. Das passiert, indem Du ein merge in die iss53 Branch machst, ähnlich dem merge mit der Hotfix Branch von vorhin. Alles was Du machen musst, ist ein checkout der Branch, in die Du das merge machen willst und das Ausführen des Kommandos git merge.
Bei Konflikten müssen diese – ähnlich wie bei anderen Systemen wie Subversion – manuell aufgelöst werden.

## Übliche Branches
Viele Git Entwickler verfolgen mit ihrem Workflow den Ansatz nur den stabilen Code in dem master-Branch zu halten – möglicherweise auch nur Code, der released wurde oder werden kann. Sie betreiben parallel einen anderen Branch zum Arbeiten oder Testen. Wenn dieser parallele Zweig einen stabilen Status erreicht, kann er mit dem master-Branch zusammengeführt werden. Es ist leichter sich die verschiedenen Branches als Arbeitsdepots vorzustellen, in denen Sätze von Commits in stabilere Depots aufsteigen, sobald sie ausreichend getestet wurden. Damit verändert Git häufig den ganzen Arbeitsansatz eines Entwicklers. Man macht sehr häufig Branches, in denen Dinge ausprobiert werden können. Man kann diese aber genauso schnell wieder verwerfen oder in einen stabileren Branch einbringen. Es ist nicht ungewöhnlich, mehrere Branches pro Stunde zu erzeugen und auch wieder zu löschen. Diese vielen Branches sind in Git einfach zu erstellen und zu handhaben. Sie sind aber eine Schwierigkeit für die Kontinuierliche Integration. Wie will ich kontinuierlich prüfen, ob alle Teile zusammenpassen, wenn sie über viele Branches verzweigt sind? Deshalb sind viele Projekte wieder zu sehr wenigen Branches übergangen. Das optimale Vorgehen ist hier noch unklar.

## Konfigurationen/Tags
Git kennt im wesentlichen zwei Typen von Tags: einfache (engl. lightweight) und kommentierte (engl. annotated) Tags. Ein einfacher Tag ist wie ein Branch, der sich niemals ändert – es ist lediglich ein Zeiger auf einen bestimmten Commit. Kommentierte Tags dagegen werden als vollwertige Objekte in der Git Datenbank gespeichert. Sie haben eine Checksumme, beinhalten Namen und E-Mail Adresse desjenigen, der den Tag angelegt hat, das jeweilige Datum sowie eine Meldung. Sie können überdies mit GNU Privacy Guard (GPG) signiert und verifiziert werden. Generell empfiehlt sich deshalb, kommentierte Tags anzulegen. Wenn man aber aus irgendeinem Grund einen temporären Tag anlegen will, für den all diese zusätzlichen Informationen nicht nötig sind, dann kann man auf einfache Tags zurückgreifen. So ein kommentierter Tag stellt dann eine Konfiguration dar.
![[Git Tag.png|300]]

## Synchronisation mit Server
Bisher verschwiegen habe ich, dass man meist nicht alleine auf einem lokalen Repository arbeitet, sondern dass man mit einem entfernten Repository auf einem Server synchronisiert. Dies passiert durch die beiden Befehle push und pull.
- pull zieht Daten von einem entferntem Repository auf das Lokale
- push schiebt die Daten vom lokalen Repository auf das entfernte