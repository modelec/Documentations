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
## Evenements envoyables à la raspi
- Activation de la tirette si armée
- Appui sur un bouton
- Activation d'un capteur
## Protocole de communication
La communication se fait en USB CDC
### Récupération d'une donnée par la raspi :
GET;XXXX;YYYY\n avec XXXX l'élément du PCB concerné et YYYY la donnée demandée dans la liste suivante :
- ASC;POS pour récupérer la position de l'ascenseur (renvoie le numéro de position prédéfini par l'utilisateur (le x de POSx dans la commande SET))
- SERVOn;POS pour récupérer la position du servo n (renvoie le numéro de position prédéfini par l'utilisateur (le x de POSx dans la commande SET))
- RELAYn;STATE pour récupérer l'état d'un relai (1 = activé, 0 = désactivé) avec n l'id du relai (1, 2 ou 3)
### Réponse du PCB à une demande de donnée
SET;XXXX;YYYY;val avec XXXX et YYYY identiques à la commande GET et val une valeur dans l'unité ou la plage de valeurs convenue.
### Modification d'une constante par la raspi :
SET;XXXX;YYYY;val avec XXXX l'élément du PCB concerné, YYYY la donnée à enregistrer et val la valeur dans la liste suivante :
- ASC;POSx;val (valeur en mm de hauteur de la position haute de l'ascenseur)
- SERVOn;POSx;angle (valeur de l'angle de la position d'un servo moteur en radians avec n et x des nombres (id du servo et de la pos de ce servo))
- SET;TIR;ARM;val (1 pour armer la tirette si le robot est prêt, 0 pour désarmer la tirette)
### Réponse du PCB à la modif d'une constante
OK;XXXX;YYYY;val avec XXXX, YYYY et val identiques à la commande SET pour valider une commande effectuée.
KO;XXXX;YYYY;val pour une commande échouée
### Déclenchement d'une action par la rasp
MOV;XXX;YYY
- ASC;POSx pour mettre l'ascenseur à la position x
- SERVOn;POSx pour mettre le servo n à la position x
- RELAYn;x avec x vaut 1 ou 0 pour activer ou désactiver des sorties
### Réponse du PCB au déclenchement d'une action
OK;XXXX;YYYY avec XXXX et YYYY identiques à la commande MOV pour valider une commande effectuée.
KO;XXXX;YYYY pour une commande échouée
### Envoi d'évènement par le PCB
Le PCB peut envoyer des informations à la rasp sans répondre à l'une de ses requêtes de la sorte :
EVENT;XXX;YYY avec XXX l'évènement et YYY une info complémentaire
- TIR;START pour une tirette armée actionnée par l'utilisateur
- TIR;ARM pour signaler un appui bouton sur le panneau de commande demandant l'armement de la tirette
- TIR;DIS pour signaler un appui bouton sur le panneau de commande et le désarmement de la tirette
### Réponse de la rasp à un évènement du PCB
Si la rasp ne répond pas à l'envoi d'un évènement par le PCB celui ci sera renvoyé jusqu'à recevoir une réponse
- OK;XXX;YYY pour un message pris en compte par la rasp, XXX et YYY identiques au message EVENT correspondant
- rien sinon