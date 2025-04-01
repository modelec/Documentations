# Odometry Logic Processor
`<modelec/odometry_logic_processor.hpp>`

## Objectif
Le but de ce noeud est de traiter les données d'odométrie envoyées par le noeud de listener USB et de les publier sur le topic `odometry` pour être utilisées par d'autres noeuds.

### Topic
**[](Odometry-Listener-Serial-Topic.md)**
- [](Raw-Data-Topic.md) : reçoit les données brutes envoyées par le port série.
- [](Send-To-Serial-Topic.md) : envoie les données brutes au port série.

### Service
- [](Add-Serial-Listener-Service.md) : créer un nouveau listener USB pour l'odométrie.
