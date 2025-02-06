# Moteur CC
[Ref Moteur](https://www.pololu.com/product/4746)
## Montage moteur avec hacheur : 

Pour le montage, on utilise celui qui est donné avec la doc du hacheur (DBH-12):
[Doc Hacheur](https://dronebotworkshop.com/dc-motor-drivers/)
 
Montage (12V tiré du pcb alimentation):  
![Montage Moteur Seul Sur Hacheur](../../img/moteurs/Montage moteur seul.png){ width="800" }

Code de test sur arduino :
```Arduino
 DBH-12 H-Bridge Demo
  dbh-12-demo.ino
  Demonstrates operation of DBH-12 Dual H-Bridge Motor Driver
    
  DroneBot Workshop 2022
  https://dronebotworkshop.com
*/
 
// Motor Connections (All must use PWM pins)
#define IN1A 3
#define IN1B 5
#define IN2A 6
#define IN2B 9
 
// Define a fixed speed - do not exceed 250
int fixedSpeed = 80;
 
void setup() {
 
  // Set motor & enable connections as outputs
  pinMode(IN1A, OUTPUT);
  pinMode(IN1B, OUTPUT);
  pinMode(IN2A, OUTPUT);
  pinMode(IN2B, OUTPUT);
 
  // Stop motors
  analogWrite(IN1A, 0);
  analogWrite(IN1B, 0);
  analogWrite(IN2A, 0);
  analogWrite(IN2B, 0);
}
 
void loop() {
 
  // Accelerate both forward
  digitalWrite(IN1A, LOW);
  digitalWrite(IN1B, LOW);
  for (int i = 0; i < 200; i++) {
    analogWrite(IN2A, i);
    analogWrite(IN2B, i);
    delay(20);
  }
 
  delay(500);
 
  // Decelerate both forward
  for (int i = 200; i >= 0; i--) {
    analogWrite(IN2A, i);
    analogWrite(IN2B, i);
    delay(20);
  }
 
  delay(500);
 
  // Accelerate both reverse
  digitalWrite(IN2A, LOW);
  digitalWrite(IN2B, LOW);
  for (int i = 0; i < 200; i++) {
    analogWrite(IN1A, i);
    analogWrite(IN1B, i);
    delay(20);
  }
 
  delay(500);
 
  // Decelerate both reverse
  for (int i = 200; i >= 0; i--) {
    analogWrite(IN1A, i);
    analogWrite(IN1B, i);
    delay(20);
  }
 
  delay(500);
 
  // Move in opposite directions at fixed speed
  digitalWrite(IN1A, LOW);
  digitalWrite(IN2B, LOW);
  analogWrite(IN1B, fixedSpeed);
  analogWrite(IN2A, fixedSpeed);
 
  delay(3000); 
 
  // Stop
  analogWrite(IN1A, 0);
  analogWrite(IN1B, 0);
  analogWrite(IN2A, 0);
  analogWrite(IN2B, 0);
 
  delay(2000);
}
```
{collapsible="true"}