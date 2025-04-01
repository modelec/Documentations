# Button
`<modelec_interface/srv/button.hpp>`

## Objectif
Connaitre l'état d'un bouton.

## Interface
```cpp
uint8 pin
string name
---
bool status
```

## Params

| Type   | Name | Description    |
|--------|------|----------------|
| uint8  | pin  | pin du button  |
| string | name | nom du button  |

## Retour

| Type | Name   | Description      |
|------|--------|------------------|
| bool | status | statue du bouton |

## Utilisé par
- [](Button-GPIO-Controller-Node.md)