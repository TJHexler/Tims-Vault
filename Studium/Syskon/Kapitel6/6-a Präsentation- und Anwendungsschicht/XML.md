---
tags: Uni Syskon
---
# Extensible Markup Language (XML)
- Tag-basiert und man kann eigene Tags erstellen (XML Schema/DTD)
- Basis für mehrere, aktuelle Webtechnologien (AJAX, RSS(Feeds), XHTML, Web-services)
- wird verwendet, um Informationen zu strukturieren und zu beschreiben
- Datentype, Nachrichtenformate, Registrierungsinformationen können modelliert werden --> Web-Services
	- SOAP modelliert Interaktion zwischen Komponenten, nur Interoperabilitätsprotokoll, kein Application Interface
	- WSDL (web service description Language) spezifiziert service Interface und verknüpft zu Grunde liegende Protokolle (Transport)
Bsp.: Studierendenausweis
![[XML Beispiel Studierendenausweis.png]]
## Vorteile von XML
- Inhalt und Darstellung sind getrennt
- lesbar für Menschen (naja)
- es können eigene Tags erstellt werden 
- offenes Format 
- Werkzeug-Unterstützung
- jede SML verarbeitende Anwendung kann die Daten potenziell verarbeiten --> ermöglicht Austausch von Daten zwischen Systemen, die dafür nicht entworfen wurden
## Nachteile von XML
- nicht sehr effizient bei Verarbeitung großer Datenmengen
- eben nicht gut lesbar für Menschen
- nicht für Darstellung binärer Daten geeignet (Bilder, Audio, etc.)
- oft "aufgeblasen"
- langsam