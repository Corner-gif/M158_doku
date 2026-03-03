# M158_doku
Dokumentation M158
# Factsheet – Software-Migration zwischen Linux und Windows (Kurzfassung)

## Plattformübergreifende Anwendungen
Folgende Anwendungen können grundsätzlich auf Linux und Windows laufen:

- Webapplikationen  
- Java  
- Python  
- JavaScript / Node.js  
- C/C++  
- Mono / .NET Core  
- Containerisierte Anwendungen  
- Plattformübergreifende GUI-Frameworks  

**Wichtig:** Trotz plattformunabhängiger Sprachen sind **unterschiedliche Installationspakete** pro Betriebssystem notwendig.

---

## Dateirechte

**Linux:**  
- POSIX-Rechtesystem (User, Group, Others)  
- Rechte: Lesen (r), Schreiben (w), Ausführen (x)

**Windows:**  
- ACLs (Access Control Lists)  
- Detailliertes, nicht direkt kompatibles Berechtigungssystem

---

## Pfad- und Dateisystem-Unterschiede

- Linux: `/` | Windows: `\`  
- Linux: Ein Root `/` | Windows: Laufwerke (C:\, D:\)  
- Linux: case sensitive | Windows: nicht case sensitive  
- Linux: versteckt mit `.` | Windows: Dateiattribut  
- Pfadlänge: Linux ~4096 Zeichen | Windows traditionell 260 Zeichen  
- Unterschiedliche Datei- und Ordnerattribute

---

## System- und Konfiguration

**Linux:**  
- Textbasierte Konfigurationsdateien (z.B. `/etc/passwd`)

**Windows:**  
- Registry + INI / proprietäre Formate  

---
