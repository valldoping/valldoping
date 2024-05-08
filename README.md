// #include <ESP8266WiFi.h>
// #include <ESP8266HTTPClient.h>
// #include <WiFiClientSecure.h>
// #include <CTBot.h>
// #include <SoftwareSerial.h>

// const char* ssid = "Vall";
// const char* password = "88888888";
// const String botToken = "5891521236:AAH7aKygOYA0FYv8H7SVLMq-MWl7RKrC0rY";
// const String chatId = "1302214303";

// const String HOST = "gpdi-apostolos.website";

// // Az
// // const String chatId = "1619670221";

// const String chatMessage = "HelloThere";

// unsigned long previousMillis = 0;
// boolean LEDState = false;

// String encode_msg(String dataMessage) {
//   String encodedMessage = "";
//   for (size_t i = 0; i < dataMessage.length(); i++) {
//     if (dataMessage[i] == ' ') {
//       encodedMessage += "%20";
//     } else {
//       encodedMessage += dataMessage[i];
//     }
//   }
//   return encodedMessage;
// }

// void blinkLED(unsigned long currentMillis) {
//   if (LEDState) {
//     if (currentMillis - previousMillis >= 25) {
//       LEDState = false;
//       previousMillis = currentMillis;
//     }
//   } else {
//     if (currentMillis - previousMillis >= 50) {
//       LEDState = true;
//       previousMillis = currentMillis;
//     }
//   }
//   digitalWrite(LED_BUILTIN, LEDState);
// }

// void send_payload(String payload) {
//   if (WiFi.status() == WL_CONNECTED) {
//       WiFiClientSecure client;
//       client.setInsecure(); // Allow self-signed certificates
//       int loop_count = 0;

//       while (true) {
//         loop_count += 1;
//         Serial.print("attempt : ");
//         Serial.println(loop_count);

//         digitalWrite(LED_BUILTIN, LOW);
//         // blinkLED(currentMillis);

//         if (client.connect("api.telegram.org", 443)) {
//           client.print(payload);

//           if (client.connected() || client.available()) {
//             Serial.println("Message sended");
//             digitalWrite(LED_BUILTIN, HIGH);
//           }

//           break;
//         }
//         else {
//           Serial.println("Retrying to connect the server ...");
//           digitalWrite(LED_BUILTIN, HIGH);
//         }

//         client.stop();
//         digitalWrite(LED_BUILTIN, HIGH);
//       }
//     }
// }


// void host_report() {
//   if (WiFi.status() == WL_CONNECTED) {
//     WiFiClientSecure client;
//     client.setInsecure(); // Allow self-signed certificates
//     int loop_count = 0;

//     while (true) {
//       loop_count += 1;
//       Serial.print("attempt : ");
//       Serial.println(loop_count);

//       digitalWrite(LED_BUILTIN, LOW);
//       // blinkLED(currentMillis);

//       if (client.connect(HOST, 443)) {
//         Serial.println("Connected to server");

//         // Define the HTTP POST request
//         String url = "/api/send";
//         String contentType = "application/json";
//         String payload = "{\"messages\":\"WASPADA SIAGA 1!!! TANAH LONGSOR\",\"type\":\"bahaya\"}";

//         // Send the POST request
//         client.print(String("POST ") + url + " HTTP/1.1\r\n");
//         client.print(String("Host: ") + HOST + "\r\n");
//         client.print("Connection: close\r\n");
//         client.print("Content-Type: " + contentType + "\r\n");
//         client.print(payload);

//         if (client.connected() || client.available()) {
//           Serial.println("Message sended");
//           digitalWrite(LED_BUILTIN, HIGH);
//         }

//         break;
//       }
//       else {
//         Serial.println("Retrying to connect the server ...");
//         digitalWrite(LED_BUILTIN, HIGH);
//       }

//       client.stop();
//       digitalWrite(LED_BUILTIN, HIGH);
//     }
//   }
// }


// void setup() {
//   pinMode(LED_BUILTIN, OUTPUT);
//   digitalWrite(LED_BUILTIN, HIGH);

//   Serial.begin(9600);
  
//   WiFi.begin(ssid, password);
//   while (WiFi.status() != WL_CONNECTED) {
//     delay(1000);
//     Serial.println("Connecting to WiFi...");
//   }

//   Serial.println("Connected to WiFi");
//   Serial.println("IP : " + WiFi.localIP().toString());
// }


// void loop() {
//   unsigned long currentMillis = millis();
//   String payload;

//   if (Serial.available()) {
//     // digitalWrite(LED_BUILTIN, LOW);
//     String receivedData = Serial.readStringUntil('\n');
//     receivedData.trim();
    
//     if (receivedData == "code-1") {
//       payload = "GET /bot" + botToken + "/sendMessage?chat_id=" + chatId + "&text=" + "PERINGATAN%20BAHAYA!!!%20TANAH%20LONGSOR" + " HTTP/1.1\r\n" +
//                       "Host: api.telegram.org\r\n" +
//                       "Connection: close\r\n\r\n";
//       send_payload(payload);
//       // host_report();

//     }
//     if (receivedData == "code-2") {
//       payload = "GET /bot" + botToken + "/sendMessage?chat_id=" + chatId + "&text=" + "WASPADA%20SIAGA%202%20!!!%20KEMUNGKINAN%20TANAH%20LONGSOR" + " HTTP/1.1\r\n" +
//                       "Host: api.telegram.org\r\n" +
//                       "Connection: close\r\n\r\n";
//       send_payload(payload);
//       // host_report();
//     }
//     if (receivedData == "code-3") {
//       payload = "GET /bot" + botToken + "/sendMessage?chat_id=" + chatId + "&text=" + "Kelembapan%20tanah%20lebih%20dari%2070%20persen.%20Waspada%20potensi%20tanah%20longsor" + " HTTP/1.1\r\n" +
//                       "Host: api.telegram.org\r\n" +
//                       "Connection: close\r\n\r\n";
//       send_payload(payload);
//       // host_report();
//     }

//   }

//   delay(250);
// }














#include <Arduino.h>
#include <Wire.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_sensor.h>
#include <LiquidCrystal_I2C.h>
#include <SoftwareSerial.h>


// SDA A4
// SCL A5
#define TX_PIN 1
#define RX_PIN 0
#define TRIGGER_PIN 2             // Ultrasonic trigger
#define ECHO_PIN 3                // Ultrasonic echo
#define BUZZER_PIN 4
#define RED_LED_PIN 7
#define ORANGE_LED_PIN 8
#define GREEN_LED_PIN 12
#define MOISTURE_ANAlOG_PIN A0
#define SDA_PIN 12
#define SCL_PIN 13

SoftwareSerial wifi(RX_PIN, TX_PIN);
Adafruit_MPU6050 mpu;


// Define Motions
const double MOTION_SENS = 1.8;
unsigned long MOTION_STATE_RESET = 5000;

unsigned long previousMotionsMillis = 0;
double prev_ax = 0;
double prev_ay = 0;
double prev_az = 0;
bool false_alarm_state = false;

bool handleMotions(unsigned long currentMotionsMillis, bool alarm_state) {
  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

  // Cari ini
  double calculated_ax_prev = abs(a.acceleration.x - prev_ax);
  double calculated_ay_prev = abs(a.acceleration.y - prev_ay);
  double calculated_az_prev = abs(a.acceleration.z - prev_az);

  // Tambah ini p dpe bawah
  Serial.print("x: "); Serial.println(a.acceleration.x);
  Serial.print("y: "); Serial.println(a.acceleration.y);
  Serial.print("z: "); Serial.println(a.acceleration.z);


  if (
      calculated_ax_prev >= MOTION_SENS ||
      calculated_ay_prev >= MOTION_SENS ||
      calculated_az_prev >= MOTION_SENS
  ) {
    alarm_state = true;
    previousMotionsMillis = currentMotionsMillis;
  }
  
  prev_ax = a.acceleration.x;
  prev_ay = a.acceleration.y;
  prev_az = a.acceleration.z;
  
  if (currentMotionsMillis - previousMotionsMillis >= MOTION_STATE_RESET) {
    alarm_state = false;

    previousMotionsMillis = currentMotionsMillis;
  }

  return alarm_state;
}


// LED
unsigned long previousMillis = 0;
boolean ledState = false;
LiquidCrystal_I2C lcd(0x27,16,2);

void handleLEDandBuzzer(long distance, unsigned long currentMillis) {
  if (distance < 8) {
    digitalWrite(ORANGE_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, LOW);
    
    if (false_alarm_state) {
      Serial.println("code-1");
    }

    if (ledState) {
      if (currentMillis - previousMillis >= 50) {
        ledState = false;
        previousMillis = currentMillis;
        
      }
    } else {
      if (currentMillis - previousMillis >= 100) {
        ledState = true;
        previousMillis = currentMillis;
      }
    }
    if (false_alarm_state) {
      digitalWrite(BUZZER_PIN, ledState);
    }
    digitalWrite(RED_LED_PIN, ledState);
  }
  else if (distance < 15) {
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(GREEN_LED_PIN, LOW);
    
    if (false_alarm_state) {
      Serial.println("code-2");
    }

    if (ledState) {
      if (currentMillis - previousMillis >= 250) {
        ledState = false;
        previousMillis = currentMillis;
      }
    } else {
      if (currentMillis - previousMillis >= 500) {
        ledState = true;
        previousMillis = currentMillis;
      }
    }
    if (false_alarm_state) {
      digitalWrite(BUZZER_PIN, ledState);
    }
    digitalWrite(ORANGE_LED_PIN, ledState);
  }
  else {
    digitalWrite(RED_LED_PIN, LOW);
    digitalWrite(ORANGE_LED_PIN, LOW);
    digitalWrite(BUZZER_PIN, LOW);

    if (ledState) {
      if (currentMillis - previousMillis >= 100) {
        ledState = false;
        previousMillis = currentMillis;
      }
    } else {
      if (currentMillis - previousMillis >= 2500) {
        ledState = true;
        previousMillis = currentMillis;
      }
    }
    digitalWrite(GREEN_LED_PIN, ledState);
  }  
}


void setup() {
  Serial.begin(9600);
  wifi.begin(9600);
  mpu.begin();

  // Output
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);      // initialize buzzer pin to output
  pinMode(RED_LED_PIN, OUTPUT);
  pinMode(ORANGE_LED_PIN, OUTPUT);
  pinMode(GREEN_LED_PIN, OUTPUT);
  // Input
  pinMode(ECHO_PIN, INPUT);

  // LiquidCrystal LCD Init
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0,0);
  lcd.print("dist(cm)");
  lcd.setCursor(10,0);
  lcd.print(":");
  lcd.setCursor(0,1);
  lcd.print("moist(%)");
  lcd.setCursor(10,1);
  lcd.print(":");  
}

void loop() {
  long duration, distance;
  unsigned long currentMillis = millis();

  // Clear the trigger pin
  digitalWrite(TRIGGER_PIN, LOW);
  delay(100);
  
  // Set the trigger pin high for 10 microseconds
  digitalWrite(TRIGGER_PIN, HIGH);
  delay(100);
  digitalWrite(TRIGGER_PIN, LOW);
  
  // Measure the pulse duration on the echo pin
  duration = pulseIn(ECHO_PIN, HIGH);
  
  // Calculate the distance in centimeters
  distance = duration * 0.034 / 2;

  // Moisture Read
  int moisture = analogRead(MOISTURE_ANAlOG_PIN);
  int moisture_pr = 100.00 - ( (moisture / 1023.00) * 100.00 );

  if (moisture_pr > 70) {
    Serial.println("code-3");
  }

  lcd.setCursor(11,0);
  lcd.print("     ");
  lcd.setCursor(11,0);
  if (distance <= 25) {
    lcd.print(distance);
  } else {
    lcd.print("aman");
  }
  lcd.setCursor(11,1);
  lcd.print("     ");
  lcd.setCursor(11,1);
  lcd.print(moisture_pr);

  handleLEDandBuzzer(distance, currentMillis);
  false_alarm_state = handleMotions(currentMillis, false_alarm_state);


  if (Serial.available()) { // Check if data is available to read
    String receivedData = Serial.readStringUntil('\n'); // Read the data until newline character
    receivedData.trim(); // Remove leading and trailing whitespaces
    
    Serial.print("ESP8266: ");
    Serial.println(receivedData); // Print the received data from ESP8266
    // delay(1000);

  }

  delay(100); // Wait taking the next reading
}

















// void setup() {
//   // put your setup code here, to run once:

// }

// void loop() {
//   // put your main code here, to run repeatedly:

// }
