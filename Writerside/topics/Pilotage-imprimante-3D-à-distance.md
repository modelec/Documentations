# Pilotage imprimante 3D à distance

### Prérequis

1. Créer un compte Tailscale
2. Enregistrer votre PC sur tailscale
3. [Installer le client Tailscale](https://tailscale.com/kb/1347/installation)
4. Se connecter à Tailscale depuis votre PC

<tabs>
<tab title="Linux">

```Bash
sudo tailscale login
```
</tab>
<tab title="Windows">
Sur la droite de la barre d'état dans les onglets cachés, cliquer sur Tailscale et se connecter à son compte.
</tab>
</tabs>

5. Demander à un administrateur (Félix Marquet) de vous donner accès aux machines Modelec depuis votre Tailscale.

<tabs>
<tab title="Linux">

```Bash
sudo tailscale status
```

Tailscale status devrait afficher l'ip des machines connectées au Tailscale. Le nom de la raspi qui pilote l'imprimante est "Octopi" son IP par défaut est 100.81.139.14. Ce paramètre est modifiable.

</tab>
<tab title="Windows">
Sur la droite de la barre d'état dans les onglets cachés, cliquer sur Tailscale et depuis votre compte accéder à la console admin.
Dans la console admin sont listées les machines sur votre réseau Tailscale. Le nom de la raspi qui pilote l'imprimante est "Octopi" son IP par défaut est 100.81.139.14. Ce paramètre est modifiable.
</tab>
</tabs>

### Accès

Dans un navigateur, ouvrir la page web à l'IP de la machine Octopi. Il est recommandé de mettre cette adresse en favori.

Sur la page de connection, se connecter avec l'identifiant "modelec" et le même mot de passe que pour les autres machines Modelec.

### Utilisation

Avant utilisation vérifier la bonne connection de l'imprimante à la raspi dans les espaces "Connection" et "State" sur la gauche de l'interface.

Si l'imprimante est déconnectée, la faire se reconnecter avec les paramètres par défaut.

Dans "Files", toujours sur la gauche se trouve la liste des fichiers imprimés récemment. Il est possible d'importer un fichier depuis votre PC avec les boutons "Upload" ou "Upload to SD".

Une fois le fichier importé, lancer l'impression en cliquant sur l'icone d'imprimante "Load and Print". Si cela ne marche pas, déconnecter puis reconnecter l'imprimante dans "Connection".

Si cela fonctionne, le "State" devrait passer en printing et les jauges de températures afficher des consignes. Les consignes Tool et Bed peuvent arriver l'une après l'autre, pas de panique s'il y en a qu'une seule au début.

Il est possible d'accéder à la vidéo en direct dans l'onglet "Control" et de récupérer les timelapses dans l'onglet "Timelapse" en triant par date la plus récente.