# Multiple Serial Listener
`<modelec/multiple_serial_listener.hpp>`

## Objectif
Un listener pour plusieurs ports série.

Le but de ce nœud est de permettre la communication avec plusieurs ports série en même temps. Il est configuré pour écouter les données sur plusieurs ports et les publier sur des topics ROS2 distincts. Cela permet de gérer plusieurs périphériques série simultanément sans avoir à créer un nœud séparé pour chaque port.

### Topic
Ce nœud écoute et publie sur les topics suivants (un pour chaque port série) :
- [](Raw-Data-Topic.md) : recup les informations brutes envoyées par le port série et les transmet au travers du topic.
- [](Send-To-Serial-Topic.md) : envoie les données brutes au port série.

### Service
Le noeud expose un service pour setup un port série :
- [](AddSerialListener-Service-Interface.md)