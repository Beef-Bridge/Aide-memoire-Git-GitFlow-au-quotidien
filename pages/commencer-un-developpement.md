# Commencer un développement

## Au début
Je commence par m'assurer que ma branche `develop` est correctement à jour sur mon dépot local :
```sh
$ git pull --rebase
```

Je poursuis en créant une branche depuis `develop` qui me permet d'effectuer mon développement sans perturber cette dernière :
```sh
$ git flow feature start #NOM_FEATURE develop
```

## Durant mon développement
Régulièrement durant cette phase, j'effectue les commandes somme toutes classiques de Git :
```sh
$ git status
$ git add [-A]
$ git commit -m "#mon_message"
...
```

Après mon premier commit, je rends publique ma feature en la poussant sur le depot distant :
```sh
$ git status
$ git flow feature publish #NOM_FEATURE
```

Je reprends le cours de mon développement :
```sh
...
$ git commit -m "#mon_message"
$ git push
$ git pull --rebase
```

## Fin de mon développement
Après la phase de tests et des éventuels retours correctifs, je bascule sur ma branche `develop` afin de s'assurer qu'elle soit toujours à jour :
```sh
$ git checkout develop
$ git pull --rebase
```

Puis je re-bascule sur la branche de ma feature, je m'assure que je n'ai plus rien en attente par rapport à Git et je la cloture :
```sh
$ git checkout #NOM_FEATURE
$ git pull --rebase
$ git flow feature finish #NOM_FEATURE
$ git push
```

Désormais la branche de mon développement se retrouve fusionnée dans la branche `develop` et elle a été automatiquement supprimée.

>Attention : après avoir fermé ma feature, la branche est supprimée donc je suis automatiquement basculé sur ma branche develop.

## Bonus
Si mon développement dure plus longtemps que prévu et que la branche `develop` évolue rapidement avec les développements de mes collègues, je peux mettre à jour la branche de ma feature en récupérant leurs travaux.

Je me place dans ma branche `develop` et je m'assure bien qu'elle soit à jour :
```sh
$ git pull --rebase
```

Je retourne dans la branche de ma feature et récupère les changements de `develop` :
```sh
$ git pull --rebase
$ git merge origin/develop
```