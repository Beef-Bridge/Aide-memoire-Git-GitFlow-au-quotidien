# Récupérer les développements des collègues durant un long développement

Si mon développement dure plus longtemps que prévu et que la branche distante `develop` évolue rapidement avec les développements de mes collègues, je peux mettre à jour la branche de ma _feature_ en récupérant leurs travaux.

Pour cela, je me place dans la branche `develop` de mon projet et je m'assure bien qu'elle soit à jour :
```sh
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > develop ✔
$ git checkout develop
$ git pull --rebase
```

Puis, je retourne dans la branche de ma _feature_ et je récupère les changements fraichement récupérés de ma branche locale `develop` :
```sh
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_branch ✘ ✹ ✭
$ git checkout feature_branch
$ git pull --rebase
$ git merge origin/develop
$ git push
```

## Régler un probleme 'Merging'
Si lors du `merge` un problème survient (pour diverses raisons), il faut -au choix- appliquer l'une des commandes suivantes :
```sh
mon-poste:bibi$ /Users/bibi/Workspaces/projets/mon-projet > feature_branch ✘ ✹ ✭ | MERGING

# continuer le processus de merge et valider le message du commit
$ git merge --continue

# ou modifier/corriger le message du commit relatif à ce merge
$ git commit -m "message de commit du merge à appliquer sur ma branche feature_branch"

# ou, alors annuler le merge
$ git merge --abort
```
