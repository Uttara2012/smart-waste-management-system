# smart-waste-management-system

#include <SoftwareSerial.h>

SoftwareSerial mySerial(2,3);

// defines pins numbers
const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 11;
const int ledPin = 5;
const int ledpin1 =6;
char phone_no[]="7780741726";

int v=0;  


     
 

// defines variables
long duration;
int distance;
int safetyDistance;



void setup() 
{
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(buzzer, OUTPUT);
pinMode(ledPin, OUTPUT);
pinMode(ledpin1,OUTPUT);
Serial.begin(9600); // Starts the serial communication


/* mySerial.print("\r");
 delay(1000);                  
 mySerial.print("AT+CMGF=1\r");    
 delay(1000);
 /*Replace XXXXXXXXXX to 10 digit mobile number &  ZZ to 2 digit country code*/   
 /*mySerial.print("AT+CMGS=\"+917780741726\"\r");    
 delay(1000);
 //The text of the message to be sent.
 mySerial.print("dustbin clean ");   
 delay(1000);
 mySerial.write(0x1A);
 delay(1000);*/ 
}


void loop() 
{
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the 
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance <=5&&v==0)
{
//distance ;
digitalWrite(buzzer, HIGH);
  digitalWrite(ledPin, HIGH);
  digitalWrite(ledpin1,LOW);
  mySerial.begin(9600);
  delay(2000);
 mySerial.print("\r");
 delay(1000);                  
 mySerial.print("AT+CMGF=1\r");    
 delay(1000);
 /*Replace XXXXXXXXXX to 10 digit mobile number &  ZZ to 2 digit country code*/
 mySerial.print("AT+CMGS=\"+91XXXXXXXXXX\"\r");    
 delay(1000);
 //The text of the message to be sent.
 mySerial.print("DUSTBIN IS FILLED UP TO 85% REGNO:1256 ");   
 delay(1000);
 mySerial.write(0x1A);
 delay(1000); 
 v=1;
}
  if (safetyDistance >5&&v==0 )
  { 
   digitalWrite(ledPin,LOW);
  digitalWrite(ledpin1,HIGH);
  /*mySerial.begin(9600);
    delay(2000);
   mySerial.print("\r"); 
 delay(1000);                  
 mySerial.print("AT+CMGF=1\r");    
 delay(1000);
// Replace XXXXXXXXXX to 10 digit mobile number &  ZZ to 2 digit country code*/
/* mySerial.print("AT+CMGS=\"+91XXXXXXXXXX\"\r");    
 delay(1000);
 //The text of the message to be sent.
 mySerial.print("DUSTBIN CLEANED ");   
 delay(1000);
 mySerial.write(0x1A);
 delay(1000); */
  }
// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay(1000);

}
