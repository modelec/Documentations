# OdometryToF
`<modelec_interface/srv/odometry_to_f.hpp>`

## Objectif
Recupérer la distance entre le robot et un obstacle à l'aide d'un capteur ToF.

## Interface
```cpp
uint8 n
---
int64 distance
```

## Params

| Type  | Name    | Description       |
|-------|---------|-------------------|
| uint8 | n       | numéro du capteur |

## Retour

| Type   | Name     | Description                         |
|--------|----------|-------------------------------------|
| int64  | distance | distance calculé par le capteur ToF |

## Utilisé par
- 