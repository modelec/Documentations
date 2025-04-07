# OdometryToF
`<modelec_interface/msg/odometry_to_f.hpp>`

## Objectif
Récupérer la distance entre le robot et un obstacle à l'aide d'un capteur ToF.

## Interface
```cpp
int8 n
int64 distance
```

## Params

| Type  | Name     | Description                         |
|-------|----------|-------------------------------------|
| uint8 | n        | numéro du capteur                   |
| int64 | distance | distance calculé par le capteur ToF |

## Utilisé par
- 