# ROS2 avec JetBrain (pour windows)
Pour les personnes utilisant un IDE JetBrain sur Windows, mais avec une installation ROS2 sur WLS, voici comment load le projet sur JetBrain.
>Test Effectué avec CLion

## Requis
- Avoir installé WSL avec une distribution Linux (Ubuntu 20.04 ou 22.04 recommandés)
- Avoir installé un editeur JetBrain (CLion préféré, car nous développons principalement en C++)
- Avoir installé ROS2 sur WSL (voir [ici](ROS2-Installation.md#installation-sur-wsl))

## 1. Ouvrir le projet
- Ouvrir CLion
- Si vous êtes dans un projet aller dans File > Close Project
- Ensuite aller dans Remote Development > WSL
- Connecter vous ensuite a votre distribution WSL via le menu
- Puis ouvrir le dossier de votre projet ROS2 (cela peut être un peu long, car JetBrain va installer un serveur sur WSL)
- Et pouf, vous avez votre projet ROS2 sur JetBrain

## 2. Configurer le projet
- Dans le terminal de votre WSL, execute les commandes suivante :
```bash
source /opt/ros/jazzy/setup.bash
colcon build --cmake-args -DCMAKE_EXPORT_COMPILE_COMMANDS=1
```
- Ensuite cela devrait avoir crée un dossier `build` dans votre projet
- Dans ce dossier build devrait être présent un fichier `compile_commands.json`
- Faite clique droit sur ce fichier et selectionner `Load Compilation Database Project`
- Si tout c'est bien passé, votre projet devrais maintenant être configuré avec ROS2 sur JetBrain !
- Pour tester, vous pouvez essayer de faire un `Ctrl + Click` sur une fonction de ROS2 et cela devrais vous amener a la déclaration de la fonction.
