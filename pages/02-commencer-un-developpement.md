# Commencer un développement

## Au début
Je commence par m'assurer que ma branche `develop` est correctement à jour sur mon dépot local :
```sh
$ git pull --rebase
```

Je poursuis en créant une branche _feature_ (ex: `feature/users`) depuis ma locale `develop`, qui me permet d'effectuer mon développement sans perturber cette dernière :
```sh
# Sans l'extension git-flow :
git checkout develop
git checkout -b feature/users

# Avec l'extension git-flow :
$ git flow feature start users develop
```

## Durant mon développement
Régulièrement durant cette phase, j'effectue les commandes somme toutes classiques de Git :
```sh
$ git status
$ git add [-A]
$ git commit -m "#mon_message"
...
```

Après mon premier commit, je rends publique ma _feature_ en la poussant sur le dépot distant :
```sh
# Avec l'extension git-flow :
$ git flow feature publish users
```

Je reprends le cours de mon développement :
```sh
...
$ git commit -m "#mon_message"
$ git push
$ git pull --rebase
...
```

## Fin de mon développement
Après la phase de tests et des éventuels retours correctifs, je bascule sur ma branche locale `develop` afin de m'assurer qu'elle soit toujours à jour :
```sh
$ git checkout develop
$ git pull --rebase
```

Puis je re-bascule sur la branche de ma _feature_, et je m'assure que je n'ai plus rien en attente par rapport à Git, puis je la cloture (sans oublier de pousser tout ça) :
```sh
$ git checkout feature/users
$ git pull --rebase

# Sans l'extension git-flow :
$ git checkout develop
$ git merge feature/users

# Avec l'extension git-flow :
$ git flow feature finish users

$ git push
```

Désormais la branche de mon développement se retrouve fusionnée dans ma branche locale `develop` et elle a été automatiquement supprimée.

>Attention : après avoir fermé ma _feature_, la branche est supprimée donc je suis automatiquement basculé sur ma branche locale `develop`.

Une fois mon développement terminé, je [réalise une version de livraison](03-preparer-une-release.md).

## Bonus
* [Récupérer les développements des collègues durant un long développement](02-bonus-1-recuperer-les-developpements-des-collegues.md)
