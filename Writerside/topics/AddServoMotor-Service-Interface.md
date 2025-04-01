# AddServoMotor
`<modelec_interface/srv/add_servo_motor.hpp>`

## Objectif

## Interface
```cpp
uint8 pin
---
bool success
```

## Params

| Type  | Name | Description         |
|-------|------|---------------------|
| uint8 | pin  | pin du servo moteur |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
- [](Arm-Controller-Node.md)
- [](Game-Controller-Listener-Node.md)
- [](PCA9685-Controller-Node.md)