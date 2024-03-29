#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include "CTBot.h"  //Pendeklarasian Library
CTBot myBot;
String ssid = "Babanggs";    //nama ssid wifi kalian
String pass = "Imam1998";  //password wifi kalian
String token = "5861350218:AAEG_1QfNkjEZSlMPLSw_RA1HisQKC0pQko";    //token bot baru kalian
const int id = 5424204248;  
int pH_Value; 
float PH=A0;
LiquidCrystal_I2C lcd(0x27,16,2);  

void setup() {
 Serial.begin(9600);
  Serial.println("Starting TelegramBot...");
  myBot.wifiConnect(ssid, pass);
  myBot.setTelegramToken(token);
  if (myBot.testConnection()) {
    Serial.println("Koneksi Bagus");
  } else {
    Serial.println("Koneksi Jelek");
  }
 lcd.init();
 lcd.backlight();
 pinMode(pH_Value, INPUT);
} 
 
void loop() 
{ 
  pH_Value = analogRead(PH); 
  PH = pH_Value * (5.0 / 1023.0); 
  Serial.println(PH); 
  myBot.sendMessage(id, "Peringatan: Ada Api di Rumah");
  lcd.backlight();
  lcd.setCursor(1,0);
  lcd.print("Project Dani");
  lcd.setCursor(4,1);
  lcd.print("PH=");
  lcd.setCursor(7,1);
  lcd.print(PH);
  delay(1000);
}
