# internal-monitoring-sensors

Thermistor and Photocell code:

#include <math.h>

int photocellPin = 0;
int photocellReading;

double thermistor(int RawADC)
{
  double Temp;
  Temp = log(8520.0*((1024.0/RawADC-1)));
 // Temp = log(8520.0/((1024.0/RawADC-1))); //For full up config
  Temp = 1/(0.001129148 + (0.000234125 + (0.0000000876741 * Temp *Temp))*Temp);

  Temp = Temp - 273.15; //Converts Kelvin to Celcius
  // Temp = (Temp *9.0)/5.0 +32.0; //Converts Celcius to Fahrenheit
  return Temp;
}



void setup() 
{
  // put your setup code here, to run once:
  Serial.begin(9600);
}

void loop() 
{
  Serial.println(" ");
  // put your main code here, to run repeatedly:
  Serial.print("Temperature reading = ");
  Serial.println(int(thermistor(analogRead(x)))); //display Celcius. Let x be the analog you connected to the circut
  
  delay(1000);  

  Serial.println(" ");
  
  photocellReading = analogRead(photocellPin);

  Serial.print("Analog reading = ");
  Serial.println(photocellReading);

  delay(1000);
}




