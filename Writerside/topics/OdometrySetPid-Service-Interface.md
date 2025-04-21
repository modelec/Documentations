# OdometrySetPid
`<modelec_interface/srv/odometry_set_pid.hpp>`

## Objectif
Configurer le PID de l'odométrie.

## Interface
```cpp
float32 p
float32 i
float32 d
---
bool success
```

## Params

| Type    | Name | Description           |
|---------|------|-----------------------|
| float32 | p    | valeur du paramètre P |
| float32 | i    | valeur du paramètre I |
| float32 | d    | valeur du paramètre D |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
-