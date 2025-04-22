# Modelec package
`modelec_core`

## Pourquoi ROS2 sur Marcel ?

### 2024
En 2024, le robot [Serge](Serge.md) n'utilisait pas ROS2 ni aucun framework de robotique. Il était programmé en C++, mais il n'y avait pas de structure de code particulière. Le code était divisé en plusieurs fichiers, mais il n'y avait pas de séparation claire entre les différentes parties du code. Le code était difficile à lire et à comprendre, ce qui rendait la maintenance et l'ajout de nouvelles fonctionnalités difficiles.


#### Avantages du vanilla c++
- Facilité de compréhension : Le code est plus facile à comprendre pour les personnes qui ne connaissent pas ROS2.
- Pas de dépendances : Le code n'a pas besoin de dépendances externes, ce qui le rend plus léger et plus facile à déployer.
- Pas de surcoût : Le code n'a pas besoin de ressources supplémentaires pour fonctionner, ce qui le rend plus rapide et plus efficace.
- Pas de complexité : Le code est plus simple et plus facile à comprendre, ce qui le rend plus facile à maintenir et à déboguer.

#### Inconvenients
- Pas de modularité : Le code n'est pas modulaire, ce qui rend difficile l'ajout de nouvelles fonctionnalités.
- Pas de réutilisabilité : Le code n'est pas réutilisable, ce qui rend difficile l'utilisation de bibliothèques externes.
- Pas de standardisation : Le code n'est pas standardisé, ce qui rend difficile la compréhension du code par d'autres personnes.
- Pas de documentation : Le code n'est pas documenté, ce qui rend difficile la compréhension du code par d'autres personnes.

### Conclusion
En 2024, le robot Serge n'utilisait pas ROS2 ni aucun framework de robotique. Le code était écrit en C++ sans structure particulière, ce qui le rendait difficile à lire et à maintenir. Bien que cela ait des avantages en termes de simplicité et de légèreté, cela a également entraîné des inconvénients majeurs tels que le manque de modularité, de réutilisabilité et de documentation. En conséquence, il était difficile d'ajouter de nouvelles fonctionnalités ou de comprendre le code par d'autres personnes.
C'est pourquoi en 2025 le club Modelec a décidé de passer à ROS2 après avoir étudié son potentiel et ses avantages par rapport à la programmation en C++ sans structure particulière. Le passage à ROS2 a permis de structurer le code, de le rendre plus modulaire et réutilisable, et de faciliter la compréhension et la maintenance du code. De plus, ROS2 offre de nombreuses bibliothèques et outils qui facilitent le développement de logiciels pour robots, ce qui a permis au club Modelec de se concentrer sur l'implémentation de nouvelles fonctionnalités plutôt que sur la gestion du code.

> À partir de maintenant, nous allons plonger à l'intérieur de l'infrastructure ROS2 et de son fonctionnement.
> Il est donc indispensable d'avoir des bases en ROS2 pour comprendre la suite.
> Si vous ne connaissez pas ROS2, il est fortement recommandé de lire la documentation officielle ou de suivre un tutoriel d'introduction avant de continuer.
{style="warning"}