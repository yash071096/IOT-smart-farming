# IOT-smart-farming
Smart farming project using IOT, implemented on Arduino IDE

//Code

#include<LiquidCrystal.h>
#include"pitches.h"
LiquidCrystal lcd(12,11,5,4,3,2);
int melody[]={NOTE_C4,NOTE_G3,NOTE_G3,NOTE_A3,NOTE_G3,0,NOTE_B3, NOTE_C4};
int noteDurations[]={4,8,8,4,4,4,4,4};
const int ledPin=7;
void setup() 
{
  // put your setup code here, to run once:
       Serial.begin(9600);
       lcd.begin(16,2);
       pinMode(ledPin,OUTPUT);

}

void loop() 
{
// put your main code here, to run repeatedly:
      int sensorValue=analogRead(A0);
      lcd.setCursor(0,0);
      Serial.println(sensorValue);
      delay(1);
      lcd.display();
      if(sensorValue>=1000)
     {
         digitalWrite(ledPin,LOW);
         lcd.print("moist low");
         delay(100);
         for(int thisNote=0;thisNote<8;thisNote++)
        {
             int noteDuration=1000/noteDurations[thisNote];
             tone(8,melody[thisNote],noteDuration);
             int pauseBetweenNotes=noteDuration*1.30;
          delay(pauseBetweenNotes);
          noTone(8);
      }
  }
  else
  {
     digitalWrite(ledPin,HIGH);
     lcd.print("moist high");
     delay(100);
     noTone(8);
   }
  delay(100);

}
