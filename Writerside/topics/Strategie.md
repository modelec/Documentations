# Strategie

## Description rapide

La strategie de notre robot est stocké dans le programe TCPSocketServer aka le server tcp qui recoit les requetes des differents client.  
La strategie est divisé en plusieurs étape clé :
```C++
enum StratPattern {
    TURN_SOLAR_PANNEL_1,
    TURN_SOLAR_PANNEL_2,
    TURN_SOLAR_PANNEL_3,
    TAKE_FLOWER_BOTTOM,
    TAKE_FLOWER_TOP,
    DROP_FLOWER,
    GO_END,
};
```
Ces étapes clé corresponde au differentes actions que le robot doit réaliser pour la coupe de france de robotique 2024.


Le programe contient un tableau avec ces differentes actions et un index qui pointe sur l'action en cours.  
```C++
 std::vector<StratPattern> stratPatterns = {
     TURN_SOLAR_PANNEL_1,
     TURN_SOLAR_PANNEL_2,
     TURN_SOLAR_PANNEL_3,
     TAKE_FLOWER_BOTTOM,
     TAKE_FLOWER_BOTTOM,
     TAKE_FLOWER_BOTTOM,
     DROP_FLOWER,
     TAKE_FLOWER_TOP,
     TAKE_FLOWER_TOP,
     TAKE_FLOWER_TOP,
     DROP_FLOWER,
     GO_END
 };

 // This is the index of the current pattern
 int whereAmI = 0;
```

Chaque actions correspond à une fonction qui est appelé par le server tcp.  
```C++
    /*
     * Start Strategy function
    */
    void goAndTurnSolarPannel(StratPattern sp);

    void findAndGoFlower(StratPattern sp);

    void goEnd();

    void dropFlowers();
    /*
     *  End Strategy function
     */
```

## Panneaux Solaires

Dans notre stratégie nous commencer par tourner trois panneaux solaires

Le but ici est de ce placer contre le bord de la tableau, le plus proche possible pour pouvoir toucher le panneau solaire avec l'actionneur tout en gardant de la marge pour que le robot puissent encore tourner

Les panneau solaire possèdes des tag Aruco qui permettent de savoir leur possition et leur rotation mais dans notre cas nous avons décidé de ne pas les utiliser pour des raisons de simplicité et de rapidité et du fait que nous connaisons leur position exact.

Le code pour tourner un panneau solaire est le suivant :

```C++
this->go(x, y);
awaitRobotIdle();

this->rotate(PI / 2);
awaitRobotIdle();

this->checkPanneau(servo_moteur);
usleep(100'000);

this->go(x+130, y);
awaitRobotIdle();

this->uncheckPanneau(servo_moteur);
```

Le but est de ce placer a coter du panneau solaire pour le tourner et ensuite avancé un peu pour replier l'actionneur.

## Fleur

En fonction de notre équipe nous allons utilisé deux zones fixes ou nous allons chercher des plantes.

Celle-ci sont, pour l'équipe bleu : 
 - 1000 1300
 - 1000 700

Et pour l'équipe jaune :
 - 2000 1300
 - 2000 700

Nous allons detecter les tag aruco present au alentours de la zone voulue.

le programe va réalisé 5 scan de la zone et checher le tag qui reviens le plus pour eviter les faux positif.

Le code pour chercher une fleur est le suivant :

```C++
 this->arucoTags.clear();
 this->broadcastMessage("strat;aruco;get aruco;1\n");
 for (int i = 0; i < 5; i++) {
     if (stopEmergency) std::terminate();

     usleep(200'000);
     this->broadcastMessage("strat;aruco;get aruco;1\n");
 }
 usleep(100'000);

 std::optional<ArucoTag> tag = getBiggestArucoTag(300, 700, -200, 200);

 if (tag.has_value()) {
     if (pinceState[1] == NONE) {
         goToAruco(tag.value(), 1);
     } else if (pinceState[2] == NONE) {
         goToAruco(tag.value(), 2);
     } else if (pinceState[0] == NONE) {
         goToAruco(tag.value(), 0);
     }
 }
```

Ensuite la fonction goTaAruco va aller a la position de la plante pour la recuperer.

```C++
void TCPServer::goToAruco(const ArucoTag &arucoTag, const int pince) {
    double robotPosX = this->robotPose.pos.x;
    double robotPosY = this->robotPose.pos.y;
    double theta = this->robotPose.theta;
    double decalage;
    double rotate;
    if (pince < 0 || pince > 2) {
        return;
    }

    switch (pince) {
        case 0:
            decalage = 60;
            rotate = -0.07;
            break;
        case 1:
            decalage = 0;
            rotate = 0;
            break;
        case 2:
            decalage = -60;
            rotate = 0.07;
            break;
        default:
            decalage = 0;
            rotate = 0;
            break;
    }

    this->baisserBras();
    this->openPince(pince);

    double xPrime = arucoTag.pos()[0];
    double yPrime = arucoTag.pos()[1];
    double roll = arucoTag.rot()[1];

    auto centerPlantX = (20 * std::cos(roll)) + xPrime/* - 50*/;
    auto centerPlantY = (-20 * std::sin(roll)) + yPrime + decalage;

    double thetaPrime = std::atan2(centerPlantY, centerPlantX);

    this->rotate(this->robotPose.theta + rotate - thetaPrime);
    awaitRobotIdle();

    double robotPosForPotX = (centerPlantX * std::cos(theta) + centerPlantY * std::sin(theta)) + robotPosX;
    double robotPosForPotY = (-centerPlantX * std::sin(theta) + centerPlantY * std::cos(theta)) + robotPosY;

    int previousSpeed = this->speed;

    this->transit(robotPosForPotX, robotPosForPotY, 130);
    awaitRobotIdle();

    this->closePince(pince);
    usleep(500'000);
    this->setSpeed(previousSpeed);
    pinceState[pince] = TCPUtils::startWith(arucoTag.name(), "Purple_flower") ? PURPLE_FLOWER : WHITE_FLOWER;
}
```

Ici le code va prendre en compte dans quelle pince nous voulons mettre la plante et va ajuster la position de la plante en fonction de la position du robot.

A savoir que le le programe pour trouver les tag arcuo nous renvoie la position du TAG pas de la plantes, celui-ci est placer tout autour de la plantes a 20mm du bord.

Dans un premier temps, ces 20mm sont rajouter et ensuite un changement de repere est effectuer pour que le robot puisse ce deplacer en fonction de la position de la plante.

## Fin de partie

Lorsque que nous commencont la partie nous evons choisir le spawn du robot, il existe 6 zone distinct sur le robot sur laquelle on peut faire partir notre robot, 3 par équipe.

La zone d'arrivé du robot doit être l'une des deux zones restante.

C'est pourquoi nous connaisont cette valeur et nous pouvons donc nous deplacer directement a la fin de la partie.

## Robot adverse trop proche

Nous avons pour obligation de ne pas toucher le robot adverse, pour cela nous avons mis en place un systeme de detection de la distance entre les deux robots grace a un lidar.

Pour cela, lorsque le lidar va detecter un adversaire il vas envoyé un message `stop proximity` avec l'angle et la distance au robot adverse.

Grace a cela nous pouvons dans un premier temps stopper notre robot et si le robot adversaire ne bouge pas, nous decaler dans le sens opposé.

Ensuite nous pouvons reprendre notre stratégie.