# PCA9685Servo
`<modelec_interface/msg/pca9685_servo.hpp>`

## Objectif
Activer / désactiver un servo moteur.

## Interface
```cpp
uint8 pin
int64 angle
```

## Params

| Type  | Name  | Description           |
|-------|-------|-----------------------|
| uint8 | pin   | pin du solenoid       |
| int64 | angle | angle du servo moteur |

## Utilisé par
- [](PCA9685-Controller-Node.md)
- [](Arm-Controller-Node.md)
- [](Game-Controller-Listener-Node.md)