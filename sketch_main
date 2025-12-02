// Deokjeong High School Smart-Farm Source Code v1.0 (2025-04-21)

#include <BluetoothSerial.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

String device_name = "BT-A005";
BluetoothSerial SerialBT;

#define wifiLed   2   //D2
#define RELAY1   27   //D33
#define RELAY2   26   //D25
#define RELAY3   25   //D26
#define RELAY4   33   //D27

LiquidCrystal_I2C lcd(0x27,16,2);
DHT dht(17, DHT11); // temp Humidity Pin17

int a;
byte x = 0x00;

void setup() {
  SerialBT.begin(device_name);
  Serial.begin(115200);
  Wire.begin();
  
  lcd.init();
  lcd.backlight();
  lcd.clear();
  lcd.setCursor(0,0);lcd.print("Connecting...");
  delay(1000);

  lcd.clear(); lcd.print("Connected!");
  SOUND_0();  delay(2000); /* 블루투스가 연결되었습니다.*/
  pinMode(wifiLed,OUTPUT); 
  digitalWrite(wifiLed,HIGH);

  lcd.clear(); lcd.print("START!!!");
  SOUND_3();  /* 식물재배기의작동을 시작합니다.*/
 
}

void loop() {

  if (SerialBT.available() > 0) {
    a = SerialBT.read();

    switch (a) {
        case 'A':
        // 블루투스 실행시 팬 기능 자동작동
        getTempHumi();
        digitalWrite(RELAY1,LOW);
//      digitalWrite(RELAY2,LOW);
        fan();
        digitalWrite(RELAY3,LOW);
        Serial.println(a);
        SOUND_3();
        break;

      case 'B':
        lcd.clear();
        lcd.print("Sleeping...");
        digitalWrite(RELAY1,HIGH);
        digitalWrite(RELAY2,HIGH);
        digitalWrite(RELAY3,HIGH);
        Serial.println(a);
        SOUND_4();
        break;

      case 'C':
        lcd.clear();
        lcd.print("LED ON");
        digitalWrite(RELAY1,LOW);
        Serial.println(a);
        SOUND_5();
        break;

      case 'D':
        lcd.clear();
        lcd.print("LED OFF");
        digitalWrite(RELAY1,HIGH);
        Serial.println(a);
        SOUND_6();
        break;

      case 'E':
        lcd.clear();
        lcd.print("FAN ON"); delay(5000); // 5초동안 강제 작동
        digitalWrite(RELAY2,LOW);
        Serial.println(a);
        SOUND_9();
        break;

      case 'F':
        lcd.clear();
        lcd.print("FAN OFF");
        digitalWrite(RELAY2,HIGH);
        Serial.println(a);
        SOUND_10();
        break;

      case 'G':
        lcd.clear();
        lcd.print("OXYGEN ON");
        digitalWrite(RELAY3,LOW);
        Serial.println(a);
        SOUND_7();
        break;

      case 'H':
        lcd.clear();
        lcd.print("OXYGEN OFF");
        digitalWrite(RELAY3,HIGH);
        Serial.println(a);
        SOUND_8();
        break;
    }
  }
  else {
    // 기본적으로 모두 작동 
    getTempHumi();
    pinMode(RELAY1,OUTPUT); digitalWrite(RELAY1,LOW);
    pinMode(RELAY2,OUTPUT); digitalWrite(RELAY2,LOW);
    pinMode(RELAY3,OUTPUT); digitalWrite(RELAY3,LOW);
    pinMode(RELAY4,OUTPUT); digitalWrite(RELAY4,LOW);
  }
  delay(500);
}

/* 블루투스가 연결되었습니다.*/
void SOUND_0(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x00);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 와이파이를 연결하고 있습니다 */
void SOUND_1(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes 소리조절
  Wire.write(0x01);              // sends one byte 음성순서
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 와이파이가 연결되었습니다. */
void SOUND_2(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x02);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(5000);
}
/* 식물재배기의 모든 작동을 시작합니다 */
void SOUND_3(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x03);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 식물재배기의 모든 작동을 중지합니다 */
void SOUND_4(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x04);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* LED가 켜졌습니다 */
void SOUND_5(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x05);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* LED가 꺼졌습니다 */
void SOUND_6(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x06);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 산소발생을 시작합니다 */
void SOUND_7(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x07);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 산소발생이 중지 되었습니다. */
void SOUND_8(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x08);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 팬이 작동 되었습니다 */
void SOUND_9(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x09);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 팬작동이 중지 되었습니다. */
void SOUND_10(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0a);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 순환펌프가 작동됩니다. */
void SOUND_11(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0b);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 순환펌프 작동이 중지되었습니다. */
void SOUND_12(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0c);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(4000);
}
/* 온습도센서가 작동하지 않습니다. */
void SOUND_13(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0d);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(4000);
}
void getTempHumi(){
 float temp = dht.readTemperature();
 float humidity = dht.readHumidity();
 if (isnan(temp) || isnan(humidity)) {
      lcd.clear();
      lcd.setCursor(0,0); lcd.print("DHT Error!!!");
      SOUND_13();
 } 
 else 
 { Serial.print(" Temp: "); Serial.print(temp); Serial.print("c");
   lcd.setCursor(0,0); lcd.print("Temp:  ");  lcd.setCursor(6,0);  lcd.print(temp); lcd.print(char(223)); lcd.print("C");
   Serial.print(" Humi: ");  Serial.print(humidity);  Serial.print("%");
   lcd.setCursor(0,1); lcd.print("Humi: "); lcd.setCursor(6,1);  lcd.print(humidity); lcd.print("%");
 }
}
void fan() {
  float temp = dht.readTemperature();
    if (temp > 22) digitalWrite(RELAY2,LOW); 
     else
     digitalWrite(RELAY2,HIGH); 
}

#include <BluetoothSerial.h>
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

String device_name = "BT-A005";
BluetoothSerial SerialBT;

#define wifiLed   2   //D2
#define RELAY1   27   //D33
#define RELAY2   26   //D25
#define RELAY3   25   //D26
#define RELAY4   33   //D27

LiquidCrystal_I2C lcd(0x27,16,2);
DHT dht(17, DHT11); // temp Humidity Pin17

int a;
byte x = 0x00;

void setup() {
  SerialBT.begin(device_name);
  Serial.begin(115200);
  Wire.begin();
  
  lcd.init();
  lcd.backlight();
  lcd.clear();
  lcd.setCursor(0,0);lcd.print("Connecting...");
  delay(1000);

  lcd.clear(); lcd.print("Connected!");
  SOUND_0();  delay(2000); /* 블루투스가 연결되었습니다.*/
  pinMode(wifiLed,OUTPUT); 
  digitalWrite(wifiLed,HIGH);

  lcd.clear(); lcd.print("START!!!");
  SOUND_3();  /* 식물재배기의작동을 시작합니다.*/
 
}

void loop() {

  if (SerialBT.available() > 0) {
    a = SerialBT.read();

    switch (a) {
        case 'A':
        // 블루투스 실행시 팬 기능 자동작동
        getTempHumi();
        digitalWrite(RELAY1,LOW);
//      digitalWrite(RELAY2,LOW);
        fan();
        digitalWrite(RELAY3,LOW);
        Serial.println(a);
        SOUND_3();
        break;

      case 'B':
        lcd.clear();
        lcd.print("Sleeping...");
        digitalWrite(RELAY1,HIGH);
        digitalWrite(RELAY2,HIGH);
        digitalWrite(RELAY3,HIGH);
        Serial.println(a);
        SOUND_4();
        break;

      case 'C':
        lcd.clear();
        lcd.print("LED ON");
        digitalWrite(RELAY1,LOW);
        Serial.println(a);
        SOUND_5();
        break;

      case 'D':
        lcd.clear();
        lcd.print("LED OFF");
        digitalWrite(RELAY1,HIGH);
        Serial.println(a);
        SOUND_6();
        break;

      case 'E':
        lcd.clear();
        lcd.print("FAN ON"); delay(5000); // 5초동안 강제 작동
        digitalWrite(RELAY2,LOW);
        Serial.println(a);
        SOUND_9();
        break;

      case 'F':
        lcd.clear();
        lcd.print("FAN OFF");
        digitalWrite(RELAY2,HIGH);
        Serial.println(a);
        SOUND_10();
        break;

      case 'G':
        lcd.clear();
        lcd.print("OXYGEN ON");
        digitalWrite(RELAY3,LOW);
        Serial.println(a);
        SOUND_7();
        break;

      case 'H':
        lcd.clear();
        lcd.print("OXYGEN OFF");
        digitalWrite(RELAY3,HIGH);
        Serial.println(a);
        SOUND_8();
        break;
    }
  }
  else {
    // 기본적으로 모두 작동 
    getTempHumi();
    pinMode(RELAY1,OUTPUT); digitalWrite(RELAY1,LOW);
    pinMode(RELAY2,OUTPUT); digitalWrite(RELAY2,LOW);
    pinMode(RELAY3,OUTPUT); digitalWrite(RELAY3,LOW);
    pinMode(RELAY4,OUTPUT); digitalWrite(RELAY4,LOW);
  }
  delay(500);
}

/* 블루투스가 연결되었습니다.*/
void SOUND_0(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x00);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 와이파이를 연결하고 있습니다 */
void SOUND_1(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes 소리조절
  Wire.write(0x01);              // sends one byte 음성순서
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 와이파이가 연결되었습니다. */
void SOUND_2(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x02);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(5000);
}
/* 식물재배기의 모든 작동을 시작합니다 */
void SOUND_3(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x03);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 식물재배기의 모든 작동을 중지합니다 */
void SOUND_4(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x04);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* LED가 켜졌습니다 */
void SOUND_5(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x05);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* LED가 꺼졌습니다 */
void SOUND_6(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x06);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 산소발생을 시작합니다 */
void SOUND_7(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x07);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 산소발생이 중지 되었습니다. */
void SOUND_8(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x08);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 팬이 작동 되었습니다 */
void SOUND_9(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x09);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(2000);
}
/* 팬작동이 중지 되었습니다. */
void SOUND_10(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0a);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 순환펌프가 작동됩니다. */
void SOUND_11(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0b);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(3000);
}
/* 순환펌프 작동이 중지되었습니다. */
void SOUND_12(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0c);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(4000);
}
/* 온습도센서가 작동하지 않습니다. */
void SOUND_13(){   
  Wire.beginTransmission(0xee); // transmit to device DC
  Wire.write(0xE0);        // sends five bytes
  Wire.write(0x0d);              // sends one byte
  Wire.endTransmission();  // stop transmitting
  delay(4000);
}
void getTempHumi(){
 float temp = dht.readTemperature();
 float humidity = dht.readHumidity();
 if (isnan(temp) || isnan(humidity)) {
      lcd.clear();
      lcd.setCursor(0,0); lcd.print("DHT Error!!!");
      SOUND_13();
 } 
 else 
 { Serial.print(" Temp: "); Serial.print(temp); Serial.print("c");
   lcd.setCursor(0,0); lcd.print("Temp:  ");  lcd.setCursor(6,0);  lcd.print(temp); lcd.print(char(223)); lcd.print("C");
   Serial.print(" Humi: ");  Serial.print(humidity);  Serial.print("%");
   lcd.setCursor(0,1); lcd.print("Humi: "); lcd.setCursor(6,1);  lcd.print(humidity); lcd.print("%");
 }
}
void fan() {
  float temp = dht.readTemperature();
    if (temp > 22) digitalWrite(RELAY2,LOW); 
     else
     digitalWrite(RELAY2,HIGH); 
}

