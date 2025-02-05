# Odométrie

La réalisation de l'odométrie se base sur un hacheur qui alimente deux moteurs CC,
ainsi que de deux encodeurs pour mesurer la distance parcourus par Serge.
Le tout controlée avec une arduino mega pour réaliser un asservissement en position.

## Moteur
{collapsible="true" default-state="expanded"}
### Fréquence signal
{collapsible="true" default-state="expanded"}
La fréquence du signal souhaité pour contrôler les moteurs CC est de 25 KHz.
Or, par default, la fréquence du pwm fournit par les pins GPIO de l'Arduino est de 50 Hz.
Pour ce faire, nous créons une fonction analogWrite25k qui envoie un signal PWM de fréquence 25 kHz
et qui prend en entrée un entier entre 0 et 320 au lieu de 0 et 255.

Cette fonction est active sur 2 timers car nous avons besoin de 2 GPIO PWM par moteur.
Les pins 2, 3, 6, 6, 7, 8 sont donc sur une fréquence de 25 kHz
```C
#define sbi(sfr, bit) (_SFR_BYTE(sfr) |= _BV(bit))

void setup() {
    // Configure Timer 3 for PWM @ 25 kHz.
  TCCR3A = 0;           // undo the configuration done by...
  TCCR3B = 0;           // ...the Arduino core library
  TCNT3  = 0;           // reset timer
  TCCR3A = _BV(COM3A1)  // non-inverted PWM on ch. A
          | _BV(COM3B1)  // same on ch; B
          | _BV(COM3C1)  // same on ch; C
          | _BV(WGM31);  // mode 10: ph. correct PWM, TOP = ICR1
  TCCR3B = _BV(WGM43)   // ditto
          | _BV(CS30);   // prescaler = 1
  ICR3   = 320;         // TOP = 320
    // Configure Timer 4 for PWM @ 25 kHz.
  TCCR4A = 0;           // undo the configuration done by...
  TCCR4B = 0;           // ...the Arduino core library
  TCNT4  = 0;           // reset timer
  TCCR4A = _BV(COM4A1)  // non-inverted PWM on ch. A
          | _BV(COM4B1)  // same on ch; B
          | _BV(COM4C1)  // same on ch; C
          | _BV(WGM41);  // mode 10: ph. correct PWM, TOP = ICR1
  TCCR4B = _BV(WGM43)   // ditto
          | _BV(CS40);   // prescaler = 1
  ICR4   = 320;         // TOP = 320
}

// PWM output @ 25 kHz, only on pins 2, 3, 5 and 6, 7, 8.
// Output value should be between 0 and 320, inclusive.
void analogWrite25k(int pin, int value) {
  if (value < 0) value = 0;
  if (value > 320) value = 320;
  pinMode(pin, OUTPUT);
    switch (pin) {
        case 2:
            sbi(TCCR3A, COM3B1);
            OCR3B = value;
            break;
        case 3:
            sbi(TCCR3A, COM3C1);
            OCR3C = value;
            break;
        case 5:
            sbi(TCCR3A, COM3A1);
            OCR3A = value;
            break;
        case 6:
            sbi(TCCR4A, COM4A1);
            OCR4A = value;
            break;
        case 7:
            sbi(TCCR4A, COM4B1);
            OCR4B = value;
            break;
        case 8:
            sbi(TCCR4A, COM4C1);
            OCR4C = value;
            break;
        default:
            // no other pin will work
            break;
    }
}
```
{collapsible="true" default-state="collapsed"}

### Commande moteur
{collapsible="true" default-state="expanded"}
Pour commander les deux moteurs avec des valeurs positives et négatives, nous utilisons la fonction ci-dessous.
Comme nous les pins en des moteurs sont toujours à 1 nous avons seulement besoin de contrôler les moteurs avec deux pins.
- Les deux vaudront LOW pour arrêter le moteur.
- L'un aura un PWM et l'autre LOW pour faire tourner le moteur dans un sens.
- Inversement pour faire tourner le moteur dans l'autre sens.
```C
void sendCmd(int cmdG,int cmdD){
  if (cmdD>0){
    analogWrite25k(moteurPinDA, cmdD);
    digitalWrite(moteurPinDB, LOW);
  }
  if (cmdG>0){
    digitalWrite(moteurPinGA, LOW);
    analogWrite25k(moteurPinGB, cmdG);
  }

  if(cmdD<0){
    digitalWrite(moteurPinDA, LOW);
    analogWrite25k(moteurPinDB, -cmdD);
  }
  if (cmdG<0){
    analogWrite25k(moteurPinGA, -cmdG);
    digitalWrite(moteurPinGB, LOW);
  }

  if(cmdD==0){
    digitalWrite(moteurPinDA,LOW);
    digitalWrite(moteurPinDB,LOW);
  }

  if(cmdG==0){
    digitalWrite(moteurPinGB,LOW);
    digitalWrite(moteurPinGA,LOW);  
  }

}
```
{collapsible="true" default-state="collapsed"}

## Encodeurs
{collapsible="true" default-state="expanded"}
Pour ce qui est des encodeurs, 
nous utilisons des interruptions afin de compter le nombre de pas parcouru par les roues codeuses.
Nous n'utilisons que la moitié des pas des encodeurs 
(nous prenons utilisons l'interruption seulement sur un des deux pins des encodeurs) 
parce que le compte est suffisament précis avec uniquement la moitié des pas 
et cela permet d'économiser de la puissance de calcul.

```C
// pin
#define interruptionPinDA 2
#define interruptionPinDB 3
#define interruptionPinGA 19
#define interruptionPinGB 18

// compte codeur 
long compteD;
long compteG;
long comptePrecD = 0;
long comptePrecG = 0;

void setup() {
  pinMode(interruptionPinDA, INPUT_PULLUP);
  pinMode(interruptionPinDB, INPUT_PULLUP);
  pinMode(interruptionPinGA, INPUT_PULLUP);
  pinMode(interruptionPinGB, INPUT_PULLUP);
  
  long countD = 0;
  long countG = 0;
  
  attachInterrupt(digitalPinToInterrupt(interruptionPinDA), interruptD, CHANGE);
  attachInterrupt(digitalPinToInterrupt(interruptionPinGA), interruptG, CHANGE);
}

void interruptD()
{
  if (digitalRead(interruptionPinDA) == digitalRead(interruptionPinDB)) {  
    compteD--;
  }else{
    compteD++;
  }
}

void interruptG()
{
  if (digitalRead(interruptionPinGA) == digitalRead(interruptionPinGB)) {  
    compteG++;
  }else{
    compteG--;
  }
}
```
{collapsible="true" default-state="collapsed"}
