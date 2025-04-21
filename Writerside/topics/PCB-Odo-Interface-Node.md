# PCB Odo Interface
`<modelec/pcb_odo_interface.hpp>`

## Objectif
Interface de communication avec le PCB Odo.
[](Pilotage-PCB-odometrie.md)

### Topic
- [](Odometry-GetPosition-Topic.md) : recupère la position du robot à partir de l'odométrie et l'envoie.
- [](Odometry-SetPosition-Topic.md) : envoie la nouvelle position du robot à l'odométrie.
- [](Odometry-Speed-Topic.md) : recupère la vitesse du robot à partir de l'odométrie et l'envoie.
- [](Odometry-ToF-Topic.md) : recupère la distance du robot à l'obstacle le plus proche et l'envoie.
- [](Odometry-WaypointReach-Topic.md) : envoie un message lorsque le robot a atteint un waypoint.
- [](Odometry-AddWaypoint-Topic.md) : ajoute un waypoint à la liste des waypoints à atteindre.
- [](Odometry-GetPID-Topic.md) : recupère les valeurs des PID de l'odométrie et les envoie.
- [](Odometry-SetPID-Topic.md) : envoie les nouvelles valeurs des PID de l'odométrie.

### Service
- [](Odometry-ToF-Service.md) : recupère la distance du robot à l'obstacle le plus proche.
- [](Odometry-Speed-Service.md) : recupère la vitesse du robot à partir de l'odométrie.
- [](Odometry-GetPosition-Service.md) : recupère la position du robot à partir de l'odométrie.
- [](Odometry-Start-Service.md) : demarre l'odométrie.
- [](Odometry-GetPID-Service.md) : recupère les valeurs des PID de l'odométrie.
- [](Odometry-SetPID-Service.md) : envoie les nouvelles valeurs des PID de l'odométrie.
- [](Odometry-AddWaypoint-Service.md) : ajoute un waypoint à la liste des waypoints à atteindre.
