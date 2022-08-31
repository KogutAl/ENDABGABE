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
- Steckboard
- Kupferband/Aluminiumband
- Pins/Stecknadeln
- LEDs
- Laptop (zur Ausgabe narrativen Textes)

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
 
 Dies sind natürlich die "Nice To Have"-Komponenten, die in einem final ausgearbeiteten Projekt schön wären. Als Physical Computing Anfängerin habe ich folgende "Must Haves" Festgelegt:
 
  &nbsp;
  
  - kleine visuelle Effekte durch LEDs
  - Einbauen eines Swicthes mit Kupferpapier
  - simple Knopfsteuerung
  - narrative Ausgabe über den Serial Monitor

 &nbsp;
 
---
### **4) Schaltplan der Endabgabe**
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
 
  #### **TESTLAUF Nr. 4 - Ziel war: Textausgabe durch Button Push**

 &nbsp;
 

**Code (nicht meiner - Referenzmaterial)** -> verworfen

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
  Der Code hat nicht das gemacht was ich mir erhofft hatte.
  Dies lag einfach daran, dass dieser nicht die "simple" Textausgabe über den Serial Monitor ermöglicht, sondern den Input von Text.
  Sprich: Eine Art Keyboard Simulation.
  
 &nbsp;
 
 
  ---
 
  #### **TESTLAUF Nr. 5 - Textausgabe**

 &nbsp;
 

**Code**


```
/*
  #include <Arduino.h>

int button = 6;

void setup() {
  pinMode (button ,INPUT_PULLUP);                   // Pin 6 ist Button Input
  Serial.begin(9600);                               // BAUD Rate, gibt vor in welcher Geschwindigkeit Daten übermittelt werden
  Serial.println("Setup...");
}

void loop() {
  if (digitalRead(button) == LOW){                  // wenn Knopf gedrückt wird
    Serial.println("Knopf wird gedrückt");          // wird Text in Serial Monitor ausgegeben
    delay (4000);                                   // alle 4000ms wird Text ausgegeben
  }

}
```
 &nbsp;
 
 ##### ERGEBNIS
 Wurde der Knopf gedrückt, erscheint der Text im Serial Monitor. Wird er gedrückt gehalten, wird der Text alle 4 Sekunden ausgegeben.
 &nbsp;
 
 ![Steckbrett und Laptop. Ausgabe des Serial Monitors besagt "Knopf wird gedrückt"](https://github.com/KogutAl/ENDABGABE/blob/main/pic_serialprint.jpg)
 
 &nbsp;
 
 
  ---
 
  #### **TESTLAUF Nr. 6 - Verbindung aller Komponenten - Erster PROTOYP**

 &nbsp;
 

**Code**


```
/*
#include <Arduino.h>

int button = 6;

const int blinkLedPin = 2;                  
const int buttonBlinkPin = 3;

int LedPin = 9;
int buttonLedPin = 10;


void setup() {
  pinMode (button ,INPUT_PULLUP);                                               // Pin 6 ist Button Input
  Serial.begin(9600);                                                           // BAUD Rate; Informationsweitergabe Rate
  Serial.println("        Der Detektiv muss den Raum betreten.");
  delay (3000); 
  Serial.println("        Begebe dich zum Eingang des Zimmers um das Spiel zu starten.");

  // --------------- EVENT 1: Licht flackert ------------------
  pinMode(blinkLedPin, OUTPUT);                                                // Pin 2 ist Output -> LED blinkt
  pinMode(buttonBlinkPin, INPUT_PULLUP);                                       // PIN 3 ist Input -> durch Knopfdruck blinkt LED

  // --------------- EVENT 2: Lampe einschalten ------------------
  pinMode(LedPin, OUTPUT);                                                     // Pin 9 ist OUTPUT, LED leuchtet
  pinMode(buttonLedPin, INPUT_PULLUP);                                         // Pin 10 ist INPUT, Button

  digitalWrite (LedPin, LOW);                                                  // Ausgangszustand LED

}

void loop() {
  if (digitalRead(button) == LOW){                                             // wenn Knopf gedrückt wird
    Serial.println("      > In dieser Dunkelheit kann ich nicht arbeiten.");   // wird Text in Serial Monitor ausgegeben
    delay (3000);   
    Serial.println("      > Ich brauche Licht.");  
  };

  // --------------- EVENT 1: Licht flackert ------------------
  
  if (digitalRead (buttonBlinkPin) == LOW ){                                   // wenn Knopf gedrückt ist...
        digitalWrite(blinkLedPin, HIGH);                                       // geht LED an...
        delay(3000);                                                           // für 3000ms...
        digitalWrite(blinkLedPin, LOW);                                        // danach geht aus..
        delay (500);                                                           // für 500ms...
        digitalWrite(blinkLedPin, HIGH);                                       // geht wieder an usw.
        delay(2000);
        digitalWrite(blinkLedPin, LOW);
        delay (100);
        digitalWrite(blinkLedPin, HIGH);
        delay(200);
        digitalWrite(blinkLedPin, LOW);
        delay (50);
  };
  if (digitalRead (buttonBlinkPin) == HIGH ){                                   // wenn Knopf nicht gedrückt ist
        digitalWrite(blinkLedPin, LOW);                                         // bleibt LED aus
  };


  // --------------- EVENT 2: Lampe einschalten ------------------

   if (digitalRead(buttonLedPin) == LOW){                                       // wenn Button gedrückt wird...
    digitalWrite(LedPin, !digitalRead(LedPin));                                 // starte Output (LED leuchtet) und lese Zustand der LED (an oder aus)
  };

}
```
 &nbsp;
 
 ##### ERGEBNIS
  Der Text wird wie gewünscht mit den Drücken der Knöpfe oder der Abfolge von Befehlen (Lichtflacker-Event) wiedergegeben. 

 
 ![Steckbrett mit 3 Buttons und 2 LEDs"](https://github.com/KogutAl/ENDABGABE/blob/main/pic_1_Prototyp.jpg)
 
 
 &nbsp;

  ---
 
  #### **FINALE ABGABE DES PROTOTYPS**

 &nbsp;
 

**Code**


```
/*
#include <Arduino.h>

int button = 6;

const int blinkLedPin = 2;                  
const int buttonBlinkPin = 3;

int LedPin = 9;
int buttonLedPin = 10;


void setup() {
  pinMode (button ,INPUT_PULLUP);                                               // Pin 6 ist Button Input
  Serial.begin(9600);                                                           // BAUD Rate; Informationsweitergabe Rate
  Serial.println("        Der Detektiv muss den Raum betreten.");
  delay (2500); 
  Serial.println("        Begebe dich zum Eingang des Zimmers um das Spiel zu starten.");

  // --------------- EVENT 1: Licht flackert ------------------
  pinMode(blinkLedPin, OUTPUT);                                                // Pin 2 ist Output -> LED blinkt
  pinMode(buttonBlinkPin, INPUT_PULLUP);                                       // PIN 3 ist Input -> durch Knopfdruck blinkt LED

  // --------------- EVENT 2: Lampe einschalten ------------------
  pinMode(LedPin, OUTPUT);                                                     // Pin 9 ist OUTPUT, LED leuchtet
  pinMode(buttonLedPin, INPUT_PULLUP);                                         // Pin 10 ist INPUT, Button

  digitalWrite (LedPin, LOW);                                                  // Ausgangszustand LED

}

void loop() {
  if (digitalRead(button) == LOW){                                             // wenn Knopf gedrückt wird
    Serial.println("      > In dieser Dunkelheit kann ich nicht arbeiten.");   // wird Text in Serial Monitor ausgegeben
    delay (3000);   
    Serial.println("      > Ich brauche Licht.");  
  };

  // --------------- EVENT 1: Licht flackert ------------------
  
  if (digitalRead (buttonBlinkPin) == LOW ){                                   // wenn Knopf gedrückt ist...
        digitalWrite(blinkLedPin, HIGH);                                       // geht LED an...
        delay(3000);                                                           // für 3000ms...
        digitalWrite(blinkLedPin, LOW);                                        // danach geht aus..
        delay (500);                                                           // für 500ms...
        digitalWrite(blinkLedPin, HIGH);                                       // geht wieder an usw.
        delay(2000);
        digitalWrite(blinkLedPin, LOW);
        delay (100);
        digitalWrite(blinkLedPin, HIGH);
        delay(200);
        digitalWrite(blinkLedPin, LOW);
        delay (150);

        Serial.println("      > Fantastisch. ");  
        delay (2500);
        Serial.println("      > Diese Lampe taugt schon mal nichts.");  
        delay (2500); 
        Serial.println("      > ..."); 
        delay (3000); 
        Serial.println("      > Hier gibt es bestimmt eine weitere Lichquelle. "); 

  };
  if (digitalRead (buttonBlinkPin) == HIGH ){                                   // wenn Knopf nicht gedrückt ist
        digitalWrite(blinkLedPin, LOW);                                         // bleibt LED aus
  };


  // --------------- EVENT 2: Lampe einschalten ------------------

   if (digitalRead(buttonLedPin) == LOW){                                       // wenn Button gedrückt wird...
    Serial.println("      > Na bitte. ");  
    delay (2000);
    Serial.println("      > Diese funktioniert. ");  
    delay (2500);
    Serial.println("      > Dann mal ran an die Arbeit");  
    delay (2500);
    digitalWrite(LedPin, !digitalRead(LedPin));                                 // starte Output (LED leuchtet) und lese Zustand der LED (an oder aus)
  };

}
```
 &nbsp;
 
 ##### ERGEBNIS
  Nun, da ich weiß, dass meine ersten drei Events seperat funktionieren, war mein nächster Schritt, alle Komponenten auf einem Steckbrett zu vereinen. Somit soll das Spielbrett/der Spielraum simuliert werden und festgestellt werden, ob noch alles so funktioniert wie es soll.
 Beim erstenne der seperaten Codes habe ich darauf geachtet, keine Pins doppelt zu belegen, sodass diese sich beim Zusammenfügen der Codes nicht gegenseitig im Wege stehen. An dieser Stelle läuft alles noch gut, aber stehen im Code noch keinem Bezug zueinander.
 
 ![Steckbrett und Laptop. Ausgabe des Serial Monitors besagt "Knopf wird gedrückt"](https://github.com/KogutAl/ENDABGABE/blob/main/pic_Final.jpg)
 
 &nbsp;
 
 ---
### **6) Reflektion**
---

&nbsp;
 
 ##### Was ist gut gelaufen?
 
 Nachdem ich festgelegt habe, welche Effekte und Interaktionen innerhalb des Detektivspiels vorhanden sein sollten, konnte ich mich zur Recherche begeben und versuchen diese nachzustellen. Hierbei habe ich jeden Effekt einzeln betrachtet und die Komponenten erst einmal separiert von den anderen auf dem Steckbrett zusammengeschlossen. So liefen der Testlauf der Einschaltung einer LEDs anhand eines Knopfdruckes oder die Ausgabe eines Textes auf der Steuerkonsole, unabhängig voneinander.
 Damit konnte ich feststellen, ob diese einzelnen Events so funktionieren wie ich es mir vorgestellt habe, bevor ich alle gemeinsam in die Prototyp-Schaltung stecke und Schwierigkeiten habe, potenzielle Fehlerquellen auszumachen. 
 Mit dieser Vorgehensweise war ich sehr zufrieden, da ich diese Testläufe zwar immer wieder aufs neue ein- und nochmal ausstecken musste, um mit dem nächsten Test weiterzumachen, jedoch bei dem Endprodukt deutlich weniger Probleme hatte und ich für jede Komponente und Eventschaltkreis genau wusste, was ich dort mache.
 Bei weiteren Physical Computing Projekten, würde ich diese Vorgehensweise zukünftig bevorzugen.
 
 &nbsp;
 
 ##### Was besitzt Verbesserungspotenzial?
 
 Das Zusammenstecken und die Generierung des Codes haben eine Menge Spaß gemacht, doch da ich blutige Anfängerin bin, waren dies alle die Produkte sehr zeitaufwendigen Recherchen. Bei den Recherchen habe ich für mich persönlich eine große Problemquelle ausmachen können, da ich mich in diesen regelrecht verloren habe. Was beispielsweise mit der Idee einer simplen einzelnen Tonausgabe begann, ist innerhalb meiner Recherche zu der durchaus komplexeren Ausgabe eines StarWars Themes geworden, das auch noch interaktiv sein sollte. Dies überstieg meinen Wissenstand und bisherigen Erfahrungen deutlich und doch, wollte ich es möglich machen, was mit der weiteren Suche und dem (nicht erfolgreichen) Schreiben des Codes resultierte, nur um dieses Konzept nach stundenlangem Probieren, letztendlich doch zu verwerfen.
 Dies geschah leider in regelrechten Abständen, bei denen ich mir super coole Effekte ausgesucht habe, die ich leider noch nicht umsetzen konnte und Zeit daran verschwendet habe.
 Das Prozedere war natürlich äußerst frustrierend und zukünftig muss ich lernen meine Ziele niedrigschweilliger festzulegen und erst mit dem Erreichen dieser, die Möglichkeit von iterativen Verbesserungen in Betracht zu ziehen.
 Aufgrund dieses immensen Recherchen- und (Scrap)Code-Schreibung, musste ich letztendlich ebenso, die visuelle Anpassung des Prototypen, wie beispielsweise die Detektivspielfigur, das Spielbrett und Objekte verwerfen.
 
 
  &nbsp;
 
 ##### Was wird aus dem Projekt?
 
 Nach wie vor bin ich überzeugt davon, dass das interaktive Detektivspiel ein spaßiges Konzept innerhalb von Mensch-Computer-Interaktionen, sein kann. Mein Wissensstand ist noch lange nicht auf dem Niveau der Umseztung, wie ich es mir visioniert habe. Dennoch möchte ich die Idee nicht verwerfen und mein Glück im nächsten Semester, mit der weiteren Ausarbeitung dieses Projektes versuchen. Dies wird warhscheinlich immernoch nicht zu meinem Traumresultat führen, doch besser kann es sicherlich werden.
 

 &nbsp;
 
 ---
### **Quellenangaben**
---
 
 
[Arduino Code Referenzen und Erklärungen](https://arduinogetstarted.com/de/reference/digitalread)
 <br>
[Kapazitiver Sensor](https://www.youtube.com/watch?v=jco-uU5ZgEU)
 <br>
[Kupfer Switch](https://www.arduinoplatform.com/subscription-projects/create-a-touch-button-with-copper-aluminum-foil/)
 <br>
[Kontakt Switch](https://www.kobakant.at/DIY/?p=8906)
 <br>
[Recherche_4](https://mehackit.org/en/courses/electronics_and_programming_basics/02-switch-stuff-on-and-off/03-exercise-1/)
 <br>
[Pressure_Switch](https://www.instructables.com/Use-a-DIY-Pressure-Plate-Switch-to-Automate-Your-H/)
 <br>
[MP3 in Code umwandeln](https://www.youtube.com/watch?v=aaqaAXlZbuc)
 <br>
[Star Wars Theme](https://www.youtube.com/watch?v=RVyLqXz-xvU)
 <br>
[Star Wars Theme-Tutorial](https://42bots.com/?s=melody)
 <br>
[State Machine](https://www.mikrocontroller.net/articles/Statemachine)
 <br>
[State Machine - Ampelbeispiel](https://www.youtube.com/watch?v=AFUAkNXTqfo)
 <br>
[Textausgabe](https://docs.arduino.cc/built-in-examples/usb/KeyboardMessage)
 <br>
[SerialPrintln_Video](https://www.youtube.com/watch?v=RUnUaE_hoHs)
 <br>
[SerialPrint](https://www.arduino.cc/reference/de/language/functions/communication/serial/println/)
<br>
[Schaltplan Symbole](https://www.build-electronic-circuits.com/schematic-symbols/)

 &nbsp;
