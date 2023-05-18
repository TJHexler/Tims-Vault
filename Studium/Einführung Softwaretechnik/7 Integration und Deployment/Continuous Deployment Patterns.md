---
tags: Uni EST
VL-Date: 15.05.23
---
# Continuous Deployment Patterns
## Blue-Green Deployments
__Problem__: Beim Deployment sollte der Cut-Over, also das Umschalten, sehr schnell gehen, damit die Software schnell wieder verfügbar ist. Auch in die andere Richtung, also das Zurückrollen (Rollback) muss schnell gehen, falls das neue Release fehlerhaft ist.

__Lösung__: halte immer zwei lauffähige Systeme vor, zwischen denen schnell, z.B. direkt am Router über das Netzwerk umgeschaltet werden kann. Ein System hat die bisherige, bewährte Version, das andere System eine neu deployte Version.

In diesem Beispielsystem haben wir Komponenten auf drei Servern laufen. Sie interagieren, um eine Webapplikation für unsere Nutzerinnen und Nutzer zur Verfügung zu stellen. Die aktuell verwendete Version ist der Release v1.1. Nun deployen wir parallel dazu die neue Version v1.2.
![[BlueGreenDeployment1.png|300]]
![[BlueGreenDeployment2.png|300]]
Nach erfolgreichem Deployment von v1.2 können wir direkt im Router die Route umstellen und nun die neue Version aufrufen.

## Canary Releasing
__Problem__: : Beim Deployment einer neuen, fehlerhaften Version mit Features, die Nutzer*innen* auswählen, sind die Auswirkungen sehr groß, da schnell alle Nutzer*innen betroffen sind.

__Lösung__: Um das Risiko zu senken, werden nicht sofort alle Nutzer*innen* auf die neue Version umgestellt, sondern nur ein kleiner Anteil. Dieser Anteil wird beobachtet, und sobald wir sicher genug sind, dass keine Probleme auftreten, wird die neue Version auf alle Nutzer*innen* ausgerollt.

Wir stellen hier erstmal nur 5% der Nutzer*innen* auf die neue Version um. Die Auswahl dieser Nutzer*innen* kann rein zufällig gemacht werden. Es kann aber auch sinnvoll sein bestimmte Nutzer*innen*-Klassen oder geographische Regionen auszuwählen. Diese sind unsere Kanarienvögel. Wenn hier Probleme auftreten, schieben wir sie einfach wieder zurück auf die alte Version. Wir haben aber in jedem Fall bei maximal 5% der Nutzerschaft Probleme verursacht.
![[CanaryRelease1.png|300]]
![[CanaryRelease2.png|300]]Nach einer gewissen Zeit und wenn keine Probleme aufgetreten sind, stellen wir auf v1.2 um. Die alte Version kann gelöscht oder für ein Blue-Green Deployment noch vorgehalten werden.

## Dark Launching
__Problem__: Beim Deployment einer neuen, fehlerhaften Version mit Features, die die Nutzung ergänzen, sind die Auswirkungen sehr groß, da schnell alle Nutzer*innen* betroffen sind.
__Lösung__: Um das Risiko zu senken, werden die neuen Features für die Nutzer*innen* unsichtbar deployt. Echte Nutzer*innen*-Interaktionen werden zusätzlich zur alten Version auch an das Feature im Backend weitergegeben und das Verhalten analysiert. Erst wenn das neue Feature sich auch mit den echten Interaktionen verhält wie erwartet, schalten wir auf das neue Feature um.

Beispielsweise hier beschrieben: https://martinfowler.com/bliki/DarkLaunching.html

![[DarkLaunching.png|300]]

In einem normalen Release einer neuen Backend-Komponente schaltet man von der Client-Software zur neuen Backend-Komponente, die dann Ergebnisse zurückliefert. Falls zu diesem Zeitpunkt Performanzprobleme bei der neuen Komponente auftreten, werden die Nutzer*innen* direkt betroffen sein. Eine Möglichkeit, das Backend unter Stress zu versetzen, ohne die Nutzer*innen* unbedingt etwas davon mitbekommen zu lassen ist das Muster Dark Launching. Die Idee ist, einen Zwischenschritt einzuführen: Die neue Backend-Komponente wird deployed und der Client startet eine „Silent Query“ (eine stille Anfrage) zur neuen Komponente, ohne den Wert zu verwenden. Parallel wird der Wert für den Client durch die alte Backend-Komponente berechnet. Damit kann man dann Probleme in der neuen Komponente erkennen bevor irgendwelche Nutzer*innen* betroffen sind.

## A/B Testing
__Problem__: Ich habe mehrere Möglichkeiten der Umsetzung eines Features oder der Benutzeroberfläche, aber ich habe keine gute Basis mich für eine Variante zu entscheiden.

__Lösung__: Ähnlich dem Canary Release testen wir die Varianten gegeneinander. Ein Teil der Nutzer*innen* wird zu Variante A geleitet, ein anderer Teil zu Variante B. Wir vergleichen dann anhand passender Messungen, welche Variante besser ist.

![[ABTesting.png|300]]

Ein inzwischen übliches Vorgehen ist dies bei Webseiten und Design-Varianten. Sehr bekannt ist das Beispiel, in dem Google eine ganze Reihe unterschiedlicher Blautöne für die Links in den Suchergebnissen getestet hat, um herauszufinden, worauf Nutzer*innen* am wahrscheinlichsten klicken.

## Feature Toggles
__Problem__: : Beim kontinuierlichen Deployment wird die Mainline bis hin zur Produktion automatisch veröffentlicht. Wenn wir in der Entwicklung aber auf der Mainline arbeiten sind dort wahrscheinlich unfertige Features, die noch nicht benutzt werden können.

__Lösung__: Wir bauen in unser System die Möglichkeit einzelne Features ein und auszuschalten. Damit können unfertige Features im Deployment deaktiviert werden.

__Alternative Namen__: Feature Flags, Feature Bits, Feature Flippers

#### Beispiel
![[Feature Toggels Beispiel.png|300]]