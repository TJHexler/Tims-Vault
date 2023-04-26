---
tags: Uni Syskon
---
# ASN.1 (Abstract Syntax Notation One)
- Notation, um abstrakte Syntax zu definieren (konzeptuelles Schema) und um Parameter von Anwenderdaten festzulegen
- ermöglicht es, Typen und Werde festzulegen ohne die Darstellung festzulegen
- zusätzlicher Standard zum Application Layer
- Codegenerator generiert Datenstrukturen für eine Programmiersprache auf Grundlage der ASN.1 Spezifizierungen
Basic Encoding Rules (BER) für ASN.1:
- bestimmte Kodierungsregeln für den Transfer durch ISO standardisiert
ASN.1 wird in SNMP (simple Network Management Protocol) verwendet
- Darstellung durch ASN.1
- Datentransfer durch UDP/IP
### abstrakte Syntax
- Menge von Typendefinitionen für Datenobjekte die im Anwendungsprotokoll verwendet werden
- stellt Datenstrukturen in einer programmiersprachenunabhängigen Sprache dar
- Teilmenge einer Schnittstellenbeschreibungssprache - Typdeklaration
### Transfer-Syntax
- konkrete Datenrepräsentation beschrieben durch abstrakte Syntax
- definiert durch eine Menge von Kodierungsregeln die abstrakte Syntax in die Transferdaten (Syntax) umsetzt
- definiert: Basic Encoding Rules (BER), andere möglich
### ASN.1 - einfache Datentypen
einfache Datentypen:
- BOOLEAN; INTEGER; ENUMERATED; REAL; OBJECT IDENTIFIER IA%STRING; CHARACTER; STRING; OCTET STRING; BIT STRING; etc.
Typdefinition:
	NameOfType ::= type
Initialisierung einer neuen Instanz:
	nameOfValue NameOfType ::= value
### ASN.1 - konstruierte Datentypen
- SEQUENZ
	- geordnete Liste eines bestimmten Datentyps mit festgelegter Länge
	- einige Datentypen können als OPTIONAL markiert werden
- SET
	- ungeordnete Liste von Datentypen
	- festgelegte Länge
	- einige Datentypen können als OPTIONAL markiert werden
- SEQUENCEOF
	- geordnete Liste von Elementen des gleichen Datentyps
	- Anzahl der Elemente kann festgelegt oder variabel sein
- SETOF
	- Menge von Elementen des gleichen Datentyps
	- Anzahl der Elemente kann festgelegt oder variabel sein
- CHOICE
	- Menge von Datentypen, von denen bestimmter Datentyp gewählt werden kann
	- festgelegte Anzahl an Elementen
Beispiel:
![[konstruierte Datentypen ASN.1 Beispiel.png]]
## Basic Encoding Rules (BER) - Tag-Länge-Wert Struktur
![[Basic Encoding Rules.png]]
##### Längenkodierung:
bekannte Länge:
- Kurzform 1 Byte (erstes Bit 0, restliche Bits kodieren Länge als Integer)
- Langform n Bytes (erstes Bit 1, restl. Bits des ersten Bytes kodieren Anzahl folgender Bytes, folgende Oktette kodieren Länge als binären Integer)
unbekannte Länge:
- erstes Bit des Längenoktetts 1, alle anderen 0
- Ende-Feld wird benutzt (2 Oktetten bestehen ausschließlich aus Nullen)
Oktett = Sequenz von 8 bits
## ASN.1 Zusammenfassung
Flexibel:
- Kodierungsregeln können frei erweitert werden
- bekannte Datentypen können dargestellt werden
- Sprachen unabhängig
ABER:
- TLV Kodierung sehr "geschwätzig"
- Typspezifizierung kann sehr aufwendig werden (explizites/implizites Tagging, Überschreibungsregeln)