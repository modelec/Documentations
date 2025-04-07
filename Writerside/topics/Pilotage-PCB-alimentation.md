# Pilotage PCB Alimentation

## Informations que le PCB peut faire remonter
- Etat du bouton d'arrêt d'urgence
- Mesure de courant/tension/puissance sur chaque sortie
- Mesure de température de la carte
- On peut imaginer de rendre les 3 précédentes configurables en envoi d'alerte si une valeur limite est dépassée ou si le BAU est appuyé
- Etat des transfos (5V/12V/24V) (allumé/éteint)
- Mesure de la tension/du courant des 2 batteries connectées et conversion vers taux de charge
- Entrée actuellement utilisée (alim externe / batterie 1 / batterie 2)
- Liste des entrées valides
## Ordres envoyables au PCB
- Activer/Désactiver des sorties (5V/12V/24V)
- Faire un arrêt d'urgence logiciel (même chose qu'arrêt d'urgence physique => arrêt immédiat du 5V, 12V et 24V)
- Configuration du buzzer (à définir : sur quels évènements on sonne ?)
- Configuration des GPIO (à définir : sur quels évènements on passe à l'état haut ou bas ?)
## Protocole de communication
La communication se fait en liaison série UART

Les mots de communication restent à définir mais un format qui peut être envisagé fonctionnerait de la sorte :

### Récupération d'une donnée par la raspi :
GET;XXXX;YYYY\n avec XXXX l'élément du PCB concerné et YYYY la donnée demandée dans la liste suivante :
- BAU;STATE pour l'état du bouton d'arrêt d'urgence (1 ou 0)
- INn;VOLT pour la tension d'entrée des entrées batteries (n vaut 1 ou 2) (En 10mV)
- INn;AMPS pour le courant d'entrée des entrées batteries (n vaut 1 ou 2) (En mA)
- INn;STATE pour l'état de l'entrée (active => entrée qui alimente la carte actuellement. Inactive sinon) (1 ou 0)
- INn;VALID pour la validité de l'entrée (une entrée peut être valide sans être active !). Valide si sa tension est correcte depuis suffisamment longtemps. (1 ou 0)
- TEMP;CELS pour la température de la carte (en dixième de celcius)
- OUT5V;STATE
- OUT5V;VOLT
- OUT5V;AMPS
- OUT5V1;YYYY
- OUT12V;YYYY
- OUT24V;YYYY
### Réponse du PCB à une demande de donnée
SET;XXXX;YYYY;val avec XXXX et YYYY identiques à la commande GET et val une valeur dans l'unité convenue.
### Envoi d'un ordre par la raspi :
SET;XXXX;YYYY;val avec XXXX l'élément du PCB concerné, YYYY la donnée à enregistrer et val la valeur dans la liste suivante :
- EMG;STATE;val avec val vaut 1 ou 0 pour activer ou désactiver un arrêt d'urgence soft
- OUT5V;STATE;val avec val vaut 1 ou 0 pour activer ou désactiver le 5V
- OUT12V;STATE;val avec val vaut 1 ou 0 pour activer ou désactiver le 12V
- OUT24V;STATE;val avec val vaut 1 ou 0 pour activer ou désactiver le 24V
### Réponse du PCB à un ordre
OK;XXXX;YYYY;val avec XXXX, YYYY et val identiques à la commande SET pour valider une commande effectuée.
KO;XXXX;YYYY;val pour une commande échouée