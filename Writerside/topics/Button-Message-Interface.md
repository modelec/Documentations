# Button
`<modelec_interface/msg/button.hpp>`

## Objectif
Bouton on / off.

## Interface
```cpp
uint8 pin
bool state
```

## Params

| Type  | Name  | Description     |
|-------|-------|-----------------|
| uint8 | pin   | pin du solenoid |
| bool  | state | état du bouton  |

## Utilisé par
- [](Button-GPIO-Controller-Node.md)