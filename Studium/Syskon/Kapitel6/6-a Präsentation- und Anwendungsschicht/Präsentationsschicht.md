---
tags: Uni Syskon
---
# Präsentationsschicht
#### Motivation
sicherstellen, dass Daten gleich Interpretiert werden (bei Empfänger und Sender)
Eine Verbindung ist noch keine Kommunikation (Semantik der Daten kann verloren gehen)
#### Probleme
- wie können strukturierte Daten in Bytestreams und zurück konvertiert werden?
- Layout: Little- vs. Big-Endian
- Darstellung: Einer-, Zweierkomplement, Gleitkommazahlen
- Ausrichtung: Byte, Word, Long Word Grenzen
- Auffüllen: Umgang mit Lücken in strukturierten Daten
## Marshalling: Typsysteme für das Netzwerk
unterschiedliche Informationen werden für Kodierung verwendet
einfache Datentypen:
- Integer (Länge, Kodierung(z.B. Zweierkomplement), Reihenfolge, Ausrichtung)
- reale Zahlen (Länge der Mantisse & des Exponenten, Bases des Exponenten, Kodierung, Reihenfolge, Ausrichtung)
- Zeichen (Kodierung (ASCII, Unicode, EBCDIC...))
- Boolean (Kodierung für TRUE und FALSE)
zusammengesetzte Datentypen:
- Record (Reihenfolge, Ausrichtung)
- Array (Reihenfolge, Ausrichtung)
## Modelle zur Datenrepräsentation
Ziel: strukturierte Daten (Anwendung) ins Netzwerkformat und zurück übertragen, möglicherweise über heterogene Host-Systeme
![[Modelle zur Datenrepräsentation.png]]
Modelle: __einfacher Ansatz, [[ASN.1]], [[XDR]]__
## Darstellung von Daten: Bytereihenfolgeprobleme lösen
##### einfacher Ansatz:
Client:
```java
mydata = htonl(815);
send(clientSocketID, &mydata, sizeof(long), 0);
```
Server:
```java
long theirdata;
msgLen = recv{clientSocketID, &theirdata, sizeof(long), 0};
theirdata = ntohl(theirdata);
printf("Received message: %d\n", theirdata);
```
##### Basis
Host-zu-Netzwerk Umwandlung von Integers
- andere Ansätze basieren auf __Oktets__ (8 bit Wert ohne Konvertierung)
- löst lediglich Problem der Reihenfolge, nicht die strukturierter Datentypen (Darstellung/Auffüllen)
## strukturierte Daten: mögliche Lösungen
beide Kommunikationspartner kennen ausgetauschte Datentypen und ihre Darstellung 
- Datentypen werden in Definitionssprache, z.B. IDL in Remote Procedure Call Systemen (RPC) festgelegt
- keine zusätzlichen Datentypinformationen muss übertragen werden
- XDL, CORBA IDL
Kommunikationspartner erhalten/hängen Datentypeninformationen an ausgetauschte Daten an
- Datentypen sind selbsterklärend
- zusätzlicher Overhead für Datentypspezifikationen
- Bsp.: [[ASN.1]], CORBA Dynamic Any, [[XML]] basierte Formate
# Presentation Layer Zusammenfassung
- Umwandlung von Daten zwischen verschiedenen Host ist unabdingbar
- strukturierte Daten sind schwer zu bearbeiten
- Typensysteme und Kodierungsregeln für Austausch notwendig, ähnlich wie Programmiersprachen
- unterschiedliche Austauschformate sind möglich:
	- explizite Typenbeschreibung ([[ASN.1]] TLV, [[XML]])
	- implizite Typenbeschreibung ([[XDR]] ausgetauschte Datentypen sind Client und Server bekannt)
- Performance (Bandbreite, DE-/Kodierung)hängt von Darstellung der Daten ab (Web services, etc.)