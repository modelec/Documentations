# OdometrySpeed
`<modelec_interface/msg/odometry_speed.hpp>`

## Objectif
Récuperer la vitesse du robot à partir de l'odométrie.

## Interface
```cpp
int64 x
int64 y
int64 theta
```

## Params

| Type  | Name  | Description                                 |
|-------|-------|---------------------------------------------|
| int64 | x     | vitesse selon l'axe x (mm^2)                |
| int64 | y     | vitesse selon l'axe x (mm^2)                |
| int64 | theta | vitesse angulaire autour de l'axe z (rad^2) |

## Utilisé par
- 