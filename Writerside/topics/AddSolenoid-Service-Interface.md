# AddSolenoid
`<modelec_interface/srv/add_solenoid.hpp>`

## Objectif

## Interface
```cpp
uint8 pin
---
bool success
```

## Params

| Type  | Name | Description     |
|-------|------|-----------------|
| uint8 | pin  | pin du solenoid |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
- [](Solenoid-Controller-Node.md)