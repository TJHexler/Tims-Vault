---
tags: Uni EST
VL-Date: 24.04.23
---
# Frage des Tages
Warum ist die Disziplin "[[Software Engineering]]" entstanden?

# Anforderungsanalyse und Spezifikation
## Anwendungsfälle
### Use Case
A sequence of interactions between an actor (or actors) and a system triggered by a specific actor, which produces a result for an actor.
Wesentliche Merkmale eines Anwendungsfalls (AF, engl. Use Case) sind:
- Neben dem System ist immer mind. eine Akteurin (actor) beteiligt. (=Rolle eines mit dem System interagierenden Benutzerin oder eines externen Systems)
- Anstoß durch ein spezielles Ereignis (einen Trigger), das eine Akteurin – der/die Hauptakteurin – auslöst.
- Ein AF ist zielorientiert, der/die Akteurin möchte das Ziel erreichen.
- Ein AF beschreibt alle Interaktionen zwischen dem System und den beteiligten Akteurinnen.
- Ein AF endet, wenn das angestrebte Ziel erreicht ist oder wenn klar ist, dass es nicht erreicht werden kann.
#### Beispiel
![[UseCaseAnwendungsbeispiel.png|350]]
Anwendungsfälle beschreiben also aus der Außensicht, was das System leisten soll und welche Interaktionen dazu notwendig sind. Jeder Anwendungsfall muss das Systemverhalten für eine konkrete Situation vollständig spezifizieren (inkl. Ausnahmefälle).
Charakteristisch:
- Formaler Aufbau nach Vorgaben eines Formulars mit bestimmten Standardfeldern (Name, Ziel, Vor-/ Nachbed., Akteurinnen)
- Normalablauf (normal = Ziel wird erreicht)
- Sonder- und Ausnahmefälle
- Klarheit über den aktiven Teil (Akteur oder System)
#### Normalablauf
1. Der Kunde führt eine Karte ein
2. Der Bankautomat liest die Karte und sendet die Daten zur Prüfung ans Banksystem
3. Das Banksystem prüft ob die Karte gültig ist
4. Der Bankautomat zeigt die Aufforderung zur PIN-Eingabe
5. Der Kunde gibt die PIN ein
6. Der Automat liest die PIN und sendet sie zur Prüfung an das Banksystem
7. Das Banksystem prüft die PIN
8. Der Bankautomat akzeptiert den Kunden und zeigt das Hauptmenü
#### Sonderfälle
Sonderfall 2a: Die Karte kann nicht gelesen werden
2a.1 Der BA42 zeigt die Meldung "Karte nicht lesbar"
2a.2 Der BA42 gibt die Karte zurück
2a.3 Der BA42 zeigt die Willkommen-Botschaft

Sonderfall 2b: Die Karte ist lesbar, aber keine BA42-Karte
2b.1 Der BA42 zeigt die Meldung "Karte nicht akzeptiert"
2b.2 ...

### Anwendungsfalldiagramm
![[Anwendungsfalldiagramm.png|350]]

Aus fachlicher Sicht hat es sich bewährt, zwischen Hauptfunktionen und Basisfunktionen zu unterscheiden. Hauptfunktionen beschreiben die geforderte fachliche Funktionalität des Systems. Basisfunktionen werden typisch in Hauptfunktionen verwendet und liefern dort einen Beitrag zur Funktionalität. Die Akteure stehen außerhalb des modellierten Systems. Die Anwendungsfälle sind als Pakete gruppiert und durch Beziehungen (include und extend) miteinander verknüpft. »Kontostand abfragen«, »Auszug drucken«, »Geld beziehen« und »Dauerauftrag einrichten« spezifizieren Hauptfunktionen. »Authentifizieren« beschreibt eine Basisfunktion (wird in jeder Hauptfunktion verwendet); darum ist er durch eine include-Beziehung eingebunden. Eine Ausnahme bildet der AF »Auszug drucken«, er kann direkt oder aus dem AF »Kontostand abfragen« in Anspruch genommen werden (über den Erweiterungspunkt »Auszug drucken«).
Bewertung: 

| positiv                                                                       | negativ                                                           |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| zeigt, welche Akteure in welchen Anwendungsfällen mit dem System interagieren | modelliert Zusammengänge zwischen Anwendungsfällen nur rudimentär |
| bei kleinen Modellen sehr übersichtlich                                       | modelliert die eigentlichen Inhalte der Anwendungsfälle nicht                                                                  |

## Anwendungsfälle
- werden durch Use-Case-Diagramme im __Überblick__ dargestellt
- werden __iterativ__ identifiziert, modelliert, formuliert und geprüft
- können nur in enger Zusammenarbeit mit dem Klienten erstellt werden. Sie sind als Kommunikationsmedium besonders geeignet, um die Ist- und Soll-Abläufe mit den Fachleuten zu diskutieren und abzustimmen
- helfen den Entwicklern, die Welt der Anwendung zu verstehen (und Kandidaten für das Begriffslexikon zu erkennen)
- sind eine gute Grundlage für Prototypen, Testfälle und die Benutzungsdokumentation