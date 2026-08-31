#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <SD.h>

// --- PIN DEFINITIONS ---
#define SD_CS 10
#define BUZZER 8
#define RESULT_BTN 9
#define LED_PIN 11 // LED lights up when vote is registered

const int buttonPins[6] = {2, 3, 4, 5, 6, 7};  // Voting buttons

// --- LCD SETUP (I2C address may vary: 0x27 or 0x3F) ---
LiquidCrystal_I2C lcd(0x27, 16, 2);

// --- PARTY DATA ---
String partyNames[6] = {"BJP", "INC", "AAP", "SP", "BSP", "Other"};
int votes[6] = {0, 0, 0, 0, 0, 0};

// --- SETUP ---
void setup() {
  Serial.begin(9600);
  lcd.init();
  lcd.backlight();

  pinMode(BUZZER, OUTPUT);
  pinMode(LED_PIN, OUTPUT);
  pinMode(RESULT_BTN, INPUT_PULLUP);

  for (int i = 0; i < 6; i++) {
    pinMode(buttonPins[i], INPUT_PULLUP);
  }

  lcd.clear();
  lcd.print("Init SD Card...");
  if (!SD.begin(SD_CS)) {
    lcd.setCursor(0, 1);
    lcd.print("SD init failed!");
    while (1) {
      tone(BUZZER, 1000, 200);
      delay(1000);
    }
  }

  lcd.clear();
  lcd.print("EVM Ready");
  lcd.setCursor(0, 1);
  lcd.print("Press to vote");

  writeHeaderToSD();
  delay(1000);
}

// --- MAIN LOOP ---
void loop() {
  // Check each voting button
  for (int i = 0; i < 6; i++) {
    if (digitalRead(buttonPins[i]) == LOW) {
      delay(50);
      if (digitalRead(buttonPins[i]) == LOW) {
        votes[i]++;
        voteFeedback();        // LED + beep
        showVoteOnLCD(i);
        saveVoteToSD(i);
        while (digitalRead(buttonPins[i]) == LOW); // wait until released
        lcd.clear();
        lcd.print("Ready to Vote");
        lcd.setCursor(0, 1);
        lcd.print("Press button...");
      }
    }
  }

  // Check result button
  if (digitalRead(RESULT_BTN) == LOW) {
    delay(80);
    if (digitalRead(RESULT_BTN) == LOW) {
      showResults();
      while (digitalRead(RESULT_BTN) == LOW); // wait release
      delay(300);
      lcd.clear();
      lcd.print("Ready to Vote");
      lcd.setCursor(0, 1);
      lcd.print("Press button...");
    }
  }
}

// --- FUNCTION: LED + buzzer feedback on vote ---
void voteFeedback() {
  digitalWrite(LED_PIN, HIGH);   // Turn ON LED
  tone(BUZZER, 2000);            // High-pitch beep
  delay(500);                    // Beep for 0.5 seconds
  noTone(BUZZER);
  delay(1500);                   // LED stays ON total 2 seconds
  digitalWrite(LED_PIN, LOW);    // Turn OFF LED
}

// --- FUNCTION: Display vote info ---
void showVoteOnLCD(int idx) {
  lcd.clear();
  lcd.print("Vote Recorded:");
  lcd.setCursor(0, 1);
  lcd.print(partyNames[idx]);
  delay(1000);
}

// --- FUNCTION: Save individual vote to SD ---
void saveVoteToSD(int i) {
  File file = SD.open("votes.txt", FILE_WRITE);
  if (file) {
    file.print(partyNames[i]);
    file.print(" = ");
    file.println(votes[i]);
    file.close();
  } else {
    lcd.clear();
    lcd.print("SD Write Error!");
  }
}

// --- FUNCTION: Write header at start ---
void writeHeaderToSD() {
  File file = SD.open("votes.txt", FILE_WRITE);
  if (file) {
    file.println("=== EVM Voting Session Started ===");
    for (int i = 0; i < 6; i++) {
      file.print("Party ");
      file.print(i + 1);
      file.print(": ");
      file.println(partyNames[i]);
    }
    file.println("------------------------------");
    file.close();
  }
}

// --- FUNCTION: Show results on LCD and SD ---
void showResults() {
  lcd.clear();
  lcd.print("Calculating...");
  delay(500);

  File file = SD.open("votes.txt", FILE_WRITE);
  if (file) {
    file.println("=== Session Results ===");
  }

  lcd.clear();
  for (int i = 0; i < 6; i++) {
    lcd.clear();
    lcd.print(partyNames[i]);
    lcd.setCursor(0, 1);
    lcd.print("Votes: ");
    lcd.print(votes[i]);
    delay(1500);

    if (file) {
      file.print(partyNames[i]);
      file.print(" = ");
      file.println(votes[i]);
    }
  }

  if (file) {
    file.println("-----------------------");
    file.close();
  }

  // High pitch beep to signal results saved
  tone(BUZZER, 2000);
  delay(500);
  noTone(BUZZER);

  lcd.clear();
  lcd.print("Results Saved!");
  delay(1200);
}
