# Projet CREACOSM

## Installation

### Git

Ce projet utilise des sous-modules Git pour chercher le contenu d'autres répertoires.
Il doit donc être initialisé un peu différemment d'un projet classique.

Pour le cloner, utilisez la commande suivante :

```bash
git clone --recurse-submodules https://github.com/VincentGonnet/Projet-CREACOSM.git
```

Si vous avez cloné sans l'argument _--recurse-submodules_, faites :

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

Pour voir le flux des logs d'un conteneur, faites :

```bash
docker compose logs -f nomduconteneur
```

Par exemple, pour voir les logs du backend:

```bash
docker compose logs -f backend
```

### Base de données

La base de données inclue dans le Docker sera initialisée et remplie automatiquement au lancement du backend. Elle n'est pas accessible depuis l'extérieur du conteneur et aucune modification manuelle ne doit y être apportée.

## Utilisation

### Routes API

#### Commencer la partie

-   POST : `/start-game` - démarre la partie et vérifie le code du groupe

    -   Le header doit contenir :
        -   `'Content-Type': 'application/json'`
    -   Le body doit contenir :
        -   `'code': '(code)'` avec (code) le numéro de partie rentré par les joueurs
    -   Retourne le code 200 si tout va bien

-   POST : `/get-ingredients` - récupère les ingrédients utilisés pour cette partie

    -   Le header doit contenir :
        -   `'Content-Type': 'application/json'`
    -   Le body doit contenir :
        -   `'group': '(numGroupe)'` avec (numGroupe) le numéro de partie rentré par les joueurs
    -   Retourne une string JSON, contenant une liste d'ingredients
        ```json
        [
            {
                "id": 8,
                "label": "parfum",
                "image": "image-url"
            },
            {
                "id": 1,
                "label": "beurre de karité",
                "image": "image-url"
            }
        ]
        ```

-   POST : `/analyze-ingredient` - analyse un ingrédient et renvoie l'état après le test
    -   Le header doit contenir :
        -   `'Content-Type': 'application/json'`
    -   Le body doit contenir :
        -   `'group': '(numGroupe)'` avec (numGroupe) le numéro de partie rentré par les joueurs
        -   `'ingredientId': '(id)'` avec (id) l'id de l'ingrédient à analyser
        -   `'condition': '(condition)'` avec (condition) soit "temperature", soit "humidite", soit "luminosite"
        -   `'value': '(value)'` avec (value) la valeur à tester
    -   Retourne un texte avec l'état de l'ingrédient après le test. Le résultat de l'analyse sera sauvegardé dans le tableau des découvertes.
-   POST : `/get-discovered-table` - récupère la table des découvertes pour un ingrédient donné
    -   Le header doit contenir :
        -   `'Content-Type': 'application/json'`
    -   Le body doit contenir :
        -   `'group': '(numGroupe)'` avec (numGroupe) le numéro de partie rentré par les joueurs
        -   `'ingredientId': '(id)'` avec (id) l'id de l'ingrédient pour lequel on veut obtenir le tableau des états découverts
    -   Retourne une string JSON, contenant une liste d'objets avec condition (température, humidité ou luminosité), des bornes inf et sup, et un message
        ```json
        [
            {
                "condition": "temperature",
                "lowerBound": 0,
                "upperBound": 50,
                "message": "l'acide hyaluronique est stable"
            },
            {
                "condition": "temperature",
                "lowerBound": -500,
                "upperBound": 0,
                "message": "l'acide hyaluronique est gelé"
            }
        ]
        ```

## Crédits

Ceci est un projet universitaire, développé pendant la L3 MIAGE à l'Université d'Orléans.

Participants :

-   [Esteban Draily](https://github.com/estelar9)
-   [Koffi-Hild Gomado](https://github.com/hild365)
-   [Vincent Gonnet](https://github.com/VincentGonnet)
-   [Arthur Goudal](https://github.com/GOUDALArthur)
