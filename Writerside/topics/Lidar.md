# Lidar

## Matériel et montage
{collapsible="true" default-state="expanded"}

### Lidar

Le lidar utilisé est un Lidar A1M8 de Slamtec. Il est capable de déterminer des distances comprises entre 0,15 et 12m à une précision de 0,5mm et des angles compris entre 0 et 360° à une précision de 1°.

La fréquence en tours est de 5,5Hz soit un scan toutes les 0,18s

### Fixation

Le Lidar est placé en hauteur de sorte à ne pas détecter les PAMI et éléments de jeu. Il est fixé de manière précise, son centre de rotation sur l'axe de rotation du robot, de sorte à avoir un seul et même point sur le robot dont la position est calculée pour l'odométrie et le lidar.

## Fonctionnement du code
{collapsible="true" default-state="expanded"}

### Prérequis

Le programme de contrôle du Lidar nécessite d'avoir préalablement installé le SDK slamtec rplidar_sdk depuis Github.

Le programme de contrôle du Lidar nécessite d'avoir préalablement installé la librairie Modelec TCPSocketClient

Une erreur Segmentation Fault est générée si le code est lancé sans avoir branché le Lidar.

Une fois le code lancé, il est nécessaire de donner au code du lidar la position du robot en passant par des messages TCP.

### Protocole de communication

| Emetteur | Destinataire       | Verbe            | Données     | Réaction du système                                                                                                 |
|----------|--------------------|------------------|-------------|---------------------------------------------------------------------------------------------------------------------|
| Tous     | lidar ou all       | ping             |             | réponse: lidar;émetteur;pong;                                                                                       |
| Tous     | lidar ou all       | get data         |             | réponse: lidar;émetteur;set avoidance;x,y,radius                                                                    |
| Tous     | lidar ou all       | get health       |             | réponse: lidar;émetteur;set health;1 ou 0                                                                           |
| Tous     | lidar ou all       | start            |             | Démarrage du moteur et du laser. Début des calculs d'évitement et de triangulation                                  |
| Tous     | lidar ou all       | stop             |             | Arrêt du moteur, du laser et des calculs                                                                            |
| Tous     | lidar ou all       | set pos          | x, y, alpha | Mise à jour de la position du robot dans le programme du lidar                                                      |
| Tous     | lidar ou all       | set team         | 1 ou 0      | Mise à jour de la position des balises de triangulation dans le programme du lidar (1 = jaune, 0 = bleu)            |
| Tous     | lidar ou all       | set beacon       | 1 ou 0      | Indique au robot si les balises ont été installées ou non 1 = balises, 0 = pas de balises                           |
| Tous     | lidar              | get pos          |             | Passe le lidar en mode triangulation **attention** voir doc du mode triangulation                                   |
| lidar    | all                | stop proximity   | dist, angle | Alerte en cas de proximité directe. Dist en mm et angle en cent. de rad. dans la base du robot (0 = avant du robot) |
| lidar    | émetteur précédent | set pos          | x, y, alpha | Renvoie les résultats calculés en mode triangulation                                                                |
| lidar    | all                | stop recalibrate | décalage    | Indique que la valeur de position calculée par l'odométrie est trop éloignée de celle calculée par triangulation    |

### Alertes de proximité

Si un obstacle est détecté trop proche du robot, une alerte est envoyée en TCP à "all" sous la forme :

lidar;all;stop proximity;distance,angle

La distance est en mm et l'angle en centièmes de radians

### Position de l'adversaire

Une fois le message start reçu, le lidar passe en mode détection de l'adversaire.

Dans ce mode de détection, les données récoltées par le capteur laser sont analysées après chaque tour afin de déterminer la position approximative et lidar et du robot adverse.

La position du robot adverse est estimée et n'est pas précise. Le but est de déterminer une zone à éviter.

Procédé : 

- Suppression des points à l'extérieur de la carte à partir de la dernière position du robot reçue
- Suppression des points solitaires considérés comme de fausses détections
- Rangement des points détectés par amas
- Calcul du centre de gravité de chaque amas (position moyenne des points)
- Si plusieurs amas, sélection de l'amas le plus probable comme étant le plus proche de la dernière position connue de l'adversaire
- Conservation du centre de gravité de l'amas et de l'écart max entre deux points au sein de l'amas comme le centre et le rayon de la zone à éviter.
- L'ajout d'une distance de sécurité est à faire dans le code de stratégie

Récupération des données : 

Pour récupérer ces données, il faut envoyer le message TCP emetteur;lidar;get data;

Le message renvoyé est le suivant : lidar;emetteur;set avoidance;x_centre,y_centre,rayon

### Triangulation

Le code du lidar permet d'entrer dans un mode triangulation afin de déterminer sur plusieurs tours de lidar la position et orientation précise du robot.

**Attention** Dans le mode triangulation, le lidar 
- Cesse de calculer la position de l'adversaire
- Estime que le robot est complètement à l'arrêt durant toute la durée de calcul

Procédé :
- Le lidar récupère les données pour le nombre de tours configurés
- Les données sont rangées par amas
- A partir de la précédente position estimée du robot, les amas correspondant aux 2 ou 3 balises visibles sont identifiés
- Sur ces amas, le point détecté le plus proche du robot est considéré comme étant au croisement du cercle de l'enveloppe extérieure de la balise et de la droite entre le robot et le centre de la balise (méthode à améliorer)
- Les cercles passant par le centre des balises et de rayons correspondant à la distance détectée + le rayon de la balise sont tracés
- Les points d'intersections des cercles sont déterminés (il y a 2 intersections entre 2 cercles)
- Les droites passant par les 2 points d'intersections de deux cercles sont tracées.
- Les points d'intersections des 2 ou 3 droites (en fonction de nombre de balises détectées) sont déterminés. Une moyenne est faite dans le cas avec 3 droites.
- Le point d'intersection ou la moyenne des points d'intersection est maintenant considérée comme étant la position du robot.
- Connaissant l'angle de lidar et donc par rapport au robot pour chaque balise détectée, on détermine l'orientation du robot comme étant la moyenne de l'orientation déterminée grâce à chaque balise.

Récupération des données :

A la fin du processus de calcul, le code du lidar envoie de lui même les résultats calculés. Il sort également tout seul du mode triangulation en même temps que cet envoi.

### Constantes réglables

Le fichier header localization.h contient un certain nombre de constantes dont les valeurs peuvent être modifiées pour optimiser la performance du programme.

| Nom                              | Modifiable | Effet sur le programme                                                                                    | Valeur type                                                     |
|----------------------------------|------------|-----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| NODES_LEN                        | NON        | Taille du tableau de points détectés à chaque tour                                                        | 8192                                                            |
| MAX_TABLE_X                      | OUI        | Longueur X de la table, à modifier seulement en test pour de petites tables                               | 3000 (Unité : mm)                                               |
| MAX_TABLE_Y                      | OUI        | Longueur Y de la table, à modifier seulement en test pour de petites tables                               | 2000 (Unité : mm)                                               |
| BEACON_DETECT_RANGE              | OUI        | Rayon du cercle à l'intérieur duquel un amas est considéré comme étant une balise                         | 100 (Unité : mm)                                                |
| PROXIMITY_ALERT_RANGE            | OUI        | Distance maximale en dessous de laquelle une alerte de proximité est lancée                               | 250 (Unité : mm)                                                |
| BORDER_DETECT_TRIGGER            | OUI        | Distance retirée aux bordures au moment de l'exclusion des points en dehors du terrain                    | 50 (Unité : mm)                                                 |
| AGGLOMERATES_TRIGGER             | OUI        | Distance entre deux points en dessous de laquelle ils sont considérés comme étant dans le même agglomérat | 250 (Unité : mm)                                                |
| BEACONS_RADIUS                   | OUI        | Rayon extérieur des balises                                                                               | 50 (Unité : mm)                                                 |
| TRIANGULATION_ROUNDS             | OUI        | Nombre de tours de lidar analysés en mode triangulation                                                   | 3                                                               |
| POSITION_CORRECT_RANGE           | OUI        | Décalage de position maximum acceptable avant envoi du message recalibrate                                | 25                                                              |
| YELLOW_TEAM_BEACONS_POS          | OUI        | Position des balises de l'équipe jaune                                                                    | {make_pair(3094,72), make_pair(3094,1928), make_pair(-94,1000)} |
| BLUE_TEAM_BEACONS_POS            | OUI        | Position des balises de l'équipe bleue                                                                    | {make_pair(-94,72), make_pair(-94,1928), make_pair(3094,1000)}  |
