# Configuration de SSH

## Configuration de SSH pour suivres le sujet Born2BeRoot

Entrer dans le dossier suivant `/etc/ssh` et configurer SSH pour suivre le sujet :

```bash
cd /etc/ssh
vim sshd_config
```

## Connexion via SSH depuis une machine distant

SSH est utile pour se connecter sur un serveur distant

Les informations fournis lors de la connexion via SSH sont les suivants :
`username`, `hostname`, `port`, `password`

1. Commande de base

Pour se connecter sur un serveur distant, on utilise la commande suivante :

```bash
ssh user@192.168.122.100 [-p 22]
```

Le `port` par défaut de SSh est le port `22`

2. Connexion SSH (via clé privée) :

- Création d'une clé SSH :

le drapeau `-t` permet de typer notre clé afin d'obtenir un bon niveau de sécurité pour notre machine distant

le drapeau `-C` permet d'écrire un commentaire pour notre clé SSH générer

le drapeau `-f` permet de spécifier le chemin où l'on voudrait stocker notre clé SSh

```bash
ssh-keygen -t ed25519 -C "local.deploy@domain.com" -f ~/.ssh/deployServer
```

Après avoir cliquer sur entrer, il nous demande un mot de passe afin de sécuriser notre clé SSh pour que personne à part le possesseur du mot de passe peut l'utiliser.
Après avoir effectuer les différentes étapes, il a générer `2 fichiers`, ce sont :

`deployServer :` qui est la clé privée que l'on doit garder en local et qui doit être sécurisé

`deployServer.pub :`qui est la clé publique que l'on peut communiquer au machine distant pour qu'il accepte notre connexion

- Copier notre clé `publique` vers la machine distant :

Il y a plusieurs méthodes pour copier le contenu de la clé publique vers la machine distante, mais nous allons utiliser la commande `ssh-copy-id`.

Le drapeau `-i` permet de choisir la clé que l'on souhaite copier, avec son chemin absolu vers la clé SSh que l'on voudrait séléctionner vers l'`adresse SSH` de la machine distante qui a pour exemple ici `192.168.122.100`

```bash
ssh-copy-id -i ~/.ssh/deployServer.pub 192.168.122.100
```

- Connexion avec la clé privé

le drapeau `-i` permet de spécifier le chemin vers le chemin absolu vers le fichier qui contient la `clé privé`

```bash
ssh -i ~/.ssh/deployServer 192.168.122.100
```

3. Connexion via un alias sur SSh :

- Création du fichier de configuration :

Pour configurer la connexion automatique de notre ordinateur vers la machine distant, il nous faut créer un fichier qui s'appelle `config` dans le dossier `~/.ssh`, pour le créer on tape la commande suivante :

```bash
touch ~/.ssh/config
```

- Ajout d'une configuration pour notre machine virtuelle

Voici un exemple de contenu pour notre fichier de configuration

```
Host *
    IgnoreUnknown AddKeysToAgent, UseKeyChain
    AddKeysToAgent yes
    UseKeyChain yes

Host deployServer
    HostName 192.168.122.100
    User hasintsoa
    Port 22
    IdentitiesOnly yes
    IdentityFile ~/.ssh/deployServer
```

Ce code sert à configurer le fonctionnement lors de la connexion via une clé SSH
