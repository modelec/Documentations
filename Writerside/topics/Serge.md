# Serge

## Objectif
Serge est un robot qui a pour objectif de déplacer des plantes et d'orienter des panneaux solaires. Pour cela il doit être completement autonome.

## Matèriel
{collapsible="true" default-state="expanded"}
- [Raspberry Pi 5](https://www.kubii.com/fr/cartes-nano-ordinateurs/4106-1831-raspberry-pi-5-3272496315938.html#/ram-4_gb)
- [Raspberry Pi Camera](https://www.kubii.com/fr/cameras-capteurs/3878-1690-module-camera-v3-raspberry-pi-3272496313699.html#/angle_de_camera-grand_angle_120)

## Fonctionnement
{collapsible="true" default-state="expanded"}
### Détéction d'une plante
La détéction des plantes est géré par OpenCV, le code est disponible [ici](https://github.com/modelec/detection_pot).

### Détéction de l'adversaire
La détéction de l'adversaire des géré par le Lidar, le code est disponible [ici](https://github.com/modelec/detection_adversaire)

