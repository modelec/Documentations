# OdometryAddWaypoint
`<modelec_interface/srv/odometry_add_waypoint.hpp>`

## Objectif
Ajouter un waypoint à la liste des waypoints de l'odométrie.

## Interface
```cpp
int8 id
bool is_end
int64 x
int64 y
int64 theta
---
bool success
```

## Params

| Type  | Name   | Description       |
|-------|--------|-------------------|
| uint8 | id     | id du waypoint    |
| bool  | is_end | waypoint de fin   |
| int64 | x      | coordonnée x      |
| int64 | y      | coordonnée y      |
| int64 | theta  | angle du waypoint |

## Retour

| Type | Name    | Description            |
|------|---------|------------------------|
| bool | success | requête réussie ou non |

## Utilisé par
-