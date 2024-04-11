# Code

Installation des différents programmes du robot
{collapsible="true" default-state="collapsed"}
<tabs>
<tab title="Dépendances">
Installtion des dépendances pour les différents programmes de Serge
lxqt est necessaire car il install des lib manquantes pour l'ihm

```BASH
sudo apt install build-essential cmake gcc libopencv-dev qt6-base-dev qt6-base-dev-tools lxqt-core qt6-wayland libcamera-dev
mkdir Serge && cd Serge
chmod 700 /run/user/1000
crontab -e
@reboot chmod 700 /run/user/1000
```
{collapsible="true"}
</tab>
<tab title="Client TCP">
Installation du client TCP, il sert à recevoir et à envoyer les paquets TCP pour l'interconnexion entre les différents programmes de Serge

```BASH
git clone https://github.com/modelec/TCPSocketClient.git
cd TCPSocketClient/
mkdir build && cd build
cmake ..
sudo make 
cd ../..
```
{collapsible="true"}
</tab>
<tab title="Serveur TCP">
Installation du serveur TCP, il sert à gérer les paquets TCP pour l'interconnexion des différents programmes de Serge.

```BASH
git clone https://github.com/modelec/TCPSocketServer.git
cd TCPSocketServer/
mkdir build && cd build
cmake ..
make
cd ../..
```
{collapsible="true"}
</tab>
<tab title="Détéction de l'adversaire">
Installation du programme de détéction de l'adversaire, il utilise le Lidar pour détécter la présence d'adversaire afin de ne pas leur rentrer dedans.

```BASH
git clone https://github.com/Slamtec/rplidar_sdk.git
cd rplidar_sdk/
make
cd ..
git clone https://github.com/modelec/detection_adversaire.git
cd detection_adversaire/
mkdir build && cd build
cmake ..
make
cd ../..
```
{collapsible="true"}
</tab>
<tab title="Contrôle des servo-moteurs">
Installation du programme de contrôle des servo-moteurs, il sert à contrôler les servo moteurs utile pour les différents actionneurs.

````Bash
git clone https://github.com/barulicm/PiPCA9685.git
cd PiPCA9685
xargs -a apt_dependencies.txt sudo apt-get install -y
cmake -B build
cmake --build build
sudo cmake --install build
cmake --build build --target install_python
cd ..
git clone https://github.com/modelec/servo_moteurs.git -b tcp-newlib
cd servo_moteurs/
mkdir build && cd build
cmake ..
make
cd ../..
````
{collapsible="true"}
</tab>
<tab title="IHM">
Installation de l'IHM, l'IHM sert à controler les différents systèmes ainsi qu'à lancer Serge.

````Bash
git clone https://github.com/modelec/ihm.git
cd ihm
mkdir build && cd build
cmake ..
make
cd ../..
````
{collapsible="true"}
</tab>
<tab title="Connecteur raspi -> ardiuno">
Installation du connecteur raspi -> arduino, il sert à transmettre les ordres de la raspi à l'arduino.

````Bash
git clone https://github.com/modelec/connectors.git -b tcp
cd connectors/
mkdir build && cd build
cmake ..
make
cd ../..
````
{collapsible="true"}
</tab>
<tab title="Détéction des pots et des panneaux solaires">
Installation du programme de détéction des pots et des panneaux solaires, il sert à détécter les pots et à transmettre leurs coordonner, même chose pour les panneaux solaires avec l'orientation en plus.

````Bash
git clone https://github.com/kbarni/LCCV.git
cd LCCV
mkdir build
cd build
cmake ..
make
sudo make install
cd ../..
git clone https://github.com/modelec/detection_pot.git -b rasp-curved-aruco
cd detection_pot/
mkdir build && cd build
cmake ..
make
cd ../..
````
{collapsible="true"}
</tab>
<tab title="Tirette">
Installation du programme de la tirette, il sert à détécter si la tirette est retier ou est en place.

````Bash
git clone https://github.com/WiringPi/WiringPi.git
cd WiringPi
./build debian
mv debian-template/wiringpi_3.2_arm64.deb .
sudo apt install ./wiringpi_3.2_arm64.deb
cd ..
git clone https://github.com/modelec/tirette.git
cd tirette
g++ main.cpp MyClient.cpp MyClient.h -o tirette -l wiringPi -l TCPSocket
cd ../
````
{collapsible="true"}
</tab>
<tab title="Initialisation">
Installation du programme d'initialisation, il sert à l'initialisation des différents programme de Serge, ainsi qu'à verifier si les différents programmes fonctionnent toujours.

````Bash
git clone https://github.com/modelec/Initialisation.git
````
{collapsible="true"}
</tab>
</tabs>