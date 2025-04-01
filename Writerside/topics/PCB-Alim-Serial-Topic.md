# PCB Alim

Un usb listener est setup avec comme nom `pcb_alim`, il permet d'envoyer des données au PCB grace au topic [](Send-To-Serial-Topic.md) et de recevoir des données du PCB grace au topic [](Raw-Data-Topic.md).
Les paramètres sont les suivants :
- **name** : `odometry`
- **baudrate** : `115200`
- **serial_port** : `/dev/serial0`

### Publisher
- [](Multiple-Serial-Listener-Node.md)

### Subscriber
- [](PCB-Alim-Interface-Node.md)
