# Pilotage PCB Odométrie

## Informations que le PCB peut faire remonter
- Position du robot
- Vitesse instantanée du robot
- Valeurs des capteurs ToF
- Id du dernier point de passage atteint
## Ordres envoyables au PCB
- Modifier les coefficients des PIDs
- Liste de points de passages
- Arrêt/marche
## Protocole de communication
La communication se fait en liaison série UART

Les mots de communication restent à définir mais un format qui peut être envisagé fonctionnerait de la sorte :

### Récupération d'une donnée par la raspi :
- GET;POS
- GET;SPEED
- GET;DIST;N pour récupérer la distance mesurée par le ToF numéro N.
### Réponse du PCB à une demande de donnée
- SET;POS;xx;yy;tt pour renvoyer la position mesurée (x,y,angle) en mm et en radians.
- SET;SPEED;xx;yy;tt pour renvoyer la vitesse mesurée (x,y,angle) en mm².
- SET;DIST;N;xx pour renvoyer la distance mesurée par le ToF N en mm.
### Reset de la position par la raspi
- SET;POS;xx;yy;tt
### Envoi de la liste des points de passage par la raspi :
- SET;WAYPOINT;id;type;xx;yy;tt pour écraser le point de passage avec l'id renseigné. Type vaut 0 pour point de passage (en vitesse, peu précis), 1 pour un point d'arrivée (à l'arrêt, très précis)
### Réponse du PCB à un ordre (2 dernières commandes)
- OK;XXXX;YYYY;...; avec XXXX, YYYY, ... identiques à la commande SET pour valider une commande effectuée.
- KO;XXXX;YYYY;...; pour une commande échouée, ou pas de réponse
### Envoi de la position en direct au passage d'un waypoint par le PCB :
- SET;WAYPOINT;id avec l'id du waypoint atteint