# Installation

Si vous êtes sur Windows, il est recommandé d'utiliser WSL (Windows Subsystem for Linux) pour installer ROS2. Si vous êtes sur Linux, vous pouvez suivre les instructions ci-dessous.
> Il existe tout de même une version de [ROS2 pour Windows](https://docs.ros.org/en/foxy/Installation/Windows-Install-Binary.html), mais elle est moins stable et moins bien supportée que la version Linux.
> De plus aucun test n'a été effectué sur cette version. À vos risques et périls.

## Installation sur WSL

### Installation ROS2 sur WSL
Installation de ROS2 sur WSL (Windows Subsystem for Linux) pour Windows. Il est recommandé d'utiliser la version 22.04 d'Ubuntu, car elle est plus stable et compatible avec ROS2.
Ensuite, suivez la documentation officielle de [ROS2 Jazzy](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)

Il faut savoir que le projet ne peut pas être lancé directement depuis WSL, Modelec utilise la librairie [WiringPi](https://github.com/WiringPi/WiringPi) pour utiliser les GPIO de la Raspberry Pi. Lorsque vous lancez le projet autre part que sur une Raspberry Pi, la lib detecteras qu'elle n'est pas sur une Raspberry Pi et ne fonctionnera pas. Il faut donc lancer le projet sur la Raspberry Pi.
Tout de même, il est possible de faire tourner le projet sans les `Nodes` liés aux actionneurs et capteurs. (Vous pouvez lancer des Nodes indépendamment de ceux liés aux actionneurs et capteurs de plus WiringPi va seulement afficher des erreurs, mais ne vas pas "cassé" le projet).

### Developpement sur WSL
Pour développer sur WSL, vous pouvez utiliser différent IDE, actuellement, nous utilisons VS-Code ainsi que CLion. Pour utiliser VS-Code, ouvrez simplement votre projet WSL, pour CLion rendez-vous [ici](ROS2-avec-JetBrain-pour-windows.md) pour savoir comment le configurer.
