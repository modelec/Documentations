# OdometryPosition
`<modelec_interface/srv/odometry_position.hpp>`

## Objectif
Récuperer la position du robot à partir de l'odométrie.

## Interface
```cpp
---
int64 x
int64 y
int64 theta

```

## Params

| Type | Name | Description |
|------|------|-------------|
|      |      |             |

## Retour

| Type  | Name  | Description                 |
|-------|-------|-----------------------------|
| int64 | x     | position selon l'axe x (mm) |
| int64 | y     | position selon l'axe x (mm) |
| int64 | theta | angle selon l'axe x (rad)   |

## Utilisé par
-