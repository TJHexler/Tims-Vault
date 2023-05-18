---
tags: Uni EST
VL-Date: 08.05.23
---
# [[Akzeptanztests]]
Wir haben bei den User Storys direkt die Verbindung zu den [[Akzeptanztests]] kennengelernt. Dieser enge Zusammenhang zwischen Anforderung und Test ist schon lange ein bewährtes Mittel, um klare Anforderungen zu spezifizieren, die testbar sind und von denen möglichst eindeutig bestimmbar sind, wann sie erfüllt sind. Eine Anforderung brauch also Tests und Tests brauchen Anforderungen. Deshalb werden wir im folgenden genauer auf das Testen als zentrales Mittel der Qualitätssicherung in im Software Engineering eingehen.

# Testen
Testen ist die Ausführung eines Programms auf dem Rechner unter Bedingungen, für die das korrekte Ergebnis bekannt ist, so dass Ist- und Sollresultat verglichen werden können; stimmen sie nicht überein, so liegt ein Fehler vor. Die Entdeckung von Fehlern ist der Zweck des Tests, ein Testfall ist gut, wenn er hohe Chancen hat, Fehler anzuzeigen. Werden Fehler angezeigt, so war der Test erfolgreich (vgl. positiven und negativen Befund in der Medizin). Die Testsituation soll die Einsatzsituation so simulieren, dass aus einem erfolglosen Test auf einen erfolgreichen Einsatz geschlossen werden kann. Beachte: Test erfolgreich bedeutet Programmierer erfolglos (und umgekehrt). Denn __Testen ist destruktiv__.

## Vorteile
- Testen is ein natürliches Prüfverfahren
- Der Test ist (u.U.) reproduzierbar und damit objektiv
- Test lässt sich , einmal gut organisiert, sehr billig wiederholen
- Zielumgebung (Übersetzer, BS usw.) wird mitgeprüft
- Systemverhalten wird sichtbar gemacht
## Nachteile
- Aussagekraft des Tests wird überschätzt, zeigt nicht Korrektheit, denn schon die Zustandsräume kleiner Programme sind riesig
- Man kann nicht alle Anwendungssituationen nachbilden
- Der Test zeigt die Fehlerursache nicht
$\rightarrow$ Darum kann der Test andere Arten der Verifikation, insbesondere das Review, nur ergänzen, nicht ersetzen.

## Testgegenstand: Prüfling
Der Prüfling entsteht aus dem Quellprogramm er enthält direkt oder indirekt die Umgebung.
Klassifizierung nach der Komplexität: 
- Einzeltest: Programmeinheiten, z.B. Funktionen, Unterprogramme
- Test von Programmkomponenten, z.B. „package“, „module“
- [[Systemtest]]: komplettes System; Sonderfall: Abnahme. 
In der Praxis geht man beim Testen in der Regel bottom-up vor, d.h. vom Einzeltest zum [[Systemtest]].

## zwei Formen der Ausführung
__Automatisierte Tests__: Häufige Ausführung, Regressionsfehler
__Explorative Tests__: Manuell, kreativ, neue Fehler
Im wesentlichen Unterscheiden wir heute zwischen zwei Formen der Testausführung. Die weitaus meisten Tests werden automatisiert und dann häufig und regelmäßig ausgeführt. Diese bringen Sicherheit für die Entwickler und helfen Regressionsfehler zu entdecken, also Fehler, die durch Änderungen an vorher funktionierenden Einheiten eingeführt wurden. Im explorativen Test arbeitet man manuell und versucht sich kreativ neue Szenarien zu überlegen, in denen die Software fehlschlagen könnte. Gerade bei neuen Features ist dies wichtig. Wenn Fehler gefunden werden, sollten diese mit einem automatisierten Test abgesichert werden.

## Teststufen
Unit/Modul $\rightarrow$ [[Integration]] $\rightarrow$ System/Akzeptanz
Wir unterscheiden vier Teststufen: 
1. Unit- oder Modultest bedeutet, dass einzelne Einheiten (Klassen, Module) separat getestet werden. 
2. Im Integrationstest werden die einzelnen Einheiten sukzessive zu größeren Einheiten kombiniert. In dieser Phase finden wir Schnittstellenfehler im Zusammenspiel der integrierten Einheiten. 
3. Im [[Systemtest]] testen wir dann das komplett integrierte System in der Produktionsumgebung oder in einer Testumgebung, die sehr ähnlich der Produktionsumgebung ist. Hier testet man komplette Funktionalitäten und insbesondere Eigenschaften, die nur auf dem Gesamtsystem möglich sind, wie z.B. bei Performanz- oder Sicherheitstests. 
4. Der Akzeptanztest wird üblicherweise vom Kunden durchgeführt nachdem das System in der Produktionsumgebung installiert wurde.
## Tests getrieben durch
Anforderungen, Struktur, Statistik, Risiko
Nach Glass (2009) unterscheiden wir vier Klassen an Treibern für die Spezifikation von Tests: 
1. Tests können durch Anforderungen getrieben sein. Wir verwenden die Anforderungsspezifikation, um Testfälle abzuleiten. Üblicherweise hat man dabei das Ziel alle Anforderungen abzudecken. -> Black-Box Tests 
2. Test können durch Struktur getrieben sein. Hauptsächlich verwenden wir dabei die interne Struktur des Quelltexts mit dem Ziel verschiedene Aspekte dieser Struktur abzudecken. -> Glass-Box Tests 
3. Tests können durch Statistik getrieben sein. Die Eingaben, die in den Testfällen verwendet werden sind durch statistische Methoden ermittelt worden. Sie folgen beispielsweise einer statistischen Verteilung oder sind zufällig. 
4. Tests können durch Risiko getrieben sein. Die betrachteten Risiken können sehr unterschiedliche sein. Beispielsweise könnte dies finanzielle Risiken von Fehlern sein oder hohe Verwendung bestimmter Funktionalität.
## Bsp.: Fakultät-Funktion
Beispiel: Ein Programm, das die Fakultät von n berechnen soll, muss (1) negative Zahlen, (2) echte Brüche, (3) Zahlen, deren Fakultät zu groß ist, sowie (4) syntaktisch falsche Eingaben ablehnen. Sonderfall: 0! ergibt mit dem „Normalfall“ insgesamt sechs Klassen. Die Menge aller möglichen Eingaben wird analysiert und zergliedert. (Das geschieht in der Praxis freilich nicht mit einer Grafik!) Schließlich gelangt man zu einer relativ feinen Gliederung. Die meisten Teilgebiete repräsentieren Fehlerfälle. Nach dem Prinzip der Äquivalenzklassen genügt pro Klasse ein Testfall. Natürlich gehört zu jedem Testfall ein Soll-Resultat. Niemand kann sicher sein, alle Klassen erkannt zu haben. Wurde eine Klasse übersehen, so verfehlt der Test möglicherweise sein Ziel. Im gezeigten Beispiel wurde übersehen, dass es neben der Klasse „zu groß“ noch eine Klasse „viel zu groß“ gibt.

## Vorgehen
1. Eingabegrößen, Bereiche Äquivalenzklassen gültiger und ungültiger Eingaben
2. Evtl. intuitiv Klassen weiter teilen
3. für jede Klasse Eingabedaten wählen, Sollresultate ermitteln

Äquivalenzklassen nach Myers (1979): _Wenn es Gründe für die Annahme gibt, dass das Programm mit zwei verschiedenen Startzuständen s1 und s2 gleiches Verhalten zeigt, also mit beiden Werten korrekte oder mit beiden Werten falsche Ergebnisse liefert, dann sind s1 und s2 äquivalent, und nur einer der beiden muss getestet werden._

Die Menge der Startzustände kann also in Äquivalenzklassen zerlegt werden. Aus jeder Klasse muss (mind.) ein Wert getestet werden. Die Äquivalenzklassen werden intuitiv identifiziert (heuristisch). In der Regel werden Klassen übersehen, sonst wäre das Verfahren „wasserdicht“. Man sollte daher lieber eine Klasse zu viel als eine zu wenig unterscheiden, wenn es denkbar scheint, dass ein Fall spezielle Reaktionen hervorruft. Jede Äquivalenzklasse der Eingabedaten muss in (mindestens) einem Testfall berücksichtigt sein. Die Erfahrung zeigt, dass Grenzwerte speziell berücksichtigt werden sollten, und zwar – soweit möglich – von beiden Seiten her.

Zur noch besseren Absicherung sollten neben einem repräsentativen Vertreters einer Äquivalenzklasse auch deren Grenzen durch Grenzwerte getestet werden. Üblicherweise verwendet man einen Wert unter, auf und über der Grenze. Im Beispiel haben wir den Grenzfall 12. Also sollten wir neben 12 auch 11 und 13 abtesten. Der Grund für die Effektivität von Grenzwerttests liegt darin, dass man in der Programmierung gerade Grenzfälle oft nicht richtig implementiert, indem man beispielsweise „>“ statt „≥“ verwendet.

## Glass-Box-Test: Überdeckung
Vollständigkeit im Sinne von „alle Kombinationen aller Eingabedaten und Anfangszustände“ ist unerreichbar. Bescheidenere Vollständigkeitskriterien, z.B. Ausführung aller Befehle, Aufruf aller Unterprogramme, können u.U. erfüllt werden. Der erreichte Grad der Vollständigkeit wird als Überdeckung (in Bezug auf ein bestimmtes Kriterium) bezeichnet; er liegt stets im Bereich von 0 bis 1 (oder 100 %). Der Wert 1 kennzeichnet die vollständige Überdeckung. Anmerkungen: 
• Es gibt viele verschiedene, verschieden gute Überdeckungskriterien. 
• Auch eine vollständige Überdeckung (welche auch immer) ist kein Korrektheitsbeweis!

- Befehlsüberdeckung
- Zweigüberdeckung
- Termüberdeckung
- Pfadüberdeckung

![[TestÜberdeckungen.png|100]]
Dem Glass-Box-Test (GBT) liegt der Ablaufgraph des Programms (d.h. sein Flussdiagramm) zu Grunde. Achtung, auch dieser wird nicht gezeichnet oder erzeugt!
- Befehlsüberdeckung: A, B, C, D müssen ausgeführt werden.
- Zweigüberdeckung: p, q, u, v müssen jeweils in beiden Zweigen durchlaufen werden. 
- Termüberdeckung: Alle möglichen Ursachen für die Verzweigungen müssen wirksam geworden sein.
- Pfadüberdeckung: Alle möglichen Pfade müssen durchlaufen worden sein (hier wegen q möglicherweise unendlich viele).

## Werkzeugunterstützung
Der Glass-Box-Test setzt – wenigstens auf der Ebene der einzelnen Anweisungen, Zweige und Bedingungen – Test-Werkzeuge voraus. Diese Werkzeuge instrumentieren die Quellprogramme (d.h. sie fügen zusätzliche Anweisungen ein), so dass während der Ausführung statistische Daten gesammelt werden. Außerdem kumulieren die Werkzeuge diese Daten, so dass eine Aussage entsteht, wie oft ein bestimmter Befehl, Zweig o.ä. insgesamt, also in allen Testläufen, durchlaufen wurde. Schließlich präsentiert das Werkzeug die Resultate in leicht lesbarer Form, z.B. durch unterschiedlich eingefärbten Quellcode, der unmittelbar die noch nicht erreichten Teile erkennen lässt. Ein solches Werkzeug ist (unvermeidlich) an eine bestimmte Programmiersprache gebunden. Allerdings werden auch Werkzeugfamilien angeboten (z.B. für C, C++ und Java).

# Empirische Evidenz
## Test-Automatisierung
### Vorteile
- verbesserte Produktqualität
- hohe Überdeckung
- verkürzte Testzeit
- Zuverlässigkeit
- erhöhtes Vertrauen
- Wiederverwendbarkeit der Tests
- Weniger menschlicher Aufwand
- Kosteneinsparung
- erhöhte Fehlerfindungsrate
### Nachteile
- Automatisierung kann manuelles Testen nicht ersetzen
- Wartung von automatisierten Testfällen
- Einführung des Prozesses braucht Zeit
- fehlende Mitarbeiter mit entsprechenden Fähigkeiten
### Effektivität, Effizienz und Fehlerentfernungskosten
![[Effektivität, Effizienz und Fehlerentfernungskosten.png|400]]
In Wagner (2006) wurden Studien zur Effektivität, Effizienz und zu den korrespondierenden Fehlerentfernungskosten gesammelt. Functional meint hier Black-Box und Structural Glass-Box.

