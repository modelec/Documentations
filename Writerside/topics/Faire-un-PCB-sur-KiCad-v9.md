# Faire un PCB sur KiCad v9

## Tips KiCad

### Glossaire

| Expression | Définition |
|------------|------------|
|            |            |

### Freeze KiCad
Cela peut arriver quand une fenetre de discussion est ouverte dans un autre outil KiCad (exemple freeze de l'outil de routage de PCB car une fenetre est ouvert dans l'outil d'éditeur d'empreinte)

### Raccourcis clavier
Passer de la couche du dessus à la couche du dessous : V (place aussi une via si on est en train de router une piste)

Remplir toutes les zones : B

Commencer à router une nouvelle piste : X

## Etapes de conception d'un PCB
Afin de gagner du temps, il est important de procéder par étapes.

1. Définition des besoins
2. Ecriture des spécifications
3. Choix des composants
4. Dessin du schéma
5. Routage de la carte

Les étapes 1 et 2 sont réalisées sans KiCad, en concertation avec les utilisateurs de la carte.

Les étapes 3 et 4 peuvent être un processus itératif

## Réaliser un PCB sur KiCad

### 1 - Définition des besoins
À faire en mode brainstorm sans vraiment de ligne directice.

Des questions qui peuvent être posées sont "Pourquoi faire ce PCB ?" "Quelle est la problématique à laquelle répondre ?" "Qu'est ce que ce PCB doit améliorer par rapport au fonctionnement antérieur ?"

Le but est de dégager la raison d'être de la carte qui permettra d'orienter les spécifications.

Attention à ne pas tomber dans le piège de la solution "magique" qui fait tout : il faut réfléchir un peu comme en programmation : un PCB est un "bloc" qui remplit une fonction précise avec des entrées et des sorties, comme une fonction.

### 2 - Ecriture des spécifications
Définir précisément les entrées et sorties, les connecteurs à utiliser, leur tension, le protocole s'il y en a un. 

Définir le format de la carte, la largeur et longueur maximales s'il y en a.

Définir précisément les fonctions qui doivent être implémentées.

Définir tout ce qui doit être écrit : on doit pouvoir tout savoir du PCB en lisant les spécifications, sauf les composants qui sont dessus (boîte noire). Cela servira aussi de documentation pour ceux qui devront l'utiliser par la suite.

### 3 - Choix des composants
L'objectif de cette étape est de sélectionner les composants à mettre sur le PCB pour répondre à nos besoins. Ceci doit permettre de connaître les entrées et sorties du composant et de récupérer son schéma et son empreinte.

Conseil perso : utiliser le moteur de recherche de composants du site Digikey qui permet d'avoir un bon nombre de paramètres.

Sélectionner le composant en filtrant parmis les caractéristiques (tension/courant acceptable, fréquence si applicable, etc.). Toujours laisser de la marge (typiquement +10% sur tension/courant max par rapport au maximum prévu sur la carte)

Vérifier si un composant équivalent n'est pas déjà en stock chez Modelec

Faire attention aux formats/boitiers des composants : peuvent ils être soudés à la main (pas de pad à souder sous le composant, invisible une fois le composant posé) ? Si ce n'est pas le cas est ce que l'achat du pochoir (stencil) a été prise en compte dans le budget ? Est ce que les composants à souder au four avec le stencil seront tous bien du même côté de la carte ?
### 4 - Dessin du schéma
#### 4.1 - Initialiser le projet
##### 4.1.1 - Créer un projet KiCad
Ouvrir KiCad 8 ou 9 et cliquer sur "Nouveau Projet", après avoir choisi l'emplacement, ceci va générer 3 fichiers : 
- .kikad_pro : le fichier du projet
- .kicad_sch : la page principale du schéma électrique du PCB
- .kicad_pcb : le fichier du routage du pcb
##### 4.1.2 - Importer la librairie Modelec
Pour importer la librairie Modelec dans un nouveau projet, il faut la récupérer depuis le repo https://github.com/modelec/pcbs_modelec.

Utiliser l'outil éditeur de symbole depuis la page d'accueil du projet ou la page schéma. 

Faire Fichier -> Ajouter librairie -> Projet -> Sélectionner le fichier Modelec.kicad_sym dans le dossier Lib_modelec.

Attention : par défaut kicad génère un lien absolu propre à la machine vers la librairie. Pour passer en lien relatif il faut éditer manuellement le fichier qui a été généré sous le nom de "sym-lib-table" et remplacer l'uri par "${KIPRJMOD}/../Lib_modelec/Modelec.kicad_sym".

Pour relier la librairie Modelec d'empreintes au projet, la démarche est la même avec l'outil éditeur d'empreinte, le dossier de librairie Modelec.pretty et le fichier de lien "fp-lib-table" dont l'uri doit être remplacée par "${KIPRJMOD}/../Lib_modelec/Modelec.pretty".
##### 4.1.3 - Ajouter des schémas de composants dans la librairie
Pour ajouter un nouveau composant à un projet il faut télécharger son schéma, son empreinte et idéalement son modèle 3D. Ceux-ci sont souvent disponibles sur les sites distributeurs (Digikey) ou sur le site du fabricant. Il faut les télécharger en KiCad v6+ et en STEP.

Ensuite ajouter les fichiers dans Lib_modelec pour les partager avec les autres utilisateurs.

Pour l'importation d'un symbole, utiliser l'éditeur de symbole, cliquer sur la librairie Modelec pour la sélectionner puis faire Fichier -> Importer -> Symbole -> Sélectionner le fichier qui vient d'être téléchargé.

Penser à modifier la description et le nom si nécessaire ainsi que d'ajouter le lien vers la datasheet du composant.

Pour les empreintes, la démarche est la même avec l'outil éditeur d'empreinte.

Pour ajouter un modèle 3D à une empreinte il faut double cliquer dans l'espace de dessin puis dans modèles 3D ajouter le fichier STEP et le positionner correctement.

Attention : il restera à faire le lien entre symbole et empreinte avec l'outil d'assignation d'empreinte.
##### 4.2 - Organiser les feuilles de dessin
Pour bien se retrouver sur la feuille de dessin il y a certaines bonnes pratiques à adopter.

Sur la feuille principale on essayera de mettre les entrées à gauche et les sorties à droite.

Sur la feuille principale on utilisera des feuilles hiérarchiques par "bloc" fonctionnel (sauf petit projet)

Sur les feuilles hiérarchiques on pourra encadrer les zones en fonction de leur fonction précise en ajoutant un texte pour préciser la fonction.

Pour transmettre des signaux d'une feuille hiérarchique "fille" à une feuille "mère", on place d'abord sur la fiche fille des Labels hiérarchiques. Le sens sélectionné par l'utilisateur ne sert qu'à l'affichage. Pour retrouver ces labels hiérarchiques sur la feuille mère, on utilise Synchroniser des pins de feuilles sur KiCad v9 ou Importer des pins de hiérarchie sur les versions précédentes (ensuite pour ces versions il faut cliquer dans le rectangle représentant la feuille fille pour placer chaque pin)
##### 4.3 - Tracer le schéma électrique
Pour aider à la compréhension du schéma, on privilégiera l'usage des fils plutôt que de multiplier les labels. (Sauf pour l'alimentation VCC et GND qui doivent utiliser des symboles)

L'utilisation des labels locaux est recommandée pour nommer les connexions, ce qui aide à la compréhension du schéma et qui sera transféré également sur le routage.

Les labels globaux sont déconseillés afin de conserver des connexions "visuelle" et éviter les erreurs.

On peut utiliser, sans en abuser, des bus KiCad pour les bus de données (par exemple SPI, I2C etc.) Pour faire passer des bus entre feuilles hiérarchiques, il existe un "tricks" présenté sur cette vidéo : https://youtu.be/_ZjyeltLMAg?t=687&si=xIgSqymeUtmvE5yl
### 5 - Routage de la carte
#### 5.1 - Initialiser les paramètres
##### 5.1.1 - Classes d'équipot
##### 5.1.2 - Réglages DRC
#### 5.2 - Placer les composants
