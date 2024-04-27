#include <Arduino.h>
#include <DHT.h>

#define DHTPIN 2     // Pin where the DHT11/DHT22 is connected
#define DHTTYPE DHT11   // DHT 11
const int lightSensorPin = A1;
const int relayPin = 7;  //connected to digital Pin 7 
const int moistureSensorPin = A2;
DHT dht(DHTPIN, DHTTYPE);
const int min_realvalue = 0; 
const int max_realvalue = 100; 
void setup() {
  Serial.begin(9600);
  pinMode(relayPin, OUTPUT);
  dht.begin();
}
void pump (){
   
}
void loop() {
   int sensorValue1 = analogRead(moistureSensorPin);
   Serial.print("Moisture:  ");
   Serial.print(sensorValue1);
 
  
  int sensorValue = analogRead(lightSensorPin); //taking reading
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();  // Celsius by default
   if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  if (sensorValue1 <= 230){
    digitalWrite(relayPin, LOW);  // Turn the relay on
      
  }
  else {
      digitalWrite(relayPin, HIGH);   // Turn the relay off    
  }
  // Check if any reads failed and exit early (to try again).
 
  Serial.print("The Light: "); 
  Serial.print(sensorValue);
  Serial.print(" \t ");  
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  
                // Wait for 1 second
  delay(1000);   
}

