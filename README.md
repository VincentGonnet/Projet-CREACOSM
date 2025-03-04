# Projet CREACOSM

## Installation

### Git

Ce projet utilise des sous-modules Git pour chercher le contenu d'autres répertoires.
Il doit donc être initialisé un peu différemment d'un projet classique.

Pour le cloner, utilisez la commande suivante : 
```bash
git clone --recurse-submodules https://github.com/VincentGonnet/Projet-CREACOSM.git
```
Si vous avez cloné sans l'argument *--recurse-submodules*, faites :
```bash
git submodule update --init --recursive
```

Pour actualiser le projet avec les dernières mises à jour, utilisez la commande suivante :
```bash
git submodule update --remote
```
Cette commande va automatiquement actualiser chaque sous-module présent dans le projet.

Pour plus de détails sur les sous-modules de Git, vous pouvez [lire ce guide](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

### Docker
Une fois le projet sur votre machine, vous pouvez le démarrer en utilisant Docker Compose :
```bash
docker compose up -d --build
```
Les deux sous-modules et la base de donnée seront ainsi initialisés et prêts à l'emploi.
Le site sera disponible sur le port [A DETERMINER] de votre machine.

### Base de données
La base de données inclue dans le Docker sera initialisée et remplie automatiquement au lancement du backend. Elle n'est pas accessible depuis l'extérieur du conteneur et aucune modification manuelle ne doit y être apportée.

## Utilisation

### Routes API

## Crédits

Ceci est un projet universitaire, développé pendant la L3 MIAGE à l'Université d'Orléans.

Participants :
- [Esteban Draily](https://github.com/estelar9)
- [Koffi-Hild Gomado](https://github.com/hild365)
- [Vincent Gonnet](https://github.com/VincentGonnet)
- [Arthur Goudal](https://github.com/GOUDALArthur)