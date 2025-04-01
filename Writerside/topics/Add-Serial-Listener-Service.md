# Add Serial Listener

## Nom du service : **add_serial_listener**
[Interface](AddSerialListener-Service-Interface.md)

## Objectif
Setup un listener sur un nouveau port série.
Deux topics sont ensuite créés :
- [](Raw-Data-Topic.md) : pour recevoir les données brutes du port série.
- [](Send-To-Serial-Topic.md) : pour envoyer des données vers le port série.

### Service
- [](Multiple-Serial-Listener-Node.md)

### Client
- [](PCB-Alim-Interface-Node.md)
- [](Game-Controller-Listener-Node.md)
- [](Odometry-Logic-Processor-Node.md)
