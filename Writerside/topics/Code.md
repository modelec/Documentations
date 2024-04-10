# Code

## Installation des dépendances
lxqt est necessaire car il install des lib manquantes pour l'ihm

```BASH
sudo apt install build-essential cmake gcc libopencv-dev qt6-base-dev qt6-base-dev-tools lxqt-core qt6-wayland libcamera-dev
mkdir Serge && cd Serge
chmod 700 /run/user/1000
```

````Bash
crontab -e
@reboot chmod 700 /run/user/1000
````

## Installation du client TCP
```BASH
git clone https://github.com/modelec/TCPSocketClient.git
cd TCPSocketClient/
mkdir build && cd build
cmake ..
sudo make install
cd ../..
echo 'export LD_LIBRARY_PATH=:/usr/local/lib64:/usr/local/lib' >> ~/.bashrc
```

## Installation du serveur TCP
```BASH
git clone https://github.com/modelec/TCPSocketServer.git
cd TCPSocketServer/
mkdir build && cd build
cmake ..
make
cd ../..
```

## Installtion de la détection de l'adversaire
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

## Installation du programme de contrôle des servo-moteurs
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

## Installtion de l'IHM
````Bash
git clone https://github.com/modelec/ihm.git
cd ihm
mkdir build && cd build
cmake ..
make
cd ../..
````

## Installation du connecteur raspi -> arduino
````Bash
git clone https://github.com/modelec/connectors.git -b tcp
cd connectors/
mkdir build && cd build
cmake ..
make
cd ../..
````

## Installtion du programme de détection des pots et des panneaux solaires
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

## Installation du programme de la tirette
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

## Installation du programme d'initialisation
````Bash
git clone https://github.com/modelec/Initialisation.git
````