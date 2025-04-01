# OdometryData
`<modelec_interface/msg/odometry_data.hpp>`

## Objectif
Transmission des données d'odométrie depuis le controller vers la rasp

## Interface
```cpp
int64 x
int64 y
int64 theta
```

## Params
| Type  | Name  | Description   |
|-------|-------|---------------|
| int64 | x     | position en x |
| int64 | y     | position en y |
| int64 | theta | angle selon z |

## Utilisé par
- [](Odometry-Logic-Processor-Node.md)