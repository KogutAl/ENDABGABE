# Interaktive Detektivgeschichte
#### (*Semesterendprojekt Physical Computing - SoSe22 von Alona Kogut*)
 &nbsp;

![Bild zeigt Detektiv und seine Ausrüstung](https://static.vecteezy.com/system/resources/previews/002/183/856/original/detective-accessories-in-retro-style-on-background-vector.jpg)

---
### **1) Konzept**
---
Schlüpfe in die Rolle des Detektiven XY und löse den Mord, der sich innerhalb eines Raum abgespielt hat. Alle Antworten befinden sich in diesem einen Zimmer. Suche nach Hinweisen und untersuche diese, um Tonspuren oder visuelle Effekte zu aktivieren, die auf die Aufklärung deuten könnten. Damit der Detektiv eine logische Gedankenkette bilden kann, ist es wichtig die Komponenten in der korreten Abfolge zu untersuchen.

 &nbsp;
 
---
### **2) Komponenten**
---

- Arduino
- Pappboard
- Kupferband/Aluminiumband
- Pins/Stecknadeln
- Draht

 &nbsp;
 
---
### **3) Wie funktioniert die interaktive Story?**
---

#### **Die Effekte**

Die Kurzgeschichte soll durch sowohl kleine visuelle Effekte, als auch narrative Events erzählt werden. 
Was ich mir als interaktive Schnittstellen, entweder als simple Aktionen oder Rätsel, für den Spieler vorstellen kann, wären folgende :

 &nbsp;

- Miniklavierstück durch Button drücken (Seperate Komponente)
- Aktivierung eines Motors (Rotation) eines Objektes (Bücherregal)
- Aktiverung eines weiteren Motors (öffnet eine geheime Klappe)
- LED-Einschaltung durch Buttons
- Starten narrativer Events durch Schließen eines Stromkreises
- oder durch Unterbrechung eines Stromkreises


 &nbsp;
 
---
### **4) Schaltplan**
---

WIP

 &nbsp;
 
---
### **5) Dokumentation/Ablauf**
---

#### **TESTLAUF Nr. 1 - Einschalten LED durch switch**

 &nbsp;
 

**Code**

```
include <Arduino.h>

const int buttonPin = 7;     
const int narrativePin =  6;     
int buttonState = 0;                        // Variable liest PushButton Status

void setup() {
  
  pinMode(narrativePin, OUTPUT);           // Pin 6 ist narrativePin OUTPUT  
  pinMode(buttonPin, INPUT_PULLUP);        // Pin 7 ist buttonPin INPUT
}

void step1(){                              // Narrative Schritt 1
  digitalWrite(narrativePin, HIGH); 
}

void loop() {

  if (buttonState){                        // liest PushButton Wert
  buttonState = digitalRead(buttonPin);
  }
  if (buttonState == LOW) {               // Wird Button gedrückt, dann... 
    step1();                              // Führe Schritt 1 durch 
  }

  else {
    digitalWrite(narrativePin, LOW);      // führt keinen Schritt durch
  }
}
```
 &nbsp;
 
 *ERGEBNIS*
 Die LED schaltet sich aus durch Schließung des Stromkreises
 
 &nbsp;
 
 
 #### **TESTLAUF Nr. 2 - LED blinkt (Licht flackern)**

 &nbsp;
 

**Code**

```
#include <Arduino.h>

const int blinkLedPin = 2;        

void setup() {
  pinMode(blinkLedPin, OUTPUT);
}

void loop() {
  digitalWrite(blinkLedPin, HIGH);
  delay(3000);
  digitalWrite(blinkLedPin, LOW);
  delay (500);
  digitalWrite(blinkLedPin, HIGH);
  delay(2000);
  digitalWrite(blinkLedPin, LOW);
  delay (100);
}
```
 &nbsp;
 
 ---
### **6) Reflektion**
---

WIP

 &nbsp;
 
[Recherche_1](https://www.youtube.com/watch?v=jco-uU5ZgEU)
[Recherche_2](https://www.arduinoplatform.com/subscription-projects/create-a-touch-button-with-copper-aluminum-foil/)
[Recherche_3](https://www.kobakant.at/DIY/?p=8906)
[Recherche_4](https://mehackit.org/en/courses/electronics_and_programming_basics/02-switch-stuff-on-and-off/03-exercise-1/)
[Pressure_Switch](https://www.instructables.com/Use-a-DIY-Pressure-Plate-Switch-to-Automate-Your-H/)

 &nbsp;
