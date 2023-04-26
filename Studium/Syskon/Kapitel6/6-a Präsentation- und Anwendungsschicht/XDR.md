---
tags: Uni Syskon
---
# External Data Representation (XDR)
- Endstand in Remote Procedure Call Systemen
- Client und Server "wissen, was sie tun"
- Interface Definition Language spezifiziert das Server Interface
- Clients können nur mit Servern interagieren, wenn sie deren Interface kennen
- IDL "formt" eine "Vertrag" zwischen Client und Server
- beide wissen, welche Datentypen ausgetauscht werden
- XDR benötigt keinen extra Header
	- RPC Header enthält Prozedurnamen, Client und Server kennen Parametertypen und -Reihenfolge
- alle Daten werden auf feste Übertragungssyntax abgebildet (keine Verhandlung) - XDR ist Transfersyntax
- Blockgröße 32bit (auf Wortgröße aufgefüllt)
- Integer im 4 Byte Big Endian Format dargestellt
- Gleitkommazahlen im IEEE-Format
Nachteil:
- zwei identische Maschinen, die eine andere interne Darstellung als die oben genannte verwenden müssen zwei überflüssige Umwandlungen durchführen
XDR Compiler erstellt C Datenstrukturen und program stubs für die Kodierung/Dekodierung auf Grundlage von XDR Definitionen
## XDR Datentypen
![[XDR Datentypen.png]]
weitere XDR Datentypen: Vorzeichenlose Integer, Aufzählung, Double-Gleitkommazahlen, String, Opaque Data mit fixer/variabler Länge, Array mit fixer/variable Länge, Boolean, Discriminated Union, Optionale Daten, Hyper Integer / Hyper Vorzeichenlose Integer (64 bit), Void
## Zusammenfassung
- unkomplizierte Darstellungsinteraktion (IDL wird sowieso benötigt, um stubs zu erstellen, effizientes Transferformat, sprachenunabhängig)
- Client und Server verlassen sich auf "einen Vertrag"
	- Änderung der Darstellung durch hinzufügen neuer Felder muss in IDL Definition reflektiert werden ([[ASN.1]] kann die Erweiterung ignorieren)
	- ABER: keine Typinformationen zusätzlich zu Nutzdaten nötig
- unnötige Umwandlung vom Host- ins Netzwerkformat
	- nicht unbedingt ein RPC-Problem: DCE, CORBA IIOP bieten eine Lösung