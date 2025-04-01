# Odometry

Un usb listener est setup avec comme nom `odometry`, il permet d'envoyer des données à l'odométrie grace au topic [](Send-To-Serial-Topic.md) et de recevoir des données de l'odométrie grace au topic [](Raw-Data-Topic.md).
Les paramètres sont les suivants :
- **name** : `odometry`
- **baudrate** : `115200`
- **serial_port** : `/dev/pts/6`

### Publisher
- [](Multiple-Serial-Listener-Node.md)

### Subscriber
- [](Odometry-Logic-Processor-Node.md)
