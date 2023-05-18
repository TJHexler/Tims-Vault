---
tags: Uni EST
VL-Date: 15.05.23
---
# Continuous Delivery and Deployment
How long would it take your organization to deploy a change that involved just one single line of code? Do you do this on a repeatable, reliable basis?

## Deployment
- Phase of a project in which a system is put into operation and cutover issues are resolved.
„Cutover“ ist von einer alten Systemversion auf eine neuere zu aktualisieren, also den Betrieb von einer Version auf eine andere umzustellen.

## Release
- Particular version of a configuration item that is made available for a specific purpose
- Collection of new or changed configuration items that are tested and introduced into a live environment together
Wir hatten ein Release schon mal als eine bestimmte Konfiguration in der Konfigurationsverwaltung kennengelernt.

### Häufige Releases?
Es war früher üblich Releases eher selten zu machen. Dies war erstens der damals aufwändigen Verteilung per Diskette, CD oder DVD geschuldet, aber zweitens auch ein aufwändiger und fehleranfälliger Prozess. Das Zusammenstellen eines Releases sollte möglichst vermieden werden. Durch die Installation dieser dann immer sehr großen Änderungen war auch das Risiko, das etwas schief geht groß. Deshalb ist die Gegenstrategie „If it hurts, do it more often!“ Der Vorschlag ist viele sehr kleine Releases zu machen. Durch die kleinen Änderungen ist das Risiko nur sehr klein. Damit dies möglich wird, muss der Release aber weitgehend automatisiert werden. Dies hat den angenehmen Nebeneffekt, dass das Zusammenstellen eines Releases und dessen Deployment aufgeschrieben und versioniert werden und damit wiederum der Qualitätssicherung unterworfen werden kann.

## Continuous Delivery
Build $\rightarrow$ Unittest $\rightarrow$ Integrationstest $\rightarrow$ Systemtest $\rightarrow$ Akzeptanztest
Ersten 3 automatisiert in Build-Umgebung, die beiden letzten automatisiert in Staging-Umgebung
Manuelles Deployment in Produktions-Umgebung

Continuous Delivery erweitert Continuous [[Integration]], in dem es fordert, dass jede Änderung nicht nur gebaut und getestet wird. Darüber hinaus werden intensive automatisierte Tests in einer produktionsnahen „Staging“- Umgebung durchgeführt und alle Ergebnisse, also Binaries und Berichte („Artefakte“) archiviert und alles was ausgeliefert werden muss zu deploy-fertigen Paketen zusammengestellt. Letzteres könnten in Java beispielsweise JAR-Dateien sein. In anderen Kontexten könnten es NPM-Dateien, Docker-Images oder PyPI Packages sein. Der letzte Schritt, die Installation auf der Zielumgebung, wird dann aber manuell ausgeführt.

#### Nutzen von Continuous Delivery
- bei jeder Änderung schnelles, automatisiertes Feedback zur Produktionsreife der Software
- Releases hängen nur noch von Geschäftsanforderungen ab, nicht Einschränkungen aus Entwicklung oder Betrieb
Die Änderung kann am Code, den Konfigurationen oder der Infrastruktur passieren. In jedem Fall bekomme ich eine Rückmeldung, ob die Software in die Produktionsumgebung gehen kann.

## Continuous Deployment
- fügt Continuous Delivery das direkte, automatische Deployment in die Prokutionsumgebung hinzu
- extrem schnelle Rückmeldung zu Änderung und damit Möglichkeit zu experimentieren

![[ContinuousDeployment.png|300]]

Grafik angelehnt an Jez Humble, David Farley. Continuous Delivery. Addison-Wesley, 2011. UAT = User Acceptance Test Wir sehen hier eine etwas ausgereiftere Deployment Pipeline mit großen Stufen, die wiederum kleinere Schritte enthalten. In der Commit-Stufe behandeln wir alles was direkt mit dem Quellcode zu tun und in der reinen Build-Umgebung erledigt werden kann. Wir übersetzen den Quellcode aus der Versionskontrolle, führen alle Tests aus, die in dieser Umgebung ausgeführt werden können (vor allem Unit- und Integrationstests, evtl. einige Systemtests). Wir stellen die Binaries zusammen und Analysen den Code auf Probleme. Alle Ergebnisse werden in einem Artefakt Repository (z.B. Nexus, Maven, Artifactory) gespeichert. Dies ist bewusst getrennt von der normalen Versionskontrolle, da Git und ähnliche Systeme nicht darauf ausgelegt sind, große Binärdateien zu versionieren. Für die Akzeptanzstufe holen wir uns Umgebungs- und Anwendungskonfigurationen aus der Versionskontrolle. Wir bauen eine Akzeptanzumgebung auf, deployen die Binaries hier und führen Smoke Tests aus. Smoke Tests sind einfache Tests, die schnell zeigen, ob die Binaries überhaupt sinnvoll lauffähig sind. Auch hier ist das Ziel wieder möglichst schnelles Feedback. Danach führen wir die automatisierten Akzeptanztests (z.B. aus BDD) aus. Bericht und Metadaten kommen wieder ins Artefakt-Repository. Danach können wir potentiell parallele Stufen durchführen. Eine Möglichkeit sind User Acceptance Tests, also Akzeptanztests, die direkt von Usern oder Expert*innen* am System manuell ausgeführt werden. Auch hier schalten wir wieder Smoke Tests vor, um unnötige Arbeit zu vermeiden. In der Kapazitätsstufe werden nichtfunktionale Anforderungen getestet, wie beispielsweise Lasttests oder Kapazitätstests. Schließlich können wir auch direkt in die Produktion deployen. Bei allen diesen Stufen kommen die Binaries aus dem Artefakt Repository und Berichte und Metadaten fließen dorthin zurück.

## Automotive Deployment Pipeline
![[automotiveDeploymentPipeline.png|300]]
ECU = Electronic Control Unit, Steuergerät

