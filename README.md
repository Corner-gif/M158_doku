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


## Übung Pfade
Lokal

Folgende Verzeichnisstruktur ist vorhanden:
```
C:\Daten\Bilder
C:\Daten\CSS
C:\Daten\index.html
C:\Daten\Bilder\Blume.jpg
C:\Daten\Bilder\test.html
C:\Daten\CSS\main.css
```



1. Wie ist der absolute Pfad von der Datei "main.css"?
C:\Daten\CSS\main.css

2. Angenommen, Sie wollen in der "index.html" Datei das Bild "Blume.jpg" einfügen, wie ist der relative Pfad zum Bild?
\Bilder\Blume.jpg

3. Sie wollen von der Datei "main.css" auf das Bild "Blume.jpg" zugreifen, wie ist der absolute Pfad?
C:\Daten\Bilder\Blume.jpg

4. Sie wollen von der Datei "main.css" auf das Bild "Blume.jpg" zugreifen, wie ist der relative Pfad?
...\Bilder\Blume.jpg

5. Sie wollen von der Datei "test.html" auf das Bild "Blume.jpg" zugreifen, wie ist der relative Pfad?
Blume.jpg