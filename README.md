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
 
 &nbsp;
 Die LED schaltet sich, durch Schließung des Stromkreises, aus
 &nbsp;
 
 ![LED ist an, Münze liegt nicht auf Switch](https://github.com/KogutAl/ENDABGABE/blob/main/pic_SWITCH_1.jpg)
 ![LED ist aus, Münze liegt auf Switch](https://github.com/KogutAl/ENDABGABE/blob/main/pic_SWITCH_2.jpg)
 
 
 &nbsp;
 
 ---

 #### **TESTLAUF Nr. 3 - Erprobung einer State Machine mit LED)**

 &nbsp;
 

**Code**

```
#include <Arduino.h>

const int blinkLedPin = 2;                  
const int buttonBlinkPin = 3;               

void setup() {
  pinMode(blinkLedPin, OUTPUT);               // Pin 2 ist Output -> LED blinkt
  pinMode(buttonBlinkPin, INPUT_PULLUP);      // PIN 3 ist Input -> durch Knopfdruck blinkt LED
}

void loop() {

  if (digitalRead (buttonBlinkPin) == LOW ){  // wenn Knopf gedrückt ist...
        digitalWrite(blinkLedPin, HIGH);      // geht LED an...
        delay(3000);                          // für 3000ms...
        digitalWrite(blinkLedPin, LOW);       // danach geht aus..
        delay (500);                          // für 500ms...
        digitalWrite(blinkLedPin, HIGH);      // geht wieder an usw.
        delay(2000);
        digitalWrite(blinkLedPin, LOW);
        delay (100);
        digitalWrite(blinkLedPin, HIGH);
        delay(200);
        digitalWrite(blinkLedPin, LOW);
        delay (50);
  }
  if (digitalRead (buttonBlinkPin) == HIGH ){ // wenn Knopf nicht gedrückt ist
        digitalWrite(blinkLedPin, LOW);       // bleibt LED aus
  }

}
```
 &nbsp;
 
  
 *ERGEBNIS*
 
 &nbsp;
 Durch Drücken des Knopfes erfolgt eine "Licht-Flacker Simulation" mit Hilfe des Ein- und Ausschaltens der LED
 &nbsp;
 
 ![Steckbrett mit Knopf, LED brennt](https://github.com/KogutAl/ENDABGABE/blob/main/pic_BLINKButton.jpg)
 
 &nbsp
 
  ---

 #### **TESTLAUF Nr. 2 - LED blinkt durch Knopfdruck (simuliert Licht flackern)**

 &nbsp;
 

**Code**

```
#include <Arduino.h>

const int blinkLedPin = 2;                  
const int buttonBlinkPin = 3;               

void setup() {
  pinMode(blinkLedPin, OUTPUT);               // Pin 2 ist Output -> LED blinkt
  pinMode(buttonBlinkPin, INPUT_PULLUP);      // PIN 3 ist Input -> durch Knopfdruck blinkt LED
}

void loop() {

  if (digitalRead (buttonBlinkPin) == LOW ){  // wenn Knopf gedrückt ist...
        digitalWrite(blinkLedPin, HIGH);      // geht LED an...
        delay(3000);                          // für 3000ms...
        digitalWrite(blinkLedPin, LOW);       // danach geht aus..
        delay (500);                          // für 500ms...
        digitalWrite(blinkLedPin, HIGH);      // geht wieder an usw.
        delay(2000);
        digitalWrite(blinkLedPin, LOW);
        delay (100);
        digitalWrite(blinkLedPin, HIGH);
        delay(200);
        digitalWrite(blinkLedPin, LOW);
        delay (50);
  }
  if (digitalRead (buttonBlinkPin) == HIGH ){ // wenn Knopf nicht gedrückt ist
        digitalWrite(blinkLedPin, LOW);       // bleibt LED aus
  }

}
```
 &nbsp;
 
  
 *ERGEBNIS*
 
 &nbsp;
 Durch Drücken des Knopfes erfolgt eine "Licht-Flacker Simulation" mit Hilfe des Ein- und Ausschaltens der LED
 &nbsp;
 
 ![Steckbrett mit Knopf, LED brennt](https://github.com/KogutAl/ENDABGABE/blob/main/pic_BLINKButton.jpg)
 
 
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
[MP3 in Code umwandeln](https://www.youtube.com/watch?v=aaqaAXlZbuc)
[Star Wars Theme](https://www.youtube.com/watch?v=RVyLqXz-xvU)
[Star Wars Theme-Tutorial](https://42bots.com/?s=melody)
[State Machine](https://www.mikrocontroller.net/articles/Statemachine)
[State Machine - Ampelbeispiel](https://www.youtube.com/watch?v=AFUAkNXTqfo)

 &nbsp;
