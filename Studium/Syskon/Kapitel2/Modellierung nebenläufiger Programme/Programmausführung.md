---
tags: Uni Syskon
---
# Programmausführung in einer Rechnerarchitektur

## Registermaschine
- modelliert bestimmte Rechnerarchitektur
- Prozessor (CPU) stellt Register bereit
- Prozessorbefehle zum Lesen/Schreiben
- Prozessorbefehle für Berechnungen auf Registerinhalte: addieren, multiplizieren

reale Bsp.: Android Dalvik VM, x86 Prozessorarchitekturen
### registerbasierte Ausführung
![[register Ausführung.png]]

## Stapelmaschinen (Stack)
- systemunabhängige Ausführung von Berechnungsschritten
- portabel über mehrere Rechnerarchitekturen hinweg

reales Bsp.: Java VM
### Stapelausführung
![[Stapelausführung.png]]

## CPU-Zyklus
- besteht aus **Ladephase** und **Ausführungsphase**
- Unterbrechung des Programms nur am Ende der Ausführungsphase
	--> dazu spezielle Hardware und [[Unterbrechungsbehandlung]](UBR) nötig

![[CPU-Zyklus.png]]