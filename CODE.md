# Littlegame
 #include <LedControl.h>

int DIN = 12;
int CS =  11;
int CLK = 10;
const int buttonPin1 = 7;
const int buttonPin2 = 6;
const int buttonPin3 = 5;
const int buttonPin4 = 4;
const int buttonPin5 = 3;
const int buttonPin6 = 2;
int hola;

byte smile[8] =   {0x3C, 0x42, 0xA5, 0x81, 0xA5, 0x99, 0x42, 0x3C};
byte neutral[8] = {0x3C, 0x42, 0xA5, 0x81, 0xBD, 0x81, 0x42, 0x3c};
byte frown[8] =   {0x3C, 0x42, 0xA5, 0x81, 0x99, 0xA5, 0x42, 0x3c};

int buttonState = 0;

LedControl lc = LedControl(DIN, CLK, CS, 0);

void setup() {
  lc.shutdown(0, false);      //The MAX72XX is in power-saving mode on startup
  lc.setIntensity(0, 15);     // Set the brightness to maximum value
  lc.clearDisplay(0);         // and clear the display
  pinMode(buttonPin1, INPUT);
  pinMode(buttonPin2, INPUT);
  pinMode(buttonPin3, INPUT);
  pinMode(buttonPin4, INPUT);
  pinMode(buttonPin5, INPUT);
  pinMode(buttonPin6, INPUT);
  Serial.begin(9600);
  Serial.println("hola");
}

void loop() {

  printByte(neutral);

  if (digitalRead(buttonPin4) == HIGH) {

    Serial.println("15+9=?");
    Serial.println("a) 24");
    Serial.println("b) 22");
    Serial.println("c) 25");


    while (digitalRead(buttonPin1) == LOW && digitalRead(buttonPin2) == LOW && digitalRead(buttonPin3) == LOW) {}

    if (digitalRead(buttonPin1) == HIGH) {
      printByte(smile);
      Serial.println("Correct!");
      delay(1000);
    } else if (digitalRead(buttonPin2) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    } else if (digitalRead(buttonPin3) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    }
  } else if (digitalRead(buttonPin5) == HIGH) {

    Serial.println("38-16=?");
    Serial.println("a) 25");
    Serial.println("b) 26");
    Serial.println("c) 22");


    while (digitalRead(buttonPin1) == LOW && digitalRead(buttonPin2) == LOW && digitalRead(buttonPin3) == LOW) {}

    if (digitalRead(buttonPin1) == HIGH) {
      printByte(smile);
      Serial.println("Correct!");

      delay(1000);
    } else if (digitalRead(buttonPin2) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    } else if (digitalRead(buttonPin3) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    }

  } else if (digitalRead(buttonPin6) == HIGH) {

    Serial.println("4x6=?");
    Serial.println("a) 30");
    Serial.println("b) 21");
    Serial.println("c) 24");

    while (digitalRead(buttonPin1) == LOW && digitalRead(buttonPin2) == LOW && digitalRead(buttonPin3) == LOW) {
    }

    if (digitalRead(buttonPin1) == HIGH) {
      printByte(smile);
      Serial.println("Correct!");

      delay(1000);
    }
    if (digitalRead(buttonPin2) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    }
    if (digitalRead(buttonPin3) == HIGH) {
      printByte(frown);
      Serial.println("Wrong!");
      delay(1000);
    }
  }
}

void printByte(byte character []) {
  int i = 0;
  for (i = 0; i < 8; i++) {
    lc.setRow(0, i, character[i]);
  }
}

