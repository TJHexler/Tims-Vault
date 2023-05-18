---
tags: Uni EST
VL-Date: 25.04.23
---
# Verzweigungsmuster: Basis
Die Informationen basieren auf den Mustern vorgeschlagen von Martin Fowler (https://martinfowler.com/articles/branching-patterns.html).

## Source Branching
#### Problem
mehrere Entwickler können nicht gleichzeitig an einem Dokument arbeiten
#### Lösung
Zweige (Branches)
Diese Verzweigungen erlauben das parallele Arbeiten, aber man kauft sich damit das Problem des Zusammenführens ein, das nicht immer trivial ist.

## Mainline
#### Problem
welchen Zweig soll ich auschecken, um mit dem Projekt zu starten? Wie gebe ich meine Änderungen an alle anderen weiter?
#### Lösung
Es gibt einen Hauptzweig (__Mainline__), der immer den aktuellen Stand enthält, der von allen als offiziell für alle verfügbare Version gilt.

## Healthy Branch
#### Problem
Zweige werden potentiell zwischen Entwicklern geteilt, aber in Zweigen kann viel "Work in Progress" sein, der noch unvollständig und ungetestet ist.
#### Lösung
Die Zweige sollten immer "gesund" sein, d.h. durch automatische Prüfungen ständig abgesichert werden. Dies beinhaltet automatisierte [[Tests]] und statische Analysen. Dies kann auf beliebige Zweige angewendet werden, ist aber gerade mit einer Mainline sinnvoll.

# Verzweigungsmuster: [[Integration]]
Die folgenden Infos n basieren auf den Mustern vorgeschlagen von Martin Fowler (https://martinfowler.com/articles/branching-patterns.html).

## Mainline Integration
#### Problem
Wie integriere ich meine Änderungen mit denen der anderen Entwickler?
#### Lösung
Alle integrieren "gesunde" Stände in die Mainline.

Ein großer Vorteil dieses Musters ist, dass ich Kontinuierliche [[Integration]] einfach auf der Mainline machen kann.

## Feature Branch
#### Problem
Wie entwickle ich an einem Feature ohne die anderen im Team mit anfertigen Zwischenlösungen zu stören?
#### Lösung
Features werden in eigenen Branches bearbeitet.
![[Feature Brach.png|300]]

Erst wenn das Feature fertig ist, wird es in die Mainline integriert. Zwischendurch kann ein/e Entwickler/in sich neue Stände von der Mainline holen. Wenn ein/e Entwickler/in gleichzeitig an mehr als einem Feature arbeitet, erzeugt er/sie jeweils einen eignen Zweig. Bei sehr langlebigen Feature Branches ist kontinuierliche Integration erschwert.

## Continuous Integration
#### Problem
Wie häufig soll ich in die Mainline integrieren?
#### Lösung
So oft wie möglich (alle paar Commits, mindestens einmal am Tag) in die Mainline integrieren

Der eigentliche Gegensatz ist nicht [[Integration]] in die Mainline vs. Feature Branch sondern häufiges vs. seltenes Integrieren in die Mainline. Sehr häufiges Integrieren führt dazu, dass man sich oft mit Merge-Konflikten beschäftigen muss, weil ich ja bei jeder Mainline-Integration potentiell so einen Konflikt haben kann und lösen muss. Je länger aber diese Integration herausgeschoben wird, desto risikoreicher und aufwändiger wird sie.

## Peer-Review Commit
#### Problem
Wann und was genau soll in ein Code Review?
#### Lösung
Jeder Commit in die Mainline wird in einem Review geprüft.

Code Review ist eine sehr wichtige und, überraschenderweise, relativ effiziente Methode, um Code zu verbessern und Fehler zu vermeiden. Die einfachste Form ist der Peer Review, in dem einfach ein/e Kolleg/in meinen Code nach Problemen untersucht. Aber wann macht man das am besten? Jeder Commit in die Mainline ist ein guter Zeitpunkt, da dann typischerweise etwas abgeschlossen ist und wir für die Mainline auf alle Fälle einen Healthy Branch wollen. Dies lässt sich sehr einfach mit Feature Branches kombinieren, aber im Prinzip auch mit Continuous Integration.

# Verzweigungsmuster: Auslieferung
Die folgenden Infos n basieren auf den Mustern vorgeschlagen von Martin Fowler (https://martinfowler.com/articles/branching-patterns.html).

## Release Branch
#### Problem
Wie bekomme ich eine Software-Version, die stabil genug für eine Auslieferung ist?
#### Lösung
Wir erstellen einen separaten Release Branch in den keine neuen Features mehr kommen, sondern nur Commits zur Stabilisierung (wie z.B. Fehlerbehebung).

Dies erlaubt auch mehrere Release Branches parallel zu haben, wenn Kund/innen noch alte Software-Versionen am Laufen haben. Es kann aber relativ schwer sein, die Änderungen im Release Branch dann wieder in die Mainline zu bekommen.

## Maturity Branch
#### Problem
Wie gehe ich mit Softwareständen auf verschiedenen Reifegraden um?
#### Lösung
Erstelle mehrere Ebenen von Branches je nach Reife

Das wird in der Praxis öfter eingesetzt. Der Nutzen ist aber eingeschränkt. Eine Alternative wären entsprechende Tags.

![[Maturity Branch.png|300]]