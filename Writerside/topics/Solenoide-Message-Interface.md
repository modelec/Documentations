# Solénoïde
`<modelec_interface/msg/solenoid.hpp>`

## Objectif
Activer / désactiver un solénoïde.

## Interface
```cpp
uint8 pin
bool state
```

## Params

| Type  | Name  | Description      |
|-------|-------|------------------|
| uint8 | pin   | pin du solenoid  |
| bool  | state | état du solenoid |

## Utilisé par
- [](Solenoid-Controller-Node.md)