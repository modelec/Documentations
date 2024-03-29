# Pixel
## Objectif
Pixel est un PAMI qui a donc pour objectif, dans les 10 dernières secondes, d'aller jusqu'à une zone et toucher
une plante dans cette zone une fois arrêté.

## Matèriel
{collapsible="true" default-state="expanded"}
- [Arduino uno](https://store.arduino.cc/products/arduino-uno-rev3)
- [CNC shield V3](https://www.amazon.fr/dExtension-Protection-Dissipateurs-Chaleur-Imprimante/dp/B07NP1DC65/ref=sr_1_6?dib=eyJ2IjoiMSJ9.JI-ma4M3AlfmZl1BozwoTpeIndYTV1RwLI0M08S6BJZL-oFJlHtbZtLUkrEXQXpujV70jkBJ24QwKIJ6h_SApP-npLF2ZLboF3EbqUKFi4al6-yxqHa8ix2sQrp6haEfEsgB0scgwkNbuo0Y2uru13x8-fIP2lwXuxIRafkffpbNBj7tc0G9vYUFDGlZ2o6p9Q-oFG-96sTmfJfE4u-SKVASjABScizKRj-TkTW8luvWboypEQIb3Ouw8uRzp2q9p2ISasbk4ZtwR2IAnndcURcSRFkZBL3iMTbXCG4SIX8.1J5rZ6CAHRMVCCVTgxMIw92O-CKN1PB2_18OYL9-wEo&dib_tag=se&keywords=cnc+shield&qid=1711545332&sr=8-6)
- [Moteur pas à pas * 2](https://www.amazon.fr/STEPPERONLINE-bipolaire-connecteur-imprimante-fraiseuse/dp/B0B38GX54H/ref=sr_1_4?__mk_fr_FR=ÅMÅŽÕÑ&crid=2Y7V0JYZLHNYN&dib=eyJ2IjoiMSJ9.pU8qhsS9CN5zYAeTOHgus2uSvLfbXPUMelD5i5HgQ8mrZ9WrLHugLzgYz1a0kqPcFaqqA4fibf6BnxSplcy7X2N445OwRl0098Cxr2KhY_dZA6FXLx5KUji1pSONjkGjDMW6RcvSgHOAgdcs27w5BEKTTi-lSprvZei7kczmnCJCr_91Gu3z_ojy6J8B5KsShZ-VMcimonv6BAdFmC4Hz6v2Pn5RRzbgEF-awp57LFgskZMkFTbdCdDZwIjSf2Ve3G6PZiEFTEs5U-Tzo_M_0aqSEULkJqpIKevZVXoLIWk.6h_q4gETAHeYGQSxt964emzU45oSIo-Bux3VG8vK9BY&dib_tag=se&keywords=Moteur+pas+a+pas&qid=1711545588&s=industrial&sprefix=moteur+pas+a+pas%2Cindustrial%2C94&sr=1-4)
- [Capteur laser * 2](https://www.amazon.fr/AZDelivery-VL53L0X-Capteur-distance-incluant/dp/B086V37JJ7/ref=sr_1_9?dib=eyJ2IjoiMSJ9.QXns_kdhCZmsBcYOFdizbDvA7zSZ_D9yaBtkJX0Ga87xd-Otask3YcUaYQn-D0eiZj9i5pS_fr2sbggtlC20ksBOf38W7ouQcRNTKGCD9GeOdzqVRPeIo_zj4QzIEXBcS2EMcM3hYyW9PD02dgZzSQ2eAagE9c68nUUD9nQ-aK16e_Ogh8kmNFXSW9gAlrcQxuZ5gt0GYlq7muIWyC_PU8CSIfvZxt3HEvOqaZISWC9gnX--5aO6zW1A-_cUWQ9xkf5SnuGhMaZc2644DacgZXyTy1UyhtbvETO-oYlywuc.SrYnuIBZr82N3FJzMM4KCfcinZaC78XeTsFftJqsSpg&dib_tag=se&keywords=Capteur+laser&qid=1711545624&sr=8-9)
- [Batterie Lipo 3S](lien batterie)
- [Bouton d'arrêt d'urgence](https://www.amazon.fr/Larret-durgence-Poussoir-Capuchon-Champignon/dp/B07RGQQTW8/ref=sr_1_12?__mk_fr_FR=ÅMÅŽÕÑ&crid=2OVF0E40NTHRC&dib=eyJ2IjoiMSJ9.oMd288voXmAfcNkFoPVqN8yayhHZ_JEXt8cUfmya2E9XZ9i3udjK0IHC6DeyZzdjGWWzUAVxiPDkPDrNntZVGDJ6in03uUXDkFXrk780uat5tKwQuj86BdigBSeRWAhoUEhx7ZnMCCoVJPrePwVLoMFQYKUWVOEQEnVQWdYVuS8P4AR58V4WQdbHZA-XsinvRF-_ybyPM4VSdbgkk7ZJb--0hciNIL6vu3teD62YoAEBDLs3rIwWwqm2w5QJ7Dm17uPyuJp5V-u0XXYCAtfidCDOER-PFhjYwOWNQ1di420.vY_SfWlzo0l8sp1uT0ZDFczzR4wlpovj7BgRyBn8CKk&dib_tag=se&keywords=Bouton+d%27arret+d%27urgence&qid=1711545690&sprefix=bouton+d%27arret+d%27urgence%2Caps%2C106&sr=8-12)
- [Tirette magnétique](lien tirette)
- [Chassis en impression 3D](lien fichier)
- [Switch](lien produit)

## Fonctionnement
{collapsible="true" default-state="expanded"}
### Detection contacte plante
Le switch permet de détecter lorsque le robot pousse sur une plante contre un mur
et donc de s'arrêter au contact d'une plante dans la zone d'arrivée.

### Detection d'adversaire
Les capteurs lasers permettent de détecter un robot adverse approchant.
Par ailleurs, le switch permet de détecter un contact avec un robot adverse.

### Direction
Pixel suit un mur, à une distance fixe, à l'aide d'un capteur laser afin d'aller à une zone d'arrivée.


## Code
{collapsible="true" default-state="collapsed"}
<tabs>
<tab title="Capteurs">
Permet de contrôler deux capteurs lasers via un bus I2C en, dans un premier temps, attribuant une adresse pour 
l'I2C différente pour chaque capteur laser. Par la suite, il récupère en permanence la distance en mm que renvoient les 
capteurs et l'envoie dans le serial suivi du pin xshut associé au capteur (séparer par '|'). Chaque capteur est séparé 
par une tabulation dans le serial.

```C
#include <Wire.h>
#include <VL53L0X.h>

// The number of sensors in your system.
const uint8_t sensorCount = 2;
// The Arduino pin connected to the XSHUT pin of each sensor.
const uint8_t xshutPins[sensorCount] = { 4, 5 };

VL53L0X sensors[sensorCount];

void setup()
{
  while (!Serial) {}
  Serial.begin(9600);
  Wire.begin();
  Wire.setClock(400000); // use 400 kHz I2C

  // Disable/reset all sensors by driving their XSHUT pins low.
  for (uint8_t i = 0; i < sensorCount; i++)
  {
    pinMode(xshutPins[i], OUTPUT);
    digitalWrite(xshutPins[i], LOW);
  }

  // Enable, initialize, and start each sensor, one by one.
  for (uint8_t i = 0; i < sensorCount; i++)
  {
    // Stop driving this sensor's XSHUT low. This should allow the carrier
    // board to pull it high. (We do NOT want to drive XSHUT high since it is
    // not level shifted.) Then wait a bit for the sensor to start up.
    pinMode(xshutPins[i], INPUT);
    delay(10);

    sensors[i].setTimeout(500);
    if (!sensors[i].init())
    {
      Serial.print("Failed to detect and initialize sensor ");
      Serial.println(i);
      while (1);
    }

    // Each sensor must have its address changed to a unique value other than
    // the default of 0x29 (except for the last one, which could be left at
    // the default). To make it simple, we'll just count up from 0x2A.
    sensors[i].setAddress(0x2A + i);

    sensors[i].startContinuous(50);
  }
}

void loop()
{
  for (uint8_t i = 0; i < sensorCount; i++)
  {    
    Serial.print(sensors[i].readRangeSingleMillimeters());
    Serial.print(" | ");
    Serial.print(xshutPins[i]);
    if (sensors[i].timeoutOccurred()) { Serial.print(" TIMEOUT"); }
    Serial.print('\t');
  }
  Serial.println();
}
```
{collapsible="true"}

</tab>
<tab title="Moteurs">
Permet de contrôler les deux moteurs en même temps afin de test si le cablage est valide.

```C
Code moteurs
```
{collapsible="true"}

</tab>
<tab title="Switch">
Permet de détecter l'appuie sur le switch.

```C
Code Switch
```
{collapsible="true"}

</tab>
<tab title="Code Complet">
Code complet de Pixel qui implémente la détection des adversaires grâce aux capteurs et au switch, le suivi des murs 
grâce aux capteurs et aux moteurs ainsi que la détection de pots grâce au switch. Le tout afin de s'arrêter dans la zone et au contact d'une plante.

```C
Code Complet
```
{collapsible="true"}

</tab>
</tabs>
