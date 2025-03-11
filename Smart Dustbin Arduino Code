#include <Servo.h>
Servo servo1;
const int trigPin = 12;
const int echoPin = 11;
const int min_distance = 1; // Minimum distance considered over soil
const int max_distance = 20; // Maximum distance considered over soil
const int min_soil_moisture = 0; // Minimum soil moisture value
const int max_soil_moisture = 100; // Maximum soil moisture value

long duration;
int distance=0;
int potPin = A0; //input pin
int soil=0;
int fsoil;
void setup() 
{
  Serial.begin(9600);
//Serial.print("Humidity");
pinMode(trigPin, OUTPUT); 
pinMode(echoPin, INPUT); 
servo1.attach(8);
}void loop() {
  int soil = 0;
  
  for(int i = 0; i < 2; i++) {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(7);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    delayMicroseconds(10);
    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2 + distance;
    delay(10);
  }
  
  distance = distance / 2;
  Serial.println(distance);
  
  if (distance >= min_distance && distance <= max_distance) {
    delay(1000);
    
    for(int i = 0; i < 3; i++) {
      soil = analogRead(potPin);
      soil = constrain(soil, 485, 1023);
      fsoil = (map(soil, 485, 1023, 100, 0)) + fsoil;
      delay(75);
    }
    
    fsoil = fsoil / 3;
    Serial.print("Soil Moisture: ");
    Serial.print(fsoil);
    Serial.println("%");
    
    if (fsoil > 3) {
      Serial.println("Wet");
      servo1.write(180);
      delay(3000);
    } else {
      Serial.println("Dry");
      servo1.write(-180);
      delay(3000);
    }
    
    servo1.write(90);
  }
  
  distance = 0;
  fsoil = 0;
  delay(1000);
}
