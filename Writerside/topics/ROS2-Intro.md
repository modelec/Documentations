# Intro

#### Intro by ChatGPT
ROS 2 (Robot Operating System 2) est un framework open-source conçu pour le développement de logiciels pour robots. C'est une évolution de ROS 1, améliorée pour mieux répondre aux exigences des systèmes robotiques modernes, notamment en matière de fiabilité, de performances et de compatibilité avec les environnements embarqués et temps réel.

##### Caractéristiques principales de ROS 2 :
- Architecture distribuée : Les différents composants d'un robot (capteurs, actionneurs, algorithmes, etc.) communiquent via un système de messages asynchrones.
- Middleware DDS : ROS 2 repose sur DDS (Data Distribution Service), un standard permettant une communication robuste et adaptable aux réseaux variés.
- Support multi-plateforme : Compatible avec Linux, Windows, macOS et même des systèmes embarqués.
- Gestion améliorée du temps réel : Permet un meilleur contrôle des latences, essentiel pour les robots nécessitant des réactions précises.
- Modularité et scalabilité : Facilite le développement de robots complexes en permettant d'ajouter ou de modifier des composants indépendamment.

##### Composants clés :
- Nœuds : Petits programmes qui effectuent des tâches spécifiques.
- Topics : Canaux de communication permettant aux nœuds d’échanger des messages.
- Services : Communication synchrone entre nœuds (requête/réponse).
- Actions : Permettent l’exécution de tâches longues avec des mises à jour d’état.
- Paramètres : Variables configurables qui influencent le comportement des nœuds.

#### Exemples d'utilisation :
- Contrôle d’un bras robotique
- Navigation autonome d’un robot mobile
- Fusion de données issues de plusieurs capteurs
- Si tu veux commencer avec ROS 2, l’installation et la configuration initiale se font via Ubuntu (recommandé) et tu peux tester avec des packages comme turtlesim pour voir le fonctionnement des nœuds et topics en pratique.
