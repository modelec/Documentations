# AlimIn
`<modelec_interface/srv/alim_in.hpp>`

## Objectif
Vérifier l'état de l'alimentation.

## Interface
```cpp
string VOLT="VOLT"
string AMPS="AMPS"
string STATE="STATE"
string VALID="VALID"

int16 input
string type "STATE"
---
bool success
int64 result
```

## Params

| Type   | Name  | Description                                   |
|--------|-------|-----------------------------------------------|
| int16  | input | input 1 ou 2                                  |
| string | type  | type de la requête (VOLT, AMPS, STATE, VALID) |

## Retour

| Type  | Name    | Description            |
|-------|---------|------------------------|
| bool  | success | requête réussie ou non |
| int64 | result  | résultat de la requête |

## Utilisé par
