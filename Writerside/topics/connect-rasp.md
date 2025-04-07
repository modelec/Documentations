# Connect To Raspberry

## Se connecter a la raspberry avec ssh sans connaissance de l'IP

Utilisation de tailscale pour se connecter à la raspberry sans connaitre son IP.

### Installation

[Télécharger le client tailscale](https://tailscale.com/kb/1347/installation)

### Usage

1. Créer un compte sur tailscale
2. Enregistrer votre appareil
3. Installer le client tailscale sur votre appareil
4. Lancer les commandes suivantes

```Bash
sudo tailscale login
```

Maintenant demandé à un admin de vous donner l'accès à la raspberry.

```Bash
sudo tailscale status
```

Avec la commande `tailscale status` vous avez l'IP de la raspberry.

```Bash
ssh modelec@<IP>
```

Demander à un admin de vous donner le mot de passe.