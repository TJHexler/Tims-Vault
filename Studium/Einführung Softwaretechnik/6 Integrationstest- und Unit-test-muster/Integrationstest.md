---
tags: Uni EST
VL-Date: 09.05.23
---
# Integrationstests
- Testing in which software components, hardware components, or both are combined and tested to evaluate the interaction among them.
Hier geht es nicht um die Fehler der einzelnen Komponenten (Modul-/Unittest), sondern um Konsistenzprobleme zwischen den Komponenten. Falls wir es schaffen würden, perfekte Unit-Tests zu bauen, dann würden nur noch Schnittstellenfehler zwischen den Modulen durch Integrationstests identifiziert werden. Beispielsweise könnten dies falsche Anordnungen von Aufruf- und Return-Abfolgen oder inkonsistente Behandlung von Datenobjekten sein (vgl. B. Beizer. Software Testing Techniques. Second Edition. Van Nostrand Reinhold, 1990).

## Test Automation Pyramid
Unittests $\rightarrow$ Integrationstest $\rightarrow$ Akzeptanztests Systemtests
Die Test-Automatisierungs-Pyramide wurde von verschiedenen Autoren verwendet und ausgebaut. Die erste noch sehr simple Version stammt aus M. Cohn. Succeeding with Agile. Addison Wesley, 2010. Es stellt visuell dar, dass auf der Unittest-Ebene die meisten automatisierten Tests vorhanden sein sollten, weniger auf der Integrationstest-Ebene und noch weniger auf der Systemtest- und Akzeptanztest-Ebene. Vor allem auf letzterer kommen auch manuelle Tests hinzu. Auf allen Ebenen kann manuell explorativ getestet werden. Besonders auf der Integrationstest-Ebene erfolgt die Automatisierung meist durch Unit-Testframeworks, wie JUnit. Man kann es also auch allgemein als grobe Einschätzung der Quantität von Testfällen auf den Ebenen verstehen.

## klassische Integrationstests

![[IntegrationstestIntegrationsschritte.png|300]]

Obwohl das prinzipielle Ziel der Entdeckung von Problemen im Zusammenspiel von Units intuitiv verständlich ist und auch heute relevant bleibt, ist es nicht mehr ganz klar, für welche Interaktionen von Units Integrationstests geschrieben werden sollen. Klassisch war der Integrationstest ein Teil der [[Integration]]. Dabei wurden Units Schrittweises zu größeren Einheiten zusammengesetzt. In jedem Schritt wurden die Tests verwendet, um die gerade zusammengesetzten Units zusammen zu verifizieren. Es gab hier viele Diskussionen, was die beste Strategie für diese schrittweise Integration ist und wie Tests hier effizient eingesetzt werden können. Leider passt dies so aber nicht mehr zu modernen Praktiken der kontinuierlichen Integration, die wir im Kapitel „Integration“ kennenlernen werden. Im Beispiel würden die Units Datenhaltung und Kommunikation zuerst integriert. Der Fokus liegt auf deren Interaktion. Der Rest des Systems wird durch ein Mock-Objekt ersetzt. Im nächsten Schritt könnten dann die Geschäftslogik mit der Datenverwaltung integriert und getestet werden usw.

### Integrationstests als Komponententests
In mancher Literatur wird der Komponententest als Test von größeren Komponenten gesehen, die schon mehrere Units umfassen (J. Gregory, L. Crispin. More Agile Testing. Addison-Wesley, 2015). Hier ist eine Komponente beispielsweise ein Service, JAR, DLL o.ä. Der Integrationstest ist dann in dieser Bedeutung ein Komponententest, der das Zusammenspiel der Units innerhalb dieser Komponente verifiziert. Dies erlaubt damit die klare Auswahl welche Interaktionen in jeder Iteration getestet werden müssen. Es bedarf dann aber auch Tests, die das Zusammenspiel der Komponenten überprüfen. Je nach Systemgröße und -Komplexität sind dazu aber evtl. Systemtests ausreichend.

### Integrationstests als Funktionstests
Hier verwenden wir die Funktionalitäten oder Features eines Systems als Grundlage für Integrationstests. Typischerweise bewegen wir uns auf der API- oder Service-Ebene (API steht für Application Programming Interface), also an der Schnittstelle, die unsere Komponenten „nach außen“ anbieten. Besonders wird hier typischerweise die graphische Benutzeroberfläche (GUI) ausgespart, um schnelle und robuste Tests zu ermöglichen. Tests durch die GUI werden tendenziell mehr auf der Akzeptanz- und Systemtest-Ebene gemacht. Hier identifizieren wir eher Funktionen (die wir beispielsweise aus User Stories ableiten) und prüfen, ob die Komponenten und Units in der Erfüllung der Funktion gut zusammenspielen. Auch hier prüfen wird das nach jeder Änderung. Man spricht hier auch von Regressionstests.