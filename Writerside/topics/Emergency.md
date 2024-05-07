# Emergency

## Description rapide
Ce programme a pour but d'amener le robot à sa position finale (stocker dans un fichier) en cas de crash d'un des programmes.

## Description détaillée du code
Ces définitions contiennent les paramètres de notre liaison série.
```C++
#define SERIAL_PORT "/dev/USB_ARDUINO"
#define MAX_MESSAGE_LEN 1048
#define BAUDS 115200 //vitesse des données (bit/sec)
```

Cette fonction sert à initialiser la liaison série entre l'arduino et la raspberry pi en utilisant les paramètres définis.
```C++
serialib init_serial(){
    serialib serial;
    char errorOpening = serial.openDevice(SERIAL_PORT, BAUDS);
    if (errorOpening!=1) exit(errorOpening);
    return serial;
}
```

Le code suivant sert à transmettre la position à laquelle aller à l'arduino qui elle va par la suite faire se déplacer
le robot à la dite position. Enfin, on va écrire dans la console le code renvoyé par l'arduino afin de vérifier qu'il
ne soit pas égale à -1.
```C++
std::string filePath;

if (argc == 2) {
    filePath = argv[1];
} else {
    return 0;
}

std::ifstream file;
file.open(filePath);
std::string line;
getline(file, line);

serialib serial = init_serial();

char myString[MAX_MESSAGE_LEN] = {0};

std::string toSend = "G " + line + "\n";
strcpy(myString, toSend.c_str());
myString[strlen(myString)] = '\0';

int errorCode = serial.writeBytes(toSend.c_str(), toSend.length());

if(errorCode == -1){
    std::cerr << "Error while sending data" << std::endl;
}
else {
    std::cout << "Data sent: " << errorCode << std::endl;
}

serial.closeDevice();
file.close();
```