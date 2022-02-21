# Commencer un développement

## Au début
Je commence par m'assurer que ma branche `develop` est correctement à jour sur mon dépot local :
```sh
$ git pull --rebase
```

Je poursuis en créant une branche _feature_ depuis `develop` qui me permet d'effectuer mon développement sans perturber cette dernière :
```sh
# Sans l'extension git-flow :
git checkout develop
git checkout -b feature_branch

# Avec l'extension git-flow :
$ git flow feature start feature_branch develop
```

## Durant mon développement
Régulièrement durant cette phase, j'effectue les commandes somme toutes classiques de Git :
```sh
$ git status
$ git add [-A]
$ git commit -m "#mon_message"
...
```

Après mon premier commit, je rends publique ma _feature_ en la poussant sur le depot distant :
```sh
# Avec l'extension git-flow :
$ git flow feature publish feature_branch
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
$ git checkout feature_branch
$ git pull --rebase

# Sans l'extension git-flow :
$ git checkout develop
$ git merge feature_branch

# Avec l'extension git-flow :
$ git flow feature finish feature_branch

$ git push
```

Désormais la branche de mon développement se retrouve fusionnée dans ma branche locale `develop` et elle a été automatiquement supprimée.

>Attention : après avoir fermé ma _feature_, la branche est supprimée donc je suis automatiquement basculé sur ma branche locale `develop`.

## Bonus
Si mon développement dure plus longtemps que prévu et que la branche distante `develop` évolue rapidement avec les développements de mes collègues, je peux mettre à jour la branche de ma _feature_ en récupérant leurs travaux.

Pour cela, je me place dans ma branche `develop` et je m'assure bien qu'elle soit à jour :
```sh
$ git checkout develop
$ git pull --rebase
```

Puis, je retourne dans la branche de ma _feature_ et je récupère les changements fraichement récupérés dans ma branche locale `develop` :
```sh
$ git checkout feature_branch
$ git pull --rebase
$ git merge origin/develop
```

Une fois mon développement terminé, je (réalise une version de livraison)[03-preparer-une-release.md].