# Practica-6-Nivel-de-Agua-con-LCD

## Descripción

Se programa una pantalla LCD-1602 atraves de un sensor ultrasonico de distancia, dicha pantalla nos indicara el porcentaje de nivel de agua medido en un tanque.

Mientras que 4 Relay Module nos indican lo mismo osea 4 leds encendidos, significa el 100% de nivel de agua en el tanque.

Mientras que 4 Relay Module nos indican lo mismo osea 3 leds encendidos, significa el 75% de nivel de agua en el tanque.

Mientras que 4 Relay Module nos indican lo mismo osea 2 leds encendidos, significa el 50% de nivel de agua en el tanque.

Mientras que 4 Relay Module nos indican lo mismo osea 1 leds encendidos, significa el 25% de nivel de agua en el tanque.

Mientras que 4 Relay Module nos indican lo mismo osea 0 leds encendidos, significa el 0% de nivel de agua en el tanque.


## Material Necesario

- wokwi
- ESP32
- Ultrasonic Sensor
- LCD-1602
- Relay Module 
  
## Programación
```
// defines pins numbers
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

const int trigPin = 4;
const int echoPin = 15;
const int led1 = 12;
const int led2 = 14;
const int led3 = 26;
const int led4 = 25;

// defines variables
long duration;
int distance;
int safetyDistance;


void setup() {
  
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);

Serial.begin(9600); 
lcd.init();
lcd.backlight();
 // Starts the serial communication
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=1 && safetyDistance<=5)
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.clear();
  lcd.setCursor(0,4);
  lcd.print("Tanque 0%");
  delay(200);
}
else if(safetyDistance>=5 && safetyDistance<=100) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.clear();
  lcd.setCursor(-3,4);
  lcd.print("Tanque 25%");
  delay(200);
}
else if (safetyDistance>=101 && safetyDistance<=200)
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.clear();
  lcd.setCursor(-6,4);
  lcd.print("Tanque 50%");
  delay(200);
}
else if (safetyDistance>=201 && safetyDistance<=300)
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
  lcd.clear();
  lcd.setCursor(-6,4);
  lcd.print("Tanque 75%");
  delay(200);
}
else 
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.clear();
  lcd.setCursor(-6,4);
  lcd.print("Tanque lleno");
  delay(200);
}


// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
}
 ```
## Librerías

1. DHT Sensor Library for EXPx
2. LiquidCrystal I2C

## Conexión

![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20202500.png?raw=true)

##Instrucciones de operación 

1. Iniciar Simulador
2. Visualizar los datos en la pantalla LCD
3. Visualizar lo que nos indican los Leds en los modulos de referencia
4. Subir y Bajar la distancia dando doble click al sensor UltraSonic

## Resultados

Los valores serán mostrados en la pantalla LCD, cada 2 segundos se actualizará, mostrará el porcentaje de agua en el tanque basado en la distancia que marca el sensor.

![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20203104.png?raw=true)
![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20203129.png?raw=true)
![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20203154.png?raw=true)
![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20203224.png?raw=true)
![image](https://github.com/MiguelMontesinos/Practica-6-Nivel-de-Agua-con-LCD/blob/main/Captura%20de%20pantalla%202024-12-17%20203238.png?raw=true)

## Desarrollado por 

**Ing. Miguel De Jesus Montesinos Molina** 

[GitHub](https://github.com/MiguelMontesinos).
