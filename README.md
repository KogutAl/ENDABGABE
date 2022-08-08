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
 
 ##### ERGEBNIS
 Die LED schaltet sich, durch Schließung des Stromkreises, aus
 &nbsp;
 
 ![LED ist an, Münze liegt nicht auf Switch](https://github.com/KogutAl/ENDABGABE/blob/main/pic_SWITCH_1.jpg)
 ![LED ist aus, Münze liegt auf Switch](https://github.com/KogutAl/ENDABGABE/blob/main/pic_SWITCH_2.jpg)
 
 
 &nbsp;
 
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
 
  
 ##### ERGEBNIS
 
 Wenn der Knopf gedrückt wird, erfolgt eine "Licht-Flacker" Simulation. Dies ist eine Abfolge von An- und Ausschalten der LED mit verschiedenen "Delay" Angaben.
 &nbsp;
 
 ![Steckbrett mit Knopf, LED brennt](https://github.com/KogutAl/ENDABGABE/blob/main/pic_BLINKButton.jpg)
 
 &nbsp
 
 ---

 #### **TESTLAUF Nr. 3 - Erprobung einer State Machine mit LED)**

 &nbsp;
 

**Code**

```
#include <Arduino.h>

  int LedPin = 9;
  int buttonLedPin = 10;

void setup() {

  pinMode(LedPin, OUTPUT);                            // Pin 9 ist OUTPUT, LED leuchtet
  pinMode(buttonLedPin, INPUT_PULLUP);                // Pin 10 ist INPUT, Button

  digitalWrite (LedPin, LOW);                         // Ausgangszustand LED
}

void loop() {
  if (digitalRead(buttonLedPin) == LOW){              // wenn Button gedrückt wird...
    digitalWrite(LedPin, !digitalRead(LedPin));       // starte Output (LED leuchtet) und lese Zustand der LED (an oder aus)
  }
}
```
 &nbsp;
 
 ##### ERGEBNIS
 Wenn der Knopf gedrückt wird, leuchtet die LED auf. Sobald die Taste ein weiteres Mal gedrückt wird, geht sie wieder aus.
 Ein Button kann somit 2 Befehle ausführen -> LED ein- und ausschalten. Es herrscht ein Wechsel des LED Zustandes.
 &nbsp;
 
 ![Steckbrett mit Knopf und LED, LED ist aus](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_1.jpg)
 ![Steckbrett mit Knopf und LED, LED ist an, nachdem Knopf gedrückt wird](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_2.jpg)
 
  &nbsp;
 
  ---
 
  #### **TESTLAUF Nr. 4 - Ausarbeitung der State-Machine**

 &nbsp;
 

**Code**

```
Here comes the code
```
 &nbsp;
 
 ##### ERGEBNIS
 Wenn der Knopf gedrückt wird, leuchtet die LED auf. Sobald die Taste ein weiteres Mal gedrückt wird, geht sie wieder aus.
 Ein Button kann somit 2 Befehle ausführen -> LED ein- und ausschalten. Es herrscht ein Wechsel des LED Zustandes.
 &nbsp;
 
 ![Steckbrett mit Knopf und LED, LED ist aus](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_1.jpg)
 ![Steckbrett mit Knopf und LED, LED ist an, nachdem Knopf gedrückt wird](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_2.jpg)
 
  &nbsp;
 
  ---
 
  #### **TESTLAUF Nr. 5 - Textausgabe durch Button Push**

 &nbsp;
 

**Code (nicht meiner - Referenzmaterial**

[Die Quelle](https://docs.arduino.cc/built-in-examples/usb/KeyboardMessage)

```
/*
  Keyboard Message test

  For the Arduino Leonardo and Micro.

  Sends a text string when a button is pressed.

  The circuit:
  - pushbutton attached from pin 4 to +5V
  - 10 kilohm resistor attached from pin 4 to ground

  created 24 Oct 2011
  modified 27 Mar 2012
  by Tom Igoe
  modified 11 Nov 2013
  by Scott Fitzgerald

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/KeyboardMessage
*/

#include "Keyboard.h"

const int buttonPin = 4;          // input pin for pushbutton
int previousButtonState = HIGH;   // for checking the state of a pushButton
int counter = 0;                  // button push counter

void setup() {
  // make the pushButton pin an input:
  pinMode(buttonPin, INPUT);
  // initialize control over the keyboard:
  Keyboard.begin();
}

void loop() {
  // read the pushbutton:
  int buttonState = digitalRead(buttonPin);
  // if the button state has changed,
  if ((buttonState != previousButtonState)
      // and it's currently pressed:
      && (buttonState == HIGH)) {
    // increment the button counter
    counter++;
    // type out a message
    Keyboard.print("You pressed the button ");
    Keyboard.print(counter);
    Keyboard.println(" times.");
  }
  // save the current button state for comparison next time:
  previousButtonState = buttonState;
}

```
 &nbsp;
 
 ##### ERGEBNIS
 Wenn der Knopf gedrückt wird, leuchtet die LED auf. Sobald die Taste ein weiteres Mal gedrückt wird, geht sie wieder aus.
 Ein Button kann somit 2 Befehle ausführen -> LED ein- und ausschalten. Es herrscht ein Wechsel des LED Zustandes.
 &nbsp;
 
 ![Steckbrett mit Knopf und LED, LED ist aus](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_1.jpg)
 ![Steckbrett mit Knopf und LED, LED ist an, nachdem Knopf gedrückt wird](https://github.com/KogutAl/ENDABGABE/blob/main/p_StateMachineButton_2.jpg)
 
 ---
### **6) Reflektion**
---

WIP

 &nbsp;
 
[Arduino Code Referenzen und Erklärungen](https://arduinogetstarted.com/de/reference/digitalread) 
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
[Textausgabe](https://docs.arduino.cc/built-in-examples/usb/KeyboardMessage)

 &nbsp;
