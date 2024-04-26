# Serge

## Objectif
Serge est un robot qui a pour objectif de déplacer des plantes et d'orienter des panneaux solaires. Pour cela il doit être completement autonome.

## Matèriel
{collapsible="true" default-state="expanded"}
- [Raspberry Pi 5](https://www.kubii.com/fr/cartes-nano-ordinateurs/4106-1831-raspberry-pi-5-3272496315938.html#/ram-4_gb)
- [Raspberry Pi Camera](https://www.kubii.com/fr/cameras-capteurs/3878-1690-module-camera-v3-raspberry-pi-3272496313699.html#/angle_de_camera-grand_angle_120)
- [Arduino Mega](https://store.arduino.cc/products/arduino-mega-2560-rev3)
- [Batterie 3s 3000 mAh](https://www.amazon.fr/dp/B07LFRFY1S?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Alimentation 12V à 5V](https://www.amazon.fr/dp/B071ZRXKJY?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Boutton d'arret d'urgence](https://www.amazon.fr/dp/B07RGQQTW8?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Servomoteur](https://www.amazon.fr/dp/B07H88DB8R?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Roulements blindés](https://www.amazon.fr/dp/B09DC4S99S?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Interface IIC](https://www.amazon.fr/dp/B07RG9ZTMD?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- [Moteur](https://www.amazon.fr/gp/product/B088PW9B8G/ref=ppx_yo_dt_b_asin_title_o03_s00?ie=UTF8&psc=1)
- [Encodeur](https://www.amazon.fr/gp/product/B08YNYPHTZ/ref=ppx_yo_dt_b_asin_title_o04_s00?ie=UTF8&psc=1)
- [PCB Puissance](https://github.com/modelec/pcb_puissance)

## Fonctionnement
{collapsible="true" default-state="expanded"}
### Détéction d'une plante
La détéction des plantes est gérée par OpenCV, le code est disponible [ici](https://github.com/modelec/detection_pot).

### Détéction de l'adversaire
La détéction de l'adversaire est gérée par le Lidar, le code est disponible [ici](https://github.com/modelec/detection_adversaire)
