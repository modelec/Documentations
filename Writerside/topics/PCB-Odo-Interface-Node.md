# PCB Odo Interface
`<modelec/pcb_odo_interface.hpp>`

## Objectif
Interface de communication avec le PCB Odo.

### Topic
- [](Odoemtry-GetPosition-Topic.md) : recupère la position du robot à partir de l'odométrie et l'envoie.
- [](Odoemtry-SetPosition-Topic.md) : envoie la nouvelle position du robot à l'odométrie.
- [](Odoemtry-Speed-Topic.md) : recupère la vitesse du robot à partir de l'odométrie et l'envoie.
- [](Odoemtry-ToF-Topic.md) : recupère la distance du robot à l'obstacle le plus proche et l'envoie.
- [](Odoemtry-WaypoointReach-Topic.md) : envoie un message lorsque le robot a atteint un waypoint.
- [](Odoemtry-AddWaypoint-Topic.md) : ajoute un waypoint à la liste des waypoints à atteindre.
- [](Odoemtry-GetPID-Topic.md) : recupère les valeurs des PID de l'odométrie et les envoie.
- [](Odoemtry-SetPID-Topic.md) : envoie les nouvelles valeurs des PID de l'odométrie.

### Service
- [](Odometry-ToF-Service.md) : recupère la distance du robot à l'obstacle le plus proche.
- [](Odometry-Speed-Service.md) : recupère la vitesse du robot à partir de l'odométrie.
- [](Odometry-GetPosition-Service.md) : recupère la position du robot à partir de l'odométrie.
- [](Odometry-Start-Service.md) : demarre l'odométrie.
- [](Odometry-GetPID-Service.md) : recupère les valeurs des PID de l'odométrie.
- [](Odometry-SetPID-Service.md) : envoie les nouvelles valeurs des PID de l'odométrie.
- [](Odometry-AddWaypoint-Service.md) : ajoute un waypoint à la liste des waypoints à atteindre.
