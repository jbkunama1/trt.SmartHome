# Lehrernotizen – Troubleshooting SmartHome Lienhard

Diese Notizen fassen typische Fehler und Lösungsstrategien zusammen, die während Aufbau und Inbetriebnahme des Smart-Home-Modells häufig auftreten.[^mp1][^code]

---

## 1. Allgemeine Hinweise

- Immer zuerst **Stromversorgung** und **gemeinsame Masse (GND)** prüfen. Viele Fehler liegen an fehlenden/losen GND-Verbindungen.
- Systematische Fehlersuche:  
  1. Mechanik ok? (Sensor sitzt richtig, Kontakte sauber)  
  2. Verdrahtung ok? (Pins, Stecker, Polung)  
  3. Code ok? (richtige Pins, Bibliotheken, Adressen)  
  4. Bauteil defekt?

---

## 2. Display / I²C-Probleme

**Symptom:** Display bleibt schwarz oder zeigt nur Kästchen.

Mögliche Ursachen & Lösungen:

- Falsche I²C-Adresse:
  - Viele 20x4 LCDs nutzen `0x27` oder `0x3F`, OLEDs häufig `0x3C` oder `0x3D`.[^mp1]
  - Mit einem einfachen „I²C-Scanner“-Sketch die Adresse ermitteln und im Code anpassen.
- Keine oder fehlerhafte `SDA/SCL`-Verbindung:
  - Arduino UNO: `SDA` an A4, `SCL` an A5.
  - Kabelverlauf und eventuelle Pull‑Up‑Widerstände (typ. 4,7 kΩ) prüfen.[^mp1]
- Kontrast bei LCD:
  - Bei manchen Modulen mit Poti auf dem Backpack den Kontrast einstellen.

---

## 3. Water-Sensor / Wasseralarm

**Symptom 1:** Wasseralarm löst schon bei minimaler Feuchtigkeit aus.

- Schwellwert im Code (`WATERTHRESHOLD`) anpassen.  
  - Beispiel: Erhöhung von 300 auf 500 hat sich bewährt.[^mp1][^code]  
- Schüler*innen können an einem trockenen und nassen Sensor mehrere Messwerte ablesen und einen sinnvollen Schwellwert selbst vorschlagen.

**Symptom 2:** Keine Reaktion auf Wasser.

- Prüfen, ob der Sensor analog (`AO`) an A0 hängt, nicht am digitalen Ausgang.  
- Sicherstellen, dass `pinMode(WATERANALOG, INPUT);` gesetzt ist.[^code]  
- Testsketch verwenden, der nur `analogRead(A0)` auf dem Seriellen Monitor ausgibt.

---

## 4. HC-SR04 / Einparkhilfe

**Symptom:** Abstandswert ist immer 0, sehr groß oder „springt“.

- Ausrichtung: Sensor muss möglichst senkrecht auf das reflektierende Objekt zeigen.  
- Verkabelung: `TRIG` an D8, `ECHO` an D9 (oder entsprechend der Pinbelegung), GND/VCC prüfen.[^mp1][^code]  
- In der `pulseIn`-Funktion ein Timeout setzen (`pulseIn(ECHOPIN, HIGH, 30000)`), um Hänger zu vermeiden.[^code]  
- Test: einfachen Sketch verwenden, der nur Distanz misst und im Seriellen Monitor ausgibt.

---

## 5. DHT-Sensor / Klimamessung

**Symptom:** `nan`‑Werte oder 0 bei Temperatur/Luftfeuchte.

- Datenleitung an korrektem Pin (z. B. D2) und Pull‑Up‑Widerstand (10 kΩ) zwischen VCC und DATA prüfen.[^mp1]  
- Bibliothek: `DHT` muss korrekt installiert und mit dem richtigen Typ (`DHT11` vs. `DHT22`) initialisiert sein.  
- Messintervall nicht zu kurz wählen, DHT‑Sensoren brauchen eine gewisse Zeit zwischen den Messungen.

---

## 6. LEDs, Buzzer & Ampel-Logik

**Symptom:** LEDs bleiben dunkel oder leuchten „falsch“.

- Pinzuordnung prüfen:
  - Z. B. Grün an D11, Gelb an D12, Rot an D13 (inkl. Vorwiderstand).[^^mp1]  
- `pinMode(LEDx, OUTPUT);` im `setup()` nicht vergessen.  
- Testsketch: Nur LEDs nacheinander schalten, um Hardwarefehler auszuschließen.

---

## 7. Taster / Virtueller Alarm

**Symptom:** Alarm reagiert gar nicht oder schaltet mehrmals bei einem Druck.

- Taster gegen GND schalten und `INPUT_PULLUP` verwenden (`pinMode(ALARMPIN, INPUT_PULLUP);`).[^code]  
- Entprellung:
  - `debounceTime` (z. B. 50–100 ms) im Code prüfen und ggf. erhöhen.  
  - Nur bei Zustandswechsel (HIGH → LOW) den Alarmzustand umschalten.

---

## 8. Nicht-blockierende Programmierung (millis)

**Symptom:** System „friert ein“ oder reagiert verzögert.

- Prüfen, ob noch `delay()`-Aufrufe im Code vorhanden sind und diese durch `millis()`-basierte Zeitabfragen ersetzen.[^mp1][^code]  
- Zeitlogik je Funktionsblock klar trennen:
  - Klimamessung (z. B. alle 3 s)  
  - Distanzmessung (z. B. alle 200 ms)  
  - Statusmeldungen (z. B. alle 15 s)

---

## 9. Didaktische Tipps

- Fehler gezielt „einbauen“ (z. B. falsche I²C-Adresse, verkehrtes LED‑Kabel), damit SuS in kleinen Gruppen Fehlersuche üben.  
- Checklistenarbeit fördern: jede Gruppe dokumentiert, welche Schritte sie geprüft hat.  
- Reflexion: SuS sollen am Ende benennen, welcher Fehler am häufigsten vorkam und wie sie ihn künftig vermeiden wollen.

---

[^mp1]: Ausführliche Beschreibung in „01_Smart-Home-MP1-Dokumentation.pdf“.  
[^code]: Details zum Sketch in „99_ArduinoCode.Pin.Funktion_Smarthome-V1-5-Water.pdf“.
