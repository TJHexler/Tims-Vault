---
tags: Uni EST
VL-Date: 09.05.23
---
# simuliertes Three Amigos Meeting
Aufgabe: Tun Sie sich mit zwei Kolleginnen oder Kollegen, die neben Ihnen sitzen zusammen. Teilen Sie die Rollen Domänenexperte, Entwickler, Tester untereinander auf und erarbeiten Sie ein Szenario im Gherkin-Stil für die folgende User Story:
As a registered student,
I want to register to take an exam in the current semester,
so that I can sit the exam and get a grade for it.

# Unit-Test-Muster
Wir verwenden hier Unit-Test und Modul-Test austauschbar. Die Idee ist immer der Test der kleinsten eigenständigen Einheiten. Die folgenden Muster stammen aus dem Buch „xUnit Test Patterns. Refactoring Test Code“ von Gerard Meszaros. Das Buch enthält noch deutlich mehr. Wir behandeln nur eine Auswahl. Wir werden noch öfter auf das Konzept „Muster“ treffen. Im Software Engineering meint man damit meist eine bewährte Lösung bzw. Lösungsstruktur für ein wiederkehrendes Problem. Im folgenden sehen wir also bewährte Möglichkeiten, Unit-Tests zu strukturieren und zu implementieren.

## Unit Test
1. Testing of individual routines and modules by the developers or an independent tester.
Es werden also kleinere Einheiten individuell getestet. Dieser Test findet isoliert von anderen Units statt. Wechselwirkungen mit anderen Units sind nicht von Interesse. Unit Tests werden oft von den Entwickler*innen* direkt geschrieben, oft direkt im Zusammenhang mit der Entwicklung des Produktionscodes. Im ISTQB-Standard wird der Begriff „Komponententest“ als allgemeine Form verwendet und „Unit-Test“ als Spezialform neben „Klassen-Test“. Ich halte mich hier aber an die international und in der ISO/IEC/IEEE-Norm gebräuchlichere Variante „Unit-Test“. Mir ist auch nicht klar, warum „Unit“ spezieller wäre als „Komponente“.

### Wiederholung jUnit Test für fibonacci(n)
![[jUnitTest fibonacci.png|200]]
- Testklasse FibonacciTest (verwendet jUnit-Framework)
- Testfall in Testmethode correctResult() testet ob fibonacci(3) == 2
- Überprüfung durch Aufruf von assertEquals(expected, result)
Details zu JUnit wurden bereits in der PSE behandelt.

## Testcase Class per Class
Wie verteilen wir unsere Testmethoden über Testfall-Klassen?
Die einfachste Art Testmethoden zu Testfallklassen zuzuordnen ist, für jede Klasse, die wir testen jeweils die zugehörigen Testmethoden in eine Testfall-Klasse zu stecken. Das ist zumindest zu Beginn ein gutes Vorgehen.

Falls die Zahl der Methoden in der Testfall-Klasse zu stark ansteigt, hat es sich bewährt, separate TestfallKlassen pro Feature anzulegen. Die Schwierigkeit dabei ist es, sinnvolle Features zu identifizieren. Wenn dies gelingt, hat man durch diese Aufteilungen einen guten Überblick über die Testfälle. Eine weitere Alternative wäre Testcase Class per Fixture, weil dies Code-Duplikate vermeidet.

## Four-Phase Test
Wie strukturieren wir unsere Testlogik, sodass offensichtlich wird, was wir testen?

Wir haben bereits kennengelernt, dass ein Testfall immer eine Eingabe und eine erwartete Ausgabe enthalten muss. Bei einem automatisierten Test kann man darüberhinaus vier Teile unterscheiden: Der Vorbereitungsteil (engl. Setup) baut die Umgebung und die Daten für einen Testfall (evtl. auch für mehrere Testfälle) auf. Dazu gehört auch die Fixture, die das SUT (System Under Test) mit anderen abhängigen Klassen verbindet und diese evtl. durch Dummys ersetzt. Der Ausführungsteil (engl. Exercise) ruft dann die zu testenden Funktionen im SUT auf. Der Verifikationsteil (engl. Verify) führt den Vergleich zwischen Resultat und erwartetem Resultat durch. Der Abschlussteil (engl. Teardown) schließlich räumt die aufgebauten Ressourcen (z.B. im Fixture) wieder auf.

## Assertion Message
Wie strukturieren wir unsere Testlogik, sodass wir wissen, welche Zusicherung fehlgeschlagen ist?

Es gibt einige Richtlinien und Bücher, die empfehlen nur eine Zusicherung pro Testfall zu benutzen. Dies hat sicherlich Vorteile, da immer klar ist, welche Zusicherung fehlgeschlagen ist. Es hat aber den Nachteil, dass ich zwei Testfälle implementieren muss, wenn ich zwei Aspekte prüfen will, wie z.B. die Länge eines Felds und dann den Inhalt. Deshalb empfiehlt dieses Muster jeder Zusicherung eine Nachricht mitzugeben, die diese beschreibt. Dabei sollte man auf drei Aspekte achten, die die Nachricht idealerweise enthält:
- Die Variable, die geprüft wird
- das erwartete Verhalten
- Argumente, die vergeben wurden

## Sate Verification
Wie machen wir den Test selbstprüfend, wenn der Zustand verifiziert werden muss?

![[state verification code example.png|300]]

Es ist nicht immer klar, was das erwartete Resultat eigentlich ist. Wenn das SUT keinen Wert zurück liefert, sondern „nur“ seinen Zustand ändert, dann müssen wir diese Zustandsänderung abprüfen. Diese könnte man durch das Abbprüfen der einzelnen Attribute tun. Hier im Beispiel verwenden wir stattdessen einen Vergleich mit dem erwarteten Objekt.

## Behaviour Verification
Wie machen wir den Test selbstprüfend, wenn es keinen Zustand gibt?
![[behaviour verification code example.png|300]]

Die normale Alternative zu State Verification ist, dass das SUT ein sichtbares Verhalten zeigt, dass wir mit dem erwarteten Verhalten vergleichen können. Dies ist der Standardfall im Unit-Test. Im gezeigten Beispiel ist es aber wiederum gar nicht so einfach, weil das Verhalten nicht direkt beim Testfall sichtbar wird. Stattdessen muss es über einen Umweg geholt werden. Hierzu verwenden wir einen Test Spy, eine Art des Test Doubles, die wir im folgenden noch genauer anschauen. Das Code-Beispiel ist aus Meszaros (2007).

## Test Double
Wie können wir Logik unabhängig verifizieren, wenn abhängiger Code nicht verwendbar ist?

Eine typische Schwierigkeit beim Unit-Test ist es, dass das SUT von anderen Klassen oder Komponenten abhängt. Damit ist der Test nicht mehr unabhängig und damit schwieriger zu testen. Evtl. kommen dadurch sogar ständig andere Ergebnisse. Deshalb verwenden wir stattdessen ein Test Double. Dies ersetzt die abhängigen Klassen insoweit, dass die Testfälle auf dem SUT durchgeführt werden können. Es muss nicht alle Funktionalität der abhängigen Klassen replizieren. Die API muss aber übereinstimmen. Wann und wie dies konkret umzusetzen ist, beschreiben die fünf weiteren Muster unten genauer.

### Test Stub
Wie können wir die Logik unabhängig prüfen, wenn sie von indirekten Eingaben anderer Komponenten abhängt?

![[TestStubCodeExample.png|300]]
Ein Test Stub liefert bestimmte Werte an das SUT. Dies kann immer der gleiche Wert (Hard-Coded Test Stub) oder ein konfigurierbarer Wert sein. Wichtig ist, wie bei jedem Test Double, dass der Test Stub installierbar ist. Er muss dem SUT also irgendwie untergeschoben werden können. Im Beispiel kann man im TimeDisplay einen TimeProvider entsprechend setzen. Das Code-Beispiel ist aus Meszaros (2007).

### Test Spy
Wie können wir die Logik unabhängig prüfen, wenn sie indirekten Ausgaben an andere Komponenten macht?

![[TestSpyCodeExample.png|300]]

Wir haben einen Testspion bereits im Einsatz gesehen, als wir die Behaviour Verification diskutiert haben. Er ist das Gegenstück zum Test Stub, indem er die Ausgaben des SUT an andere Komponenten abfängt und dem Testfall zur Verifikation übergibt. Das Code-Beispiel ist aus Meszaros (2007).

### Mock Object
Wie können wir die Logik unabhängig prüfen, wenn sie von indirekten Eingaben und Ausgaben abhängt?

![[MockObjectCodeExample.png|300]]

Bei der Verwendung eines Mock-Objekts ersetzen wir ein Objekt, auf das sich das SUT verlässt mit einem testspezifischen Objekt, das verifiziert, dass es vom SUT korrekt verwendet wird. Der Testfall setzt das MockObjekt mit der richtigen API und entsprechenden Erwartungen auf. Im Mock-Objekt prüfen wir dann die Zusicherungen ab. Ein Mock-Objekt ist insbesondere bei State Verification notwendig. Bei Behaviour Verification ist es üblicherweise nicht notwendig. Da reicht ein Test Stub oder ein Fake Object. Wir können für das Beispiel des Flugs statt einem Test Spy auch ein Mock Object verwenden. Im Beispiel sehen wird, dass sowohl mit einem assertFalse geprüft wird, ob der Flug noch im SUT existiert, als auch eine Abfrage am MockObjekt durchgeführt wird, ob alles richtig abgelaufen ist. Das Code-Beispiel ist aus Meszaros (2007).

### Fake Object
Wie können wir die Logik unabhängig prüfen, wenn Objekte , die sie benötigt, nicht verwendet werden können?

![[FakeObjectCodeExample.png|300]]

Ein Fake Object ist eng mit den vorherigen verwandt. Der Fokus liegt hier auf einer sehr leichtgewichtigen Implementierung. Das Fake Object ersetzt den Zugriff auf ein anderes Objekt oder eine andere Komponente, auf die nicht zugegriffen werden sollte, nicht zugegriffen werden kann oder bei der ein Zugriff sehr lange dauern würde. Insbesondere versucht man damit unerwünscht Seiteneffekte zu vermeiden. Beispielsweise ist eine Fake Database beliebt, die vermeidet, auf die richtige Datenbank zugreifen zu müssen. Dies kann enorme Geschwindigkeitsgewinne bringen. Das Code-Beispiel ist aus Meszaros (2007).

### Dummy Object
Wie spezifizieren wir Werte in Tests, die nur für irrelevante Aufrufe benötigt werden?

![[DummyObjectCodeExample.png|300]]

Teilweise werden Werte in einem Test benötigt, damit das SUT etwas aufrufen kann. Es ist für den Test aber u.U. unwichtig, welche Werte dies genau sind, da dieser Aspekt nicht hier geprüft wird. Dann verwenden wir ein Dummy-Objekt. Dies kann den Test deutlich kompakter machen anstatt jedes einzelne Attribute separat innerhalb des Testfalls zu setzen. Das Code-Beispiel ist aus Meszaros (2007).