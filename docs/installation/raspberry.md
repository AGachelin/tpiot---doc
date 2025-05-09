# Installer un Raspberry Pi

## SSH

SSH (_Secure Shell_) est un protocole permettant d’établir une connexion sécurisée à distance entre deux machines via un réseau, en chiffrant les communications. Il est principalement utilisé pour l’administration de serveurs et le transfert de fichiers de manière sécurisée.

Pour vous connecter au Raspberry Pi sans utiliser de périphériques, il faut utiliser SSH. Si la commande `ssh` renvoie un message sur l'utilisation de la commande alors SSH est déjà installé, sinon il faut l'installer.
```
>ssh
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface] [-b bind_address]
[-c cipher_spec] [-D [bind_address:]port] [-E log_file]
[-e escape_char] [-F configfile] [-I pkcs11] [-i identity_file]
[-J destination] [-L address] [-l login_name] [-m mac_spec]
[-O ctl_cmd] [-o option] [-P tag] [-p port] [-Q query_option]
[-R address] [-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]]
destination [command [argument ...]]
```
### Installer OpenSSH (Windows)
https://learn.microsoft.com/fr-fr/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui&pivots=windows-server-2025

### Installer SSH (Linux)
`sudo apt install openssh-client`

### Générer une paire de clefs

La paire de clés en cryptographie asymétrique (comme SSH) fonctionne comme un cadenas et une clé : la clé publique est comme un cadenas que tout le monde peut fermer (chiffrer un message), mais seule la clé privée, gardée secrète, peut l’ouvrir (déchiffrer le message).

Générer les clefs `ssh-keygen -t ecdsa`. En cas de problème, se référer à cette [page](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_keymanagement).
Par défaut les clefs se trouvent dans le dossier `C:\Users\<Utilisateur>\.ssh` (`/home/<Utilisateur>/.ssh` sous Linux). Le fichier `id_ecdsa` contient la clef **privée** et le fichier `id_ecdsa.pub` contient la clef **publique**.

## OS (Système d'expoitation)

Tout d'abord il faut "flasher" un os sur une carte micro SD. Pour cela on utilise un logiciel spécifique (ex: [Raspberry Pi Imager](https://www.raspberrypi.com/software/)).
Cliquer sur `CHOISIR L'OS` puis sur `Raspberry Pi OS (other)` et enfin `Raspberry Pi OS Lite (64-bit)`.
Sélectionner la carte SD en cliquant sur `CHOISIR LE STOCKAGE`.
Afficher les options avancées `Ctrl+Shift+X`.
Compléter les réglages de la page `Général` et modifier les valeurs par défaut si besoin.
Dans la Page `Services` cocher la case `activer SSH` puis `Authentification via clef publique` et renseigner la clef publique.
Cliquer sur `Enregistrer`
Puis Cliquer sur `Suivant`.
Mettre la carte SD dans le Raspberry Pi puis le démarrer.
La connexion se fait en utilisant la commande `ssh utilisateur@hôte` (ex : `ssh pi@192.168.1.3`). Voir [cette page](../Autres/ip_discovery.md) pour l'obtenetion de l'ip du raspberry.
Par défaut, l'identifiant est `pi` et le mot de passe `raspberry`