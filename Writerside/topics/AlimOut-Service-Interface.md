# AlimOut
`<modelec_interface/srv/alim_out.hpp>`

## Objectif
Vérifier l'état des sorties d'alimentation.

## Interface
```cpp
string OUT_5V="OUT5V"
string OUT_5V1="OUT5V1"
string OUT_12V="OUT12V"
string OUT_24V="OUT24V"

string STATE="STATE"
string VOLT="VOLT"
string AMPS="AMPS"

string out
string type "STATE"
int8 enable -1
---
bool success
int64 result
```

## Params

| Type   | Name   | Description                                            |
|--------|--------|--------------------------------------------------------|
| string | out    | nom de la sortie d'alimentation                        |
| string | type   | type de la requête                                     |
| int8   | enable | 1 pour activer, 0 pour désactiver, -1 pour lire l'état |

## Retour

| Type  | Name    | Description            |
|-------|---------|------------------------|
| bool  | success | requête réussie ou non |
| int64 | result  | résultat de la requête |

## Utilisé par
