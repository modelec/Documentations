# GUI packages

Modelec utilise Qt6 pour créer l'interface graphique de son robot.
> ROS2 utilise nativement Qt5 pour l'interface graphique, mais nous avons choisi de passer à Qt6 pour des raisons de compatibilité et de fonctionnalités.

## Installation de Qt6
Pour installer Qt6 sur votre Raspberry Pi, suivez les instructions suivantes :
- exécutez la commande suivante :
```bash
sudo apt install qt6-base-dev qt6-base-dev-tools
```

## Programmation de l'interface graphique
L'interface graphique est developpée dans le package ros <modelec_gui> et tourne dans une Node (ce qui lui permet d'échanger avec les autres Nodes du projet).