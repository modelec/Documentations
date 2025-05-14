# Pilotage PCB Actionneurs

## Informations que le PCB peut faire remonter
- Position des servomoteurs
- Position des moteurs pas à pas
- Etat des relais
- Information des capteurs fin de course
- Etat de la tirette
## Ordres envoyables au PCB
- Armer la tirette
- Désarmer la tirette
- Activer/désactiver le relai (qui alimente les solénoïdes)
- Faire tourner le servo vers un angle
## Protocole de communication
La communication se fait en USB CDC
### Récupération d'une donnée par la raspi :
GET;XXXX;YYYY\n avec XXXX l'élément du PCB concerné et YYYY la donnée demandée dans la liste suivante :
- ASC;POS pour récupérer la position de l'ascenseur ('low', 'climb', 'high', ou 'desc')
- SERVOn;POS pour récupérer la position du servo n (renvoie le numéro de position prédéfini par l'utilisateur (le x de POSx dans la commande SET))
- RELAYn;STATE pour récupérer l'état d'un relai (1 = activé, 0 = désactivé) avec n l'id du relai (1, 2 ou 3)
### Réponse du PCB à une demande de donnée
SET;XXXX;YYYY;val avec XXXX et YYYY identiques à la commande GET et val une valeur dans l'unité ou la plage de valeurs convenue.
### Modification d'une constante par la raspi :
SET;XXXX;YYYY;val avec XXXX l'élément du PCB concerné, YYYY la donnée à enregistrer et val la valeur dans la liste suivante :
- ASC;HIGH;val (valeur en mm de hauteur de la position haute de l'ascenseur)
- SERVOn;POSx;angle (valeur de l'angle de la position d'un servo moteur en radians avec n et x des nombres (id du servo et de la pos de ce servo))
### Réponse du PCB à la modif d'une constante
OK;XXXX;YYYY;val avec XXXX, YYYY et val identiques à la commande SET pour valider une commande effectuée.
KO;XXXX;YYYY;val pour une commande échouée
### Déclenchement d'une action par la rasp
MOV;XXX;YYY
- ASC;HIGH pour mettre l'ascenseur à l'étage haut
- ASC;LOW pour mettre l'ascenseur à l'étage bas
- SERVOn;POSx pour mettre le servo n à la position x
- RELAY;x avec x vaut 1 ou 0 pour activer ou désactiver des sorties
### Réponse du PCB au déclenchement d'une action
OK;XXXX;YYYY avec XXXX et YYYY identiques à la commande MOV pour valider une commande effectuée.
KO;XXXX;YYYY pour une commande échouée