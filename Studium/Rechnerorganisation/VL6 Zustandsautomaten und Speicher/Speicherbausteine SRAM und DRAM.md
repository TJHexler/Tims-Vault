---
tags: Uni RO
VL-Date: 17.05.23
---
# Radom-Access Memory vs. Serial Memory
- Speicherzellen auf die jederzeit auf beliebige Adressen zugegriffen werden kann, werden Random Access Memory genannt
- Im Gegensatz dazu ist das Serial Memory zu nennen - das beispielsweise von Festplatten benutzt wird. Hier spielt die Position aus der eine Speicherzugriff erfolgt, eine Rolle, da je nach Position des Zugriffs unterschiedliche Zugriffszeiten auftreten.
# Speicherbausteine
- bestehen aus Zellen , die die Fähigkeit besitzen binäre Informationen zu speichern. Zusätzlich besitzen diese Bausteine elektronische Schaltungen um Daten zu speichern (Schreibvorgang) und zu lesen (Lesevorgang).
- grundsätzlich werden lesbare und beschreibbare Speicher unterschieden:
	- Random-access memory (RAM) (Wahlfreier Speicherzugriff)
	- Read-only Memory (ROM) (nur lesbarer Zugriff)
- binäre Informationen werden in Gruppen von Bits bzw. Bytes gespeichert, die WORT genannt werden.

# Random-Access Memory
![[RAM.png|300]]
- Ein Wort bezeichnet eine Gruppe von Bits, die sich in und aus dem Speicher, als eine Einheit bewegt:
  eine Gruppe von 1 und 0, die eine Zahl, einen Befehl, die ein Codeinformation darstellt. 
- Die meisten Computer verwenden Wörter, die ein Vielfaches von 8 Bits (1Byte) lang sind,
- Die Kapazität einer Speichereinheit wird in der Regel als die Gesamtzahl der Bytes, die sie speichern kann angegeben.
![[RAMSpeicheradresse.png|300]]

# Kontroll-Signale und Timing Diagramme
## Random-Access Memory - Steuereingänge
- Chip Select $\rightarrow$ wird benutzt, um den Memory-Chip einzuschalten, der das gewünschte Wort enthält.
- Chip Select inactiv $\rightarrow$ Es wird keine Operation ausgeführt
- Chip Select active $\rightarrow$ der Lese/Schreibeingang definiert die ausgeführte Operation
![[Kontrolleingänge eines Speicherbausteins.png|300]]

# Random-Access Memory
- Die Operation des Speicherbausteins werden von extern von der CPU gesteuert.
- Der Speicherbaustein und die CPU werden von einer unterschiedlichen Taktgebung synchronisiert - Lese- und Schreiboperationen werden durch Werteunterschiede innerhalb der Kontrolleingaben getaktet.
- Die Zugriffszeit eines Lesezugriffs im Speicher beschreibt die maximale Zeit von der Adressierung bis zur Datenausgabe
- Der Schreibzyklus beschreibt die maximale Zeit von der Adressierung über die Komplettierung aller internen Speicheroperatioen, die für das Speichern eines Wortes notwendig sind.
- Die CPU muss die Kontrollsignale für den Speicherbausteins in einer Art bereitstellen, die die Synchronisation interner Taktoperationen mit den Lese- und Schreiboperationen gewährleistet
- Dies bedeutet, dass die Zugriffzeit und der Schreibzyklus des Speicherbausteins einer Periode, aus festen CPU Taktperioden entsprechen muss
- Schreibzyklus
  ![[RAMSchreibzyklus.png|300]]
- Lesezyklus
  ![[RAMLesezyklus.png|300]]

# statisches vs. dynamisches Random Access Memory
SRAM und DRAM sind beide flüchtige Speicher (sie verlieren gespeicherten Informationen, wenn die Stromversorgung abgeschaltet wird)
## statischer RAM (SRAM)
besteht aus internen Schaltungen mit Rückkopplung, die binäre Informationen speichern. Die gespeicherten Informationen erhalten, solange eine Stromquelle den Speicherbaustein mit Energie versorgt.
- SRAM ist einfacher zu Handhabung und hat kürzere Lese und Schreibzyklen.
$\rightarrow$ es ist kein "Refresh" erforderlich

- Die Schaltkreise bestehen aus Dekodern , die entscheiden, ob das Wort gelesen oder geschrieben werden soll , Schaltungen für den Lesevorgang, Schaltungen für den Schreibvorgang, sowie der Ausgabelogik
- Die RAM Zelle ist die elementare Binär Speicherzelle , die in einem RAM Speicherbaustein benutzt wird
- Die Speichereinheit wird durch ein SR Latch modelliert
- Die Eingänge zum Latch werden durch ein Auswahlsignal aktiviert
- Die Ausgabe des Latches wird durch die “ Auswahl Schaltung generiert , um die Zellausgaben zu erzeugen

![[RAMZelle.png|300]]

- Für das Bilden eines Bit Slice, der alle Schaltkreise enthält , die einer einzelnen Bit Position aus einer Reihe von RAM Wörtern zugeordnet sind , wird eine Verbindung von RAM Zellen mit den Schaltkreisen die für Lese und Schreibvorgänge benötigt. Grafische Darstellung einer Bit-Slice:
![[SRAMBitSlice.png|300]]

- Der Dekoder mit 𝑘 Eingängen und 2𝑘 Augängen benötigtbenötigt2𝑘 AND Gatter bei 𝑘 Eingängen pro Gatter
- Die Gesamtzahl der Dekoder Gatter , die Anzahl der Eingänge pro Gatter sowie die Anzahl der RAM Zellen pro Bit Slice, können alle durch die Verwendung zweier Dekoder mit einem gleichen Auswahlschema , verringert werden.
![[SRAM.png|400]]
![[SRAM2.png|400]]


## dynamischer RAM (DRAM)
binäre Informationen werden in Form von elektrischen Ladungen in den Kondensatoren gespeichert. Auf diese Kondensatoren die sich innerhalb des Chips befinden, kann durch n Kanal MOS Transistoren zugegriffen werden.
- bietet reduzierten Energieverbrauch und eine größere Speicherkapazität in einem einzigen Speicherchip.

- hohe Kapazitäten bei geringen Kosten
- DRAM-Speicher dominieren bei Anwendungen, die hohe Kapazitäten benötigen (z.B. RAM in einem Computer)
- dynamisch impliziert, dass Informationen nicht inheränt sondern lediglich kurzfristig gespeichert werden
- Die Informationen müssen in periodischen Zyklen erneuert werden
- modifizierte Prozesstechnologie für die Herstellung von DRAMs gegenüber SRAM

## Zeilen- und Spaltendecoder
RAM Größe: $32K \times 8 \rightarrow$ Gesamt: $256K$ Bits
- Die ersten 9 Bits werden für den Zeilendekoder verwendet. Die verbleibenden 6 Bits werden für den Spaltendekoder verwendet. Beachten Sie es gilt: 29+6= 32K
- Die Nutzung eines einzelnen Dekoders ermöglicht 15 Eingaben und 32768 Ausgaben
- Mittels simultaner/gleichzeitiger Auswahl:
	- ein 9-Bit Zeilendekoder
	- ein 6-Bit Zeilendekoder
- Die Anzahl der Gatter, die durch die Anwendung eines Spalten- und Zeilendekoders benötigt wird gegenüber einer einzigen Adressierungseinheit ist deutlich geringer

## Verbund von SRAM ICs
- Ist die Speichereinheit , die für eine Anwendung erforderlich ist, größer ist als die Kapazität eines Chips, so besteht die Notwendigkei , eine Anzahl von Chips in einem Verbund von Speicherzellen zu kombinieren, um die erforderliche Größe des Speichers implementieren zu können.
![[SRAMICs.png|300]]
- Ein $256K \times 8$ RAM mit vier $64K \times 8$ RAM chips
	- Zwei zusätzliche Adressbits werden hinzugefügt , um den CS eines jeden Chips zu kontrollieren
![[Verbund von SRAM ICs.png|300]]

## Array of SRAM ICs
- Realisierung eines $64K \times 16$ RAM mit zwei $64K \times 8$ RAM chips
![[Array SRAM ICs.png|300]]

## DRAM-Zelle
- Der Kondensator wird benutzt um Ladungen zu speichern. Ausreichendes Ladungspotential $\rightarrow 1$. Für alle sonsitigen Fälle $\rightarrow 0$
![[DRAM Zelle.png|300]]

## DRAM Bit-Slice Modell
- entspricht logisch dem SRAM Bit-Slice Model
- Kosten pro Bit:
  DRAM-Zelle $\rightarrow1$ Kondensator + 1 Transistor
  SRAM-Zelle $\rightarrow$ sechs Transistoren
- SRAM Komplexität $\approx$ DRAM Komplexität
- DRAMs benötigen "Refreshing"
![[DRAMBitSliceModell.png|300]]

## DRAM mit Refresh Logikeinheit
![[DRAM mit refresh Logikeinheit.png|300]]

## DRAM Schreibzyklus
![[DRAM Schreibzyklus.png|300]]

## DRAM Lesezyklus
![[DRAM Lesezyklus.png|300]]

