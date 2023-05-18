---
tags: Uni EST
VL-Date: 08.05.23
---
# Systemtests
Der Systemtest ist die Teststufe, bei der das gesamte System gegen die gesamten Anforderungen (funktionale und nicht-funktionale Anforderungen) getestet wird. Gewöhnlich findet der Test auf einer Testumgebung statt und wird mit Testdaten durchgeführt. Die Testumgebung soll die Produktivumgebung des Kunden simulieren, d. h. ihr möglichst ähnlich sein.“ https://de.wikipedia.org/wiki/Softwaretest#Systemtest Wir schauen uns im folgenden Beispiele an, was über [[Akzeptanztests]] hinaus sinnvoll auf Systemebene getestet werden kann.

1. Testing conducted on a complete, integrated system to evaluate the system's compliance with its specified requirements.

## Lasttest
![[Lasttest.png|300]]
Grundsätzlich lässt sich unterscheiden zwischen (1) Performanztests und (2) Lasttests. Performanztests wiederholen ausgewählte Testfälle bzw. Einzelprozesse aus dem Systemtest unter einer Grundlast: dadurch werden einzelne Funktionen auf ihre Performanzeigenschaften geprüft, wodurch die Skalierbarkeit für die Einzelfunktion(en) getestet wird. Lasttests im engeren Sinne testen gesamte Prozessketten (mehrere zusammenhängende Funktionen) auf Performanz, d. h. die Verknüpfungen der Einzelprozesse; damit simulieren sie konkrete Vorgänge aus der Nutzung. Auch hier ist die Skalierbarkeit von entscheidender Bedeutung, jedoch jetzt für die gesamte Prozesskette. Eine dabei häufige auftretende Fehlerwirkung sind Deadlocks beim Datenbankzugriff, die sonst nur schwer testbar sind.

Wird das System bewusst über die definierte Lastgrenze hinaus beansprucht, spricht man vom Stresstest. Dabei sollte die Last (Anzahl der virtuellen Nutzer*innen*) schrittweise bis über die definierte Lastgrenze hinaus erhöht werden.

Damit werden folgende Fragestellungen untersucht: 
• Wie ändert sich das Antwortzeitverhalten in Abhängigkeit von der Last? 
• Kann mit dem System auch unter hoher Last noch akzeptabel gearbeitet werden? 
• Zeigt das System undefiniertes Verhalten (z. B. Absturz)? 
• Kommt es zu Dateninkonsistenz? 
• Geht das System nach Rückgang der Überlast wieder in den normalen Bereich zurück?

## Usability-Test

Taskbeschreibung $\rightarrow$ Taskdurchführung (System under Test) $\rightarrow$ Auswertung (Video, Eye Tracking, Log-Dateien)

Es gibt eine sehr große Bandbreite an Möglichkeiten, was zum Test der Benutzbarkeit {Usability) eines Softwaresystems getan werden kann. Wir fokussieren uns hier auf den Test mit Nutzer*innen*. Für eine tiefergehende Behandlung empfehle ich das Modul „Mensch-Computer-Interaktion“. Hier konzentrieren wir uns also auf das Qualitätsattribut Benutzbarkeit. Viele Aspekte der Benutzbarkeit lassen sich erst sinnvoll auf der Systemebene prüfen. Deshalb kann es notwendig sein, im Systemtest systematische Evaluierungen mit (potenziellen) echten Nutzer*innen* zu machen. Diesen werden Taskbeschreibungen gegeben, die eine realistische erwartete Nutzung widerspiegeln. Diese führen die Test-Nutzer*innen* dann an unserem System aus. Dabei setzen wir verschiedene Messmethoden, wie Videos, Beobachtungen, Eye Tracking oder einfach das Aufzeichnen der Benutzung in Log-Dateien ein. Daraus können dann Rückschlüsse auf die Benutzbarkeit gezogen werden.

## Sicherheitstest
White Hat Hacker $\rightarrow$ Angriffsdurchführung (System under Test) $\rightarrow$ Dokumentation der Schwachstellen (Log-Dateien)

Sicherheitstests beziehen sich hier auf die Informationssicherheit. Diese sollten nicht erst auf Systemebene ansetzen. Viele Aspekte lassen sich bereits auf kleineren Einheiten prüfen. Es ist aber sinnvoll auf der Systemebene nochmals intensiv nach Sicherheitslücken zu suchen. Auch hier verweise ich auf spezialisierte Veranstaltungen, insbesondere das Modul „System- und Websicherheit“.
„Sicherheitstests haben eine andere Fragestellung als die meisten der übrigen, allgemeinen [[Tests]], weil sie den Nachweis erbringen sollen, dass eine Software keine Funktionen enthält, die sie nicht enthalten soll. Daher handelt es sich bei Sicherheitstests meistens um sogenannte Negativtests. Weiterhin sollen Sicherheitstests den Beweis erbringen, dass keine unsicheren Nebeneffekte in einem Programm vorhanden sind, weil bereits ein einzelner Fehler ausreicht, um das gesamte Programm zu kompromittieren.“ https://de.wikipedia.org/wiki/Sicherheitstest_(Software) 
Ein üblicher Ansatz ist hier das Penetrationstest, d.h. ein*e* Tester*in* simuliert einen böswilligen Angreifer und versucht Lücken zu entdecken, mit denen sie das System kompromittieren können.