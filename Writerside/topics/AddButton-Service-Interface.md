# AddButton
`<modelec_interface/srv/add_button.hpp>`

## Objectif
Ajouter le contrôle d'un bouton.

## Interface
```cpp
uint8 pin
string name
---
bool success
```

## Params

| Type   | Name | Description   |
|--------|------|---------------|
| uint8  | pin  | pin du bouton |
| string | name | nom du bouton |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
- [](Button-GPIO-Controller-Node.md)