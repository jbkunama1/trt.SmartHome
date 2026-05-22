# Projekt: Arduino SmartHome – Unterrichtssequenz (ca. 10 Doppelstunden)

## 1. Rahmeninformationen

- Fach: Technik (Wahlpflichtfach)
- Schulart: Realschule / Gemeinschaftsschule Sek I, Baden-Württemberg
- Klassenstufe: 8–10
- Umfang: ca. 10 Doppelstunden (10 × 90 Minuten) – modular kürzbar
- Thema: Smart-Home-Modellhaus mit Arduino – vom EVA-Prinzip zum funktionsfähigen Modell
- Bezug Bildungsplan 2016:
  - Kompetenzbereich 3.2.2 „Systeme und Prozesse“
  - Inhaltsbezogene Kompetenzen 12–18 (Mikrocontroller, Sensorik/Aktorik, Schaltpläne, Programmierung, Steuer-/Regelvorgänge)
  - Prozessbezogene Kompetenzen: Erkenntnisgewinnung, Kommunikation, Bewertung, Herstellung und Nutzung
- Leitperspektiven: Bildung für nachhaltige Entwicklung (BNE), Medienbildung (MB), Berufliche Orientierung (BO)

## 2. Projektidee in Kürze

Die Lernenden entwickeln in Gruppen ein Smart-Home-Modellhaus (DIN-A3-Grundfläche) mit Arduino-Mikrocontroller.  
Es werden drei Bereiche eng verzahnt:

1. **Mechanik**: Grundplatte, 3D-gedrucktes Haus, Halterungen
2. **Elektronik**: Sensorik (DHT, HC-SR04, Water-Sensor), Aktorik (LED-Ampel, Buzzer, Display)
3. **Programmierung**: Arduino-Sketch mit nicht-blockierender Logik (millis), Zustandsautomaten für Einparkhilfe, Klimamessung, Wasseralarm und Alarmfunktion.

## 3. Übersicht Sequenz (10 Doppelstunden)

| DS | Titel / Schwerpunkt                    | Inhalte (Kurzfassung)                                           | Kompetenzen (Auszug)      |
|----|----------------------------------------|------------------------------------------------------------------|---------------------------|
| 1  | Einführung & EVA-Prinzip              | Smart-Home-Beispiele, EVA, Modellhaus-Demo, Sicherheitsregeln   | 3.2.2, 12, 13, Erkenntnis |
| 2  | Arduino-Basics & LED-Übung            | Aufbau Arduino, IDE, LED-Blinkprog., erste Sensor-Vorschau      | 12, 14, 15                |
| 3  | Sensorik: DHT, HC-SR04, Water-Sensor  | Sensoren einzeln anschließen und messen, Werte interpretieren   | 13, 16, Erkenntnis        |
| 4  | Aktorik: LEDs, Buzzer, Display        | LED-Ampel, Buzzer, LCD/OLED ansteuern, einfache Statusanzeigen  | 14, 15, 16                |
| 5  | Mechanik: Grundplatte                 | Fertigung DIN-A3-Grundplatte, Layout für Haus und Einbauten     | 18, Herstellung           |
| 6  | 3D-Druck & Gehäuse                    | STL-Auswahl, Slicing, Druckplanung, Einbaupositionen planen     | 18, MB                    |
| 7  | Elektronikmontage I                   | Verkabelung nach Schaltplan, Teiltests der Komponenten          | 16, 18, Erkenntnis        |
| 8  | Elektronikmontage II                  | Fehlersuche, Kabelmanagement, vollständige Funktionsprüfung     | 16, 18, Bewertung         |
| 9  | Programmierung Gesamtsystem           | Zusammenführen der Module, millis-Logik, Tests & Optimierung    | 15, 17, 18                |
| 10 | Test, Präsentation & Reflexion        | Abschlusstest, Kurzpräsentationen, Selbst- und Projektreflexion | Bewertung, BO, BNE        |

> Hinweise:  
> - Mechanik/3D-Druck kann bei Bedarf teilweise vorproduziert werden (Hausteile) und im Unterricht stärker auf Elektronik/Programmierung fokussiert werden.  
> - Die Sequenz ist so angelegt, dass du einzelne Bausteine (z. B. nur Sensorik/Aktorik) auch isoliert einsetzen kannst.

---

## 4. Detailplanung der Doppelstunden

### Doppelstunde 1 – Einführung & EVA-Prinzip

**Ziele**

- SuS verstehen Smart-Home als technisches System mit Sensoren, Verarbeitung und Aktoren.
- Sie kennen zentrale Sicherheitsregeln (Holzbearbeitung, Elektronik, 3D-Druck).

**Inhalte / Ablauf (Kurz)**

1. Einstieg: Smart-Home-Beispiele der SuS, Sammlung an der Tafel.  
2. Input: EVA-Prinzip mit Infografik, Vorstellung des Modellhauses als Gesamtsystem.  
3. Kurz-Demo: Einparkhilfe, Klimamessung, Wasseralarm.  
4. Sicherheitsregeln für Werkstatt und Elektronik (RiSU-konform).  

**Produkt**: Mindmap „Mein SmartHome – Eingabe / Verarbeitung / Ausgabe“.

---

### Doppelstunde 2 – Arduino-Basics & LED-Übung

**Ziele**

- SuS kennen Aufbau und Grundfunktionen des Arduino UNO.
- Sie können ein einfaches LED-Programm (Blinken) erstellen, übertragen und anpassen.

**Inhalte / Ablauf (Kurz)**

1. Arduino als „Gehirn“: Pinübersicht, Stromversorgung, Schutzkleinspannung.  
2. Arduino IDE: Board/Port einstellen, Beispielsketch „Blink“ laden.  
3. Übung: eigene Blinkfrequenz, Blinken von zwei LEDs (Wechselblinker).  
4. Sicherung: EVA-Prinzip am LED-Beispiel (Taster optional).

**Differenzierung**

- Basis: Arbeiten mit stark kommentiertem Beispielsketch.  
- Plus: Stärkere SuS erstellen Funktionen für „Blinkmuster X/Y“ und rufen diese aus `loop()` auf.

---

### Doppelstunde 3 – Sensorik: DHT, HC-SR04, Water-Sensor

**Ziele**

- SuS schließen DHT, HC-SR04 und Water-Sensor korrekt an.
- Sie lesen Messwerte aus, interpretieren diese und benennen typische Fehlerquellen.

**Inhalte / Ablauf (Kurz)**

1. Kurzinput: Datenblätter und Pinbelegung (Infoblätter/Infografik).  
2. Stationenarbeit:
   - Station A: DHT – Temperatur/Luftfeuchte im Seriellen Monitor.  
   - Station B: HC-SR04 – Distanz in cm, einfache Grenzen (nah/fern).  
   - Station C: Water-Sensor – analoger Wert, Schwellwert testen (trocken/nass).  
3. Ergebnissicherung im Plenum (Was funktioniert, was war schwierig?).

**Hinweis**: Die Pinbelegung orientiert sich an der finalen MP1-Version (DHT an D2, HC-SR04 an D8/D9, Water-Sensor an A0).

---

### Doppelstunde 4 – Aktorik: LEDs, Buzzer, Display

**Ziele**

- SuS steuern LED-Ampel, Buzzer und Display an.
- Sie gestalten einfache Statusmeldungen / Warnhinweise.

**Inhalte / Ablauf (Kurz)**

1. Wiederholung: digitale Ausgänge, Vorwiderstand bei LEDs.  
2. Übung 1: Ampel-Logik mit drei LEDs (Rot/Gelb/Grün).  
3. Übung 2: Buzzer als Warnsignal (kurze Beeper-Sequenz).  
4. Übung 3: LCD/OLED – erste Textausgabe („SmartHome aktiv“, Temperatur).  
5. Sicherung: Diskussion, welches Feedback im realen Smart-Home sinnvoll ist (visuell/akustisch).

**Differenzierung**

- Basis: Vorgefertigte Code-Bausteine je Aktor.  
- Plus: SuS gestalten eigene Meldungstexte (z. B. für verschiedene Alarmzustände).

---

### Doppelstunde 5 – Mechanik: Grundplatte

**Ziele**

- SuS fertigen eine DIN-A3-Grundplatte fachgerecht.
- Sie planen das Layout (Position von Haus, Einfahrt, Sensoren, Elektronik).

**Inhalte / Ablauf (Kurz)**

1. Planungsphase: Skizze der Grundplatte mit Positionen (Haus, Einfahrt, Ampel, Sensoren, Elektronikbereich).  
2. Werkstattarbeit: Anreissen, Sägen, Schleifen, optional Lackieren.  
3. Markieren der späteren Bohr-/Befestigungspunkte.  

**Sicherheit**

- Schutzbrille, Fixierung des Werkstücks, Einweisung an Stichsäge / Dekupiersäge.

---

### Doppelstunde 6 – 3D-Druck & Gehäuse

**Ziele**

- SuS verstehen den Ablauf von CAD → STL → Slicing → 3D-Druck.
- Sie wählen geeignete 3D-Teile (Haus, Halterungen) aus und planen Druckjobs.

**Inhalte / Ablauf (Kurz)**

1. Kurzer Input: FDM-Verfahren, PLA, Layerhöhe, Infill.  
2. Demo: Slicing eines Gehäuseteils (z. B. Haus-Korpus oder Sensorhalterung).  
3. Gruppen planen, welche Teile sie benötigen (Haus, Halter, Ampelgehäuse, Kabelkanäle).  
4. Druckjobs einteilen (läuft teils außerhalb der Unterrichtszeit).

**Hinweis**: Je nach Infrastruktur können zentrale Teile von der Lehrkraft vorbereitet werden, während SuS sich stärker auf Elektronik und Programmierung konzentrieren.

---

### Doppelstunde 7 – Elektronikmontage I

**Ziele**

- SuS bauen die Elektronik gemäß Schaltplan auf der Grundplatte auf.
- Sie führen erste Teiltests der einzelnen Komponenten durch.

**Inhalte / Ablauf (Kurz)**

1. Schaltplan & Pinbelegung gemeinsam besprechen (Projektor/Dokumentenkamera).  
2. Gruppenarbeit: Arduino, Breadboard und Sensor/Aktor-Komponenten auf Grundplatte positionieren und verdrahten.  
3. Teiltests: Jede Gruppe prüft nacheinander DHT, HC-SR04, Water-Sensor, LEDs, Buzzer, Display (ggf. mit Testsketches).  

**Dokumentation**

- Fotos vom Aufbau, Markierung von Fehlern und Lösungen im Projektprotokoll.

---

### Doppelstunde 8 – Elektronikmontage II (Fehlersuche & Ordnung)

**Ziele**

- SuS beheben typische Fehler (falsche Pins, lose Kabel, gemeinsame Masse).
- Sie ordnen die Kabel sinnvoll und machen das Modell „wartungsfreundlich“.

**Inhalte / Ablauf (Kurz)**

1. Kurzer Input: „Typische Fehlerbilder“ (nichts leuchtet, Sensor liefert 0, Display bleibt dunkel).  
2. Checklisten-Arbeit in Gruppen (z. B. „5-Punkte-Fehlersuche“: Strom, GND, Pin, Code, Bauteil).  
3. Kabelmanagement mit Kabelbindern / Kabelkanälen.  
4. Erste Gesamtfunktionsprüfung mit einem einfachen Kombinationssketch (z. B. nur Klimamessung + Ampel).  

---

### Doppelstunde 9 – Programmierung Gesamtsystem

**Ziele**

- SuS fügen die einzelnen Funktionen im Arduino-Sketch zusammen.
- Sie nutzen eine nicht-blockierende Logik (`millis()`), damit alle Sensoren/Aktoren quasi parallel arbeiten.

**Inhalte / Ablauf (Kurz)**

1. Struktur des Gesamt-Sketches: Setup, Loop, Funktionsbausteine.  
2. Gemeinsam am Beamer: Ablaufplan / Struktogramm der Logik (z. B. Einparkhilfe, Klimamessung, Wasseralarm, Alarmzustand).  
3. Gruppenarbeit am PC:
   - fertigen Beispielcode (Version 1.5) verstehen, kommentieren und anpassen (z. B. Schwellen, Texte, Zeitintervalle).  
   - eigene Erweiterungen (z. B. zusätzliche Statusmeldungen, andere Blinkmuster).  
4. Testläufe an den Modellen, protokollierte Fehlersuche.

**Differenzierung**

- Basis: Arbeiten mit kommentiertem Beispielsketch, kleinere Parameteränderungen.  
- Plus: Eigene Funktionsbausteine entwerfen, Zustandsautomaten erweitern (weitere Alarmmodi).

---

### Doppelstunde 10 – Test, Präsentation & Reflexion

**Ziele**

- SuS prüfen ihr System systematisch und präsentieren die Funktionsweise.
- Sie reflektieren Stärken/Schwächen ihres Modells sowie mögliche Weiterentwicklungen.

**Inhalte / Ablauf (Kurz)**

1. **Systemtest**: Checkliste mit allen Anwendungsszenarien (Klimamessung, Einparkhilfe, Wasseralarm, Alarmfunktion).  
2. **Kurzpräsentationen** (je Gruppe 3–5 Minuten):
   - Funktionsdemo (Live)  
   - Erklärung: Welche Sensoren/Aktoren? Wie funktioniert die Logik grob?  
   - Was lief gut? Wo gab es Probleme?  
3. **Reflexion** (schriftlich oder mündlich):
   - „Was würdest du bei Version 2.0 verändern?“  
   - „Wo ist so ein System im echten Leben sinnvoll – und welche Risiken siehst du?“  

---

## 5. Differenzierung & Inklusion

- **Leistungsschwächere SuS**
  - mehr Anleitung bei Verkabelung (Steckbilder), vorgefertigte Test-Sketche.
  - Fokus auf Funktionsverständnis und sichere Bedienung.
- **Leistungsstärkere SuS**
  - eigenständige Erweiterungen (z. B. zusätzliche Sensoren, neue Meldungen).
  - Übernahme von Rollen wie „Fehlerdetektiv“ oder „Dokumentationsverantwortlicher“.
- **Inklusive Elemente**
  - klare Rollenteilung in Gruppen (Bau, Code, Doku, Test).  
  - Arbeit mit Infografiken, Fotos, Piktogrammen; ggf. sprachlich reduzierte Arbeitsaufträge.

---

## 6. Leistungsbewertung (Vorschlag)

- **Produkt (ca. 60 %)**
  - Funktionsfähigkeit des Modells (mind. zwei Anwendungsszenarien laufen stabil).
  - Sauberer Aufbau (Mechanik, Elektronik), Einhaltung Sicherheitsvorgaben.
- **Prozess (ca. 20 %)**
  - Teamarbeit, Zuverlässigkeit, Umgang mit Fehlern, Einhaltung der Arbeitssicherheit.
- **Präsentation/Reflexion (ca. 20 %)**
  - Fachliche Darstellung der Funktionsweise (Bezug auf EVA & Sensor/Aktor-System).
  - Reflexion zu Energieeffizienz, Sicherheit und Datenschutz im Smart-Home-Kontext.

---

## 7. Mögliche Erweiterungen (für Folgekurs / AG)

- Integration eines ESP32 für WLAN-Anbindung und Web-Dashboard.
- Einsatz zusätzlicher Sensoren (LDR, Regensensor) und komplexerer Regelstrategien.
- Fächerübergreifende Projekte mit Physik (elektrische Größen, Sensorik), Informatik (Algorithmen, Datenstrukturen) und Gemeinschaftskunde (Datenschutz, gesellschaftliche Auswirkungen von Smart-Home-Technik).
