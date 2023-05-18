---
tags: Uni EST
VL-Date: 15.05.23
---
# Frage des Tages
Was unterscheidet Continuous Integration, Continuous Delivery und Continuous Deployment?

# Integration
## Software Bauen
Das Bauen der Software besteht aus dem Übersetzen, Linken der Teile der Software und Bibliotheken und eventuell weiteren Schritten, wie statischer Analyse, Ausführung von automatisierten Tests, Verteilung auf die Test- oder Zielmaschinen bis hin zur Installation.
### Automatisches Bauen
Wegen der Komplexität der Zusammenhänge und notwendigen Schritte sowie zur Sicherstellung der Wiederholbarkeit, wird das Bauen der Software heute quasi immer automatisiert. Dazu verwendet man typischerweise ein sogn. __Build Script__, das die Schritte und Konfigurationen beschreibt.

#### Werkzeuge zur Automatisierung
Apache Ant, Make, Maven, Gulp.js, Rake, Grunt, Gradle
Über die Jahrzehnte wurde eine große Bandbreite an Werkzeugen hierfür entwickelt. Der Großvater aller dieser Werkzeuge ist Unix Make. Die neueren Werkzeuge versuchen Make auf verschiedene Arten zu verbessern. Einige spezialisieren sich auf eine Programmiersprache. Andere unterstützen verschiedene Sprachen.

##### Gradle
Durch gradle init kann man ein leeres Projekt erzeugen.
![[Gradle.png|250]]
![[GradleCode.png|250]]

Hier sieht man ein Skript, das durch die Initialisierung für eine Java-Applikation erzeugt wurde. Es bindet ein passendes Plugin ein, das Tasks zum Kompilieren und Testen einer Java-Applikation zur Verfügung stellt. Gradle kann außerdem automatisch Abhängigkeiten in Form von Bibliotheken herunterladen und linken. Dazu definiert man, welches Repository verwendet wird (hier: Maven Central). Weiterhin ist die zu verwendende Java-Version definiert, zwei Abhängigkeiten voreingestellt und die Hauptklasse, die beim Start der Applikation ausgeführt werden soll, wird festgelegt.

## Kontinuierliche Integration
Integration: process of combining software components, hardware components, or both into an overall system

### Architektur eines Bankautomaten
![[BankautomatArchitektur.png|200]]
#### Teilintegriertes System
![[BankautomatArchitekturTeilintegriertesSystem.png|250]]
Solange das System noch nicht vollständig integriert ist, wird das Ergebnis jedes Integrationsschritts als teilintegriertes System bezeichnet. Typisches Problem der Integration: Inkompatible Schnittstellen (syntaktische und semantische Konflikte durch unterschiedliches Verständnis der Spezifikation und durch Schlamperei oder – weit schlimmer – durch das Fehlen einer Spezifikation) Darum wird das teilintegrierte System vor jeder Verwendung und weiteren Integrationen getestet und korrigiert (Integrationstest).

### Big-Bang-Integration
__positiv__: keine Testtreiber und Platzhalter, sofort vollständiges System
__negativ__: System wahrscheinlich nicht lauffähig, Fehler nur auf Systemebene
- Im Prinzip sehr attraktiv, denn Test Double sind nicht notwendig
- Nach der Integration ist das System vollständig und kann ohne Hilfsmittel getestet werden
In der Praxis kaum möglich, weil die Komponenten zu viele Fehler und Inkonsistenzen enthalten; das System ist kaum ausführbar, die Probleme lassen sich in einem großen, den Beteiligten kaum bekannten System nicht zuordnen.

## Continuous Integration
![[ContinuousIntegration.png|300]]

Kontinuierliche Integration (Continuous Integration, CI) ist eine laufende (typisch tägliche) Integration auf dem (von den Entwicklungsumgebungen getrennten) Integrationsrechner (CI-System). Die Integration wird zu einem fortlaufenden Prozess. Sobald eine neue Komponente fertig oder eine bereits vorhandene modifiziert ist, wird sie integriert und getestet. Nur wenn der Test keine Fehler zeigt, bleibt der neue Code auf dem Integrationsrechner. Hier können neben Tests auch weitere Qualitätsanalysen, wie statische Analysen, kontinuierlich ausgeführt werden. Ein Beispiel für einen CI-Server, der heute sehr häufig eingesetzt wird ist Jenkins (jenkins-ci-org).

## CI Pipeline
Build $\rightarrow$ Unit-Test $\rightarrow$ Integrationstest $\rightarrow$ Systemtest $\rightarrow$ Akzeptanztest
Man spricht oft von einer CI Pipeline, die in der kontinuierlichen Integration durchlaufen wird. Dabei teilt sich die Pipeline in Stufen („Stages“) auf. Die Regel hinter der Reihenfolge ist dabei „Fail fast“, also wenn etwas schief geht, sollte es möglichst früh schief gehen. Dadurch hat man möglichst schnell eine Rückmeldung und kann die Software daraufhin verbessern. Man könnte beispielsweise sehr aufwändige Performanz- und Stresstests noch hinter die Akzeptanztests schieben, damit sie nur ausgeführt werden, wenn alles andere geklappt hat.

## Risiken, die durch kontinuierliche Integration reduziert werden
##### keine auslieferbare Software
- "Works on my machine"
- Datenbank-Synchronisation
- Manuelles Anstossen
##### späte Fehlerentdeckung
- Regressionstests
- Testüberdeckung
##### fehlende Sicht auf Projektstatus
- "Did you get the Memo?"
- keine Visualisierung der Software
##### niedrige Softwarequalität
- Einhaltung von Codier-Standards
- Einhaltung der Architektur
- duplizierter Code

