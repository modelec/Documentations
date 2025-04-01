# ServoMode
<primary-label ref="Deprecated"/>

`<modelec_interface/msg/servo_mode.hpp>`

## Objectif
Activer / désactiver un servo moteur (dans le contexte de Serge).

## Interface
```cpp
uint8 PINCE_CLOSED=0
uint8 PINCE_MIDDLE=1
uint8 PINCE_OPEN=2
uint8 PINCE_FULLY_OPEN=3
uint8 ARM_BOTTOM=4
uint8 ARM_MIDDLE=5
uint8 ARM_TOP=6

uint8 pin
uint8 mode
bool is_arm
```

> DEPECATED: Ce message était utilisé pour [Serge](Serge.md)
> Il va donc être supprimé dans une prochaine version.
{style="warning"}

## Params

| Type  | Name   | Description          |
|-------|--------|----------------------|
| uint8 | pin    | pin du solenoid      |
| uint8 | mode   | mode du servo moteur |
| bool  | is_arm | si c'est un bras     |

## Utilisé par
- [](Arm-Controller-Node.md)
- [](Game-Controller-Listener-Node.md)