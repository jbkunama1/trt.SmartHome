# 🏠 SmartHome Lienhard – Arduino-Modellhaus

[![Made for Education](https://img.shields.io/badge/Made%20for-Sek%20I%20Technik-blue)](#-einsatz-im-unterricht)
[![Curriculum](https://img.shields.io/badge/Bildungsplan-BW%202016-success)](#-bildungsplan--kompetenzen)
[![Arduino](https://img.shields.io/badge/Platform-Arduino%20UNO-orange)](#-technisches-konzept)
[![License](https://img.shields.io/badge/License-MIT-lightgrey)](#-lizenz)

> Ein modular aufgebautes Smart‑Home-Modellhaus für den Technikunterricht (Klasse 8–10) in Baden‑Württemberg.

---

## 📸 Überblick

![SmartHome Logo](media/SmartHome_Logo.jpg)

Das **SmartHome Lienhard** ist ein Arduino‑basiertes Modellhaus, das zentrale Smart‑Home‑Funktionen wie **Klimamessung**, **Einparkhilfe**, **Wasseralarm** und eine **virtuelle Alarmanlage** demonstriert.[^mp1]  
Es wurde speziell für den Einsatz im Unterricht (Sek I, Fach Technik) entwickelt und erfüllt die Anforderungen des Bildungsplans 2016 im Kompetenzbereich *Systeme und Prozesse*.[^bp]

---

## 🎯 Zielgruppe & Kontext

- Schulart: Realschule / Gemeinschaftsschule Sek I  
- Fach: Technik (Wahlpflichtfach)  
- Klassenstufen: 8–10  
- Typischer Einsatz:
  - MP1-Modellprüfung / Langzeitarbeit  
  - Projektunterricht „Smart Home – Das moderne Haus denkt mit“  
  - Demo-Objekt für BO, MINT-Tage, Elternabende  

---

## 🧠 Technisches Konzept

Das Modell folgt konsequent dem **EVA‑Prinzip** (Eingabe – Verarbeitung – Ausgabe).[^mp1]

### Eingabe (Sensoren)

- **DHT‑Sensor**: Temperatur- und Luftfeuchtemessung  
- **HC‑SR04**: Distanzmessung für Einparkhilfe  
- **Water‑Sensor (analog)**: Erkennung von Feuchtigkeit/Wasser  
- **Taster A3**: Virtueller Alarm EIN/AUS  

### Verarbeitung (Mikrocontroller)

- **Arduino UNO** als zentrale Steuereinheit  
- Nicht‑blockierende Programmlogik mit `millis()` statt `delay()`  
- Zustandsautomaten (State Machines) für:
  - Alarmmodus  
  - Wasseralarm / Normalbetrieb  
  - Anzeigewechsel (Temperatur/Luftfeuchte, Statusmeldungen)  

### Ausgabe (Aktoren)

- **LED‑Ampel** (Grün / Gelb / Rot) für Einparkhilfe  
- **Buzzer** als akustischer Alarm  
- **20x4 I²C‑LCD / OLED** zur Darstellung von:
  - Temperatur & Luftfeuchte  
  - Abstand in cm  
  - Status- und Alarmmeldungen  
  - Wasserstand als Balkendiagramm (0–20 Zeichen)

---

## 🧩 Realisierte Funktionen

Die aktuelle Sketch‑Version `SmartHome v1.5` umfasst u. a.:[^code]

- Klimamessung mit DHT-Sensor (Temperatur & Luftfeuchte)  
- Distanzmessung mit HC‑SR04 und Ampel‑Logik:
  - Grün: großer Abstand  
  - Gelb: mittlerer Abstand  
  - Rot: kritischer Abstand (optional mit Buzzer)  
- Virtueller Alarm (Taster A3):
  - Anzeige „Virtueller Alarm AN/AUS“ auf dem Display  
  - definierte Blinksequenzen der LEDs im Alarmfall  
- Wasseralarm:
  - analoger Water‑Sensor am Eingang A0  
  - Textmeldung „WASSER ALARM!“  
  - Balkenanzeige des Wasserstandes (0–20 Zeichen)  
  - blinkende rote LED
- 25 rotierende Statusmeldungen im Normalbetrieb (z. B. „System aktiv“, „Daten stabil“, …)  

Der vollständige Arduino‑Sketch liegt im Ordner [`arduino/`](arduino/).

---

## 🧱 Hardware-Setup

**Zentrale Komponenten**

- Arduino UNO / kompatibles Board  
- DHT‑Sensor (Temp/Feuchte)  
- HC‑SR04 Ultraschallsensor  
- Analoger Water‑Sensor  
- 3× LEDs (Grün, Gelb, Rot) mit Vorwiderständen (ca. 220 Ω)  
- 1× Taster (Alarm)  
- 1× 20x4 I²C‑LCD oder OLED  
- Breadboard, Jumper‑Kabel, USB‑Kabel  
- 5 V‑Versorgung (Arduino‑USB, ggf. zusätzliche 5 V‑Quelle für LEDs/Sensoren)  

**Mechanik & 3D‑Druck**

- Grundplatte: DIN A3 (ca. 297 × 420 mm), Sperrholz / MDF, 3–5 mm  
- 3D‑gedrucktes Haus (Korpus + Dach, z. B. PLA/Holzfilament)  
- Diverse 3D‑gedruckte Halterungen:
  - Sensorhalterungen (DHT, HC‑SR04, Water‑Sensor)  
  - Ampelgehäuse  
  - Elektronikwanne / Kabelkanäle  
- Dekoration: Straße, Rasen, Zaun, Schild „SmartHome“  

Eine detaillierte Stückliste (Elektronik & 3D‑Druck) findest du in [`docs/`](docs/) und [`3d-print/`](3d-print/).[^stl]

---

## 🏫 Bildungsplan & Kompetenzen

Das Projekt ist passgenau zum **Bildungsplan 2016 – Technik, Sek I, BW** entwickelt.[^bp]

**Kompetenzbereich 3.2.2 „Systeme und Prozesse“**

- K 12: Aufbau und Funktion eines Mikrocontroller‑Systems beschreiben und anwenden  
- K 13: Sensoren zur Erfassung physikalischer Größen einsetzen  
- K 14: Aktoren zur Ausgabe steuern  
- K 15: Einfache Programme für Mikrocontroller erstellen  
- K 16: Schaltpläne interpretieren und erstellen  
- K 17: Steuerungsabläufe planen und dokumentieren  
- K 18: Regelkreise analysieren und umsetzen (z. B. Schwellwertlogik Einparkhilfe)

**Prozessbezogene Kompetenzen**

- Erkenntnisgewinnung: Experimente mit Sensoren, Schwellwertoptimierung, Fehlersuche  
- Herstellung & Nutzung: Holzbearbeitung, 3D‑Druck, Verdrahtung, Programmierung  
- Kommunikation: technische Dokumentation, Präsentationen  
- Bewertung: Reflexion zu Sicherheit, Energieeffizienz, Datenschutz im Smart‑Home‑Kontext  

**Leitperspektiven**

- **BNE**: Energieeffizienz, ressourcenschonender 3D‑Druck, sinnvolle Automatisierung  
- **Medienbildung**: Programmierung, Datenerfassung und ‑verarbeitung  
- **Berufliche Orientierung**: Einblicke in Elektro‑, Gebäude‑ und Automatisierungstechnik, Mechatronik  

---

## 📚 Einsatz im Unterricht

Dieses Repository unterstützt zwei typische Einsatzszenarien:

### 1. 20‑Minuten‑Einstiegseinheit

- kurzer Impuls zu Smart‑Home im Alltag  
- Einführung in das EVA‑Prinzip  
- Live‑Demo der Kernfunktionen (Einparkhilfe, Klimamessung, Wasseralarm, Alarmmodus)  
- Diskussionsanstoß zu Chancen/Risiken (Komfort, Sicherheit, Datenschutz)

➡️ Ausformulierte Verlaufsplanung: [`unterricht/20min_Einstieg_SmartHome.md`](unterricht/20min_Einstieg_SmartHome.md)

### 2. Mehrwöchiges Projekt „Smart‑Home-Modellhaus“

Umfang: ca. 10 Doppelstunden (modular kürzbar).[^mp1]

**Mögliche Module**

1. Systemanalyse & EVA  
2. Arduino‑Basics & LED‑Übung  
3. Sensorik (DHT, HC‑SR04, Water‑Sensor)  
4. Aktorik (LED‑Ampel, Buzzer, Display)  
5. Mechanik (Grundplatte, Layout)  
6. 3D‑Druck (Haus, Halterungen)  
7. Elektronikaufbau I (Verdrahtung, Teiltests)  
8. Elektronikaufbau II (Fehlersuche, Kabelmanagement)  
9. Programmierung Gesamtsystem (millis‑Logik)  
10. Systemtest, Präsentation & Reflexion  

➡️ Ausführlicher Unterrichtsentwurf: [`unterricht/Projekt_ArduinoSmartHome_Sequenz.md`](unterricht/Projekt_ArduinoSmartHome_Sequenz.md)

---

## 🧪 Unterrichtsbausteine (modular nutzbar)

Jeder Baustein kann auch als eigenständige Einheit eingesetzt werden:

- **Sensorik‑Workshop**: einzelne Sensoren testen und auswerten  
- **Aktorik‑Workshop**: Ausgabe über LEDs, Buzzer, Display gestalten  
- **3D‑Druck‑Projekt**: Haus & Halterungen im CAD entwerfen und fertigen  
- **Programmier‑Lab**: Zustandsautomaten, nicht‑blockierende Logik, Debugging  
- **Reflexionsmodul**: Datenschutz, Energie, Komfort vs. Abhängigkeit diskutieren  

Ideal auch für Vertretungsstunden, Projekttage oder MINT‑AGs.

---

## 📂 Repository-Struktur

```text
arduino-smarthome-lienhard/
├─ README.md
├─ /arduino/              → Arduino-Sketch & Code-Snippets
│  └─ SmartHome_V1_5_Water.ino
├─ /docs/                 → MP1-Dokumentation, Briefing, Pinbelegung, Stücklisten
│  ├─ 01_Smart-Home-MP1-Dokumentation.pdf
│  ├─ 99_BriefingHandout.pdf
│  └─ 99_ArduinoCode.Pin.Funktion_Smarthome-V1-5-Water.pdf
├─ /3d-print/             → 3D-Druck-Stückliste, ggf. STL-Dateien
│  └─ 99_SmartHome-3D-Druck-Stuckliste.pdf
├─ /media/                → Logo, Infografiken, Fotos, Videos
│  ├─ SmartHome_Logo.jpg
│  ├─ SmartHome_Infografik_01.jpg
│  ├─ SmartHome_Infografik_02.jpg
│  ├─ SmartHome_Infografik_03_SuS.jpg
│  ├─ fotos_fertiges_modell/
│  └─ video/
├─ /unterricht/           → Unterrichtsentwürfe, Arbeitsblätter
│  ├─ 20min_Einstieg_SmartHome.md
│  └─ Projekt_ArduinoSmartHome_Sequenz.md
└─ /license/
   └─ LICENSE             → MIT-Lizenztext
```

---

## ⚙️ Installation & Inbetriebnahme (Kurz)

1. **Repository klonen / Dateien herunterladen**  
2. **Arduino-Sketch öffnen**:  
   - `arduino/SmartHome_V1_5_Water.ino` in der Arduino IDE öffnen  
   - ggf. Board & Port konfigurieren  
3. **Bibliotheken installieren** (über Bibliotheksverwalter):
   - `DHT`  
   - `LiquidCrystal_I2C` oder `Adafruit_SSD1306` (je nach Display)  
   - `Wire` (I²C – meist schon vorhanden)  
4. **Schaltplan aufbauen** / Modell anschließen  
5. **Sketch hochladen & Funktionen testen**  

---

## 🧩 Weiterentwicklungsideen

- Integration eines **ESP32** für WLAN‑Anbindung und Web‑Dashboard  
- zusätzliche Sensoren (LDR, Regensensor, Gassensor) für weitere Szenarien  
- Datenlogging (Temperatur, Luftfeuchtigkeit, Abstand, Wasserstand)  
- Energieauswertungen (z. B. simulierte Heizoptimierung)  
- Übertragung auf andere Kontexte (z. B. Gewächshaus‑Automatisierung)

---

## 🤝 Mitmachen & Anpassung

Du kannst dieses Projekt gerne:

- an deine schulische Infrastruktur anpassen,  
- neue Unterrichtsmaterialien ergänzen,  
- alternative Sketch‑Versionen (z. B. mit anderen Sensoren) beitragen.

Pull Requests mit **Code‑Verbesserungen**, **Unterrichtsbausteinen** oder **Übersetzungen** sind willkommen. 🙌

---

## 📜 Lizenz

Dieses Projekt (Code, Unterrichtsmaterialien und 3D‑Druck‑Dateien in diesem Repository) steht unter der **MIT-Lizenz**.

© 2026 Daniel Lienhard.

Die vollständigen Lizenzbedingungen findest du in der Datei [`license/LICENSE`](license/LICENSE). Kurzfassung:

> Permission is hereby granted, free of charge, to any person obtaining a copy  
> of this software and associated documentation files (the "Software"), to deal  
> in the Software without restriction, including without limitation the rights  
> to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
> copies of the Software, and to permit persons to whom the Software is  
> furnished to do so, subject to the following conditions:  
>  
> The above copyright notice and this permission notice shall be included in all  
> copies or substantial portions of the Software.

Hinweis: Die verwendeten Arduino‑Libraries und ggf. externe Grafiken/Bilder/Videos unterliegen weiterhin ihren jeweiligen Original‑Lizenzen und sind davon unberührt. Bitte prüfe vor Veröffentlichung immer die Rechte an eingebundenen Medien.

---

[^mp1]: Siehe ausführliche MP1‑Dokumentation „Smart‑Home‑Modellhaus“ im Ordner `docs/`.  
[^bp]: Bildungsplan 2016, Technik, Sekundarstufe I, Baden‑Württemberg.  
[^code]: Technische Beschreibung & Sketch `SmartHome v1.5` in `99_ArduinoCode.Pin.Funktion_Smarthome-V1-5-Water.pdf`.  
[^stl]: 3D‑Druck‑Stückliste in `99_SmartHome-3D-Druck-Stuckliste.pdf`.
