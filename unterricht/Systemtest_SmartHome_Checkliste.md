# Systemtest-Checkliste – SmartHome Lienhard

## 1. Ziel des Systemtests

Die Checkliste hilft dir und den Schüler*innen, alle Funktionen des Smart-Home-Modellhauses systematisch zu überprüfen:

- Klimamessung (Temperatur/Luftfeuchte)
- Einparkhilfe (Abstand + Ampel)
- Wasseralarm (Sensor + Anzeige)
- Virtueller Alarm (Taster + Blinkmuster)

> Tipp: Test immer mit eingestecktem USB-Kabel und stabilem 5-V-Netzteil durchführen.

---

## 2. Allgemeine Vorbereitung

- [ ] Arduino ist per USB mit dem PC oder Netzteil verbunden.  
- [ ] Sketch `SmartHome v1.5` ist erfolgreich hochgeladen (keine Fehlermeldung in der IDE).  
- [ ] Alle Kabel sitzen fest, keine losen Verbindungen sichtbar.  
- [ ] Gemeinsame Masse (GND) zwischen Arduino, Sensoren und Aktoren ist hergestellt.  
- [ ] Display zeigt beim Start eine Begrüßungsnachricht (z. B. „SmartHome Lienhard“).

---

## 3. Klimamessung (DHT-Sensor)

**Ziel:** Temperatur und Luftfeuchtigkeit werden korrekt erfasst und angezeigt.

- [ ] DHT-Sensor ist außen am Haus befestigt und mit dem richtigen Pin (D2) verbunden.  
- [ ] Auf dem Display erscheint in einer Zeile **Temp** oder **Hum** mit sinnvollen Werten (z. B. 18–28 °C, 30–70 % RH).  
- [ ] Beim Anhauchen des Sensors steigt die Luftfeuchtigkeit deutlich an (z. B. von 40 % auf >60 %).  
- [ ] Nach einigen Sekunden kehren die Werte wieder in den Normalbereich zurück.

**Fehlernotizen (optional):**

- [ ] Keine Anzeige → Verkabelung DHT prüfen, Pull‑Up‑Widerstand, Bibliothek installiert?  
- [ ] Werte „nan“ oder 0 → Datenleitung, Pin‑Definition im Sketch kontrollieren.

---

## 4. Einparkhilfe (HC-SR04 + Ampel-LEDs)

**Ziel:** Abstand wird gemessen und über die LED-Ampel visualisiert.

- [ ] HC-SR04 ist an der Einfahrt ausgerichtet, TRIG/ECHO korrekt (D8/D9) angeschlossen.  
- [ ] Auf dem Display wird der Abstand in cm angezeigt (`Abstand xx.x cm` oder `Abstand -- cm`).  
- [ ] Bei großem Abstand (z. B. >40 cm) leuchtet nur die **grüne** LED.  
- [ ] Bei mittlerem Abstand (ca. 20–40 cm) leuchtet die **gelbe** LED.  
- [ ] Bei geringem Abstand (<20 cm) leuchtet die **rote** LED, optional mit Buzzer.  
- [ ] Wenn kein Objekt erkannt wird, zeigt das Display `Abstand -- cm` und alle LEDs sind aus.

**Fehlernotizen (optional):**

- [ ] Abstand immer 0 oder sehr groß → Ausrichtung des Sensors, Pinbelegung, Zeitüberschreitung prüfen.  
- [ ] LEDs reagieren nicht → Pins D11/D12/D13, Vorwiderstände, `if`-Bedingungen im Sketch prüfen.

---

## 5. Wasseralarm (Water-Sensor A0)

**Ziel:** Feuchtigkeit wird erkannt und als Alarm + Balkenanzeige dargestellt.

- [ ] Water-Sensor ist an A0 angeschlossen und an einer sinnvollen Stelle im Modell montiert.  
- [ ] Im trockenen Zustand wird kein Wasseralarm angezeigt, Balken bleibt leer.  
- [ ] Bei Kontakt mit Wasser/feuchtem Tuch:
  - [ ] erscheint der Text **„WASSER ALARM!“** im Display.  
  - [ ] blinkt die **rote LED** deutlich sichtbar.  
  - [ ] wird der Wasserstand als Balken (0–20 Zeichen) angezeigt.  
- [ ] Beim Entfernen der Feuchtigkeit verschwindet der Alarm nach kurzer Zeit.

**Fehlernotizen (optional):**

- [ ] Alarm schon bei minimaler Feuchtigkeit → Schwellwert im Sketch (z. B. `WATERTHRESHOLD 500`) anpassen.  
- [ ] Keine Reaktion → Verkabelung A0, VCC/GND, Analogeingang im Code prüfen.

---

## 6. Virtueller Alarm (Taster A3)

**Ziel:** Alarmzustand kann per Taster umgeschaltet werden, Anzeige + Blinkmuster reagieren.

- [ ] Alarmtaster ist an A3 angeschlossen (`INPUT_PULLUP` im Sketch gesetzt).  
- [ ] Kurzer Tastendruck schaltet den virtuellen Alarm **ein**:
  - [ ] Display zeigt z. B. **„Virtueller Alarm AN“**.  
  - [ ] definierte Blinksequenz der LEDs ist sichtbar (z. B. rot/gelb).  
- [ ] erneuter Tastendruck schaltet den Alarm **aus**:
  - [ ] Display zeigt **„Virtueller Alarm AUS“**.  
  - [ ] LEDs kehren in den Normalzustand zurück.  
- [ ] Alarmzustand bleibt auch nach einigen Sekunden stabil (kein Flackern).

**Fehlernotizen (optional):**

- [ ] Taster reagiert gar nicht → Verdrahtung A3, interne Pull‑Ups, Entprellung im Code prüfen.  
- [ ] Mehrfachschaltungen bei einem Tastendruck → Debounce‑Zeit (`debounceTime`) erhöhen.

---

## 7. Statusmeldungen & Normalbetrieb

**Ziel:** Im Normalbetrieb (kein Wasseralarm, kein aktueller Alarmwechsel) zeigt das System zyklisch Statusmeldungen.

- [ ] Im unteren Displaybereich werden in größeren Abständen kurze Statusmeldungen angezeigt (z. B. „System aktiv“, „Daten stabil“).  
- [ ] Statusmeldungen werden nur im Normalbetrieb gezeigt, nicht während Alarmmeldungen.  

---

## 8. Abschluss

- [ ] Alle vier Funktionsteile (Klimamessung, Einparkhilfe, Wasseralarm, virtueller Alarm) wurden getestet.  
- [ ] Auffälligkeiten oder Fehler wurden im Protokoll / Heft notiert.  
- [ ] Ggf. To‑Do‑Liste für nächste Stunde erstellt (z. B. „Schwellwerte anpassen“, „I²C-Adresse prüfen“).
