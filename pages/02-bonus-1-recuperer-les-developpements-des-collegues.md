# Bonus 1 : récupérer les développements des collègues durant un long développement

Si mon développement dure plus longtemps que prévu et que la branche distante `develop` évolue rapidement avec les développements de mes collègues, je peux mettre à jour la branche de ma _feature_ en récupérant leurs travaux.

Pour cela, je me place dans ma branche `develop` et je m'assure bien qu'elle soit à jour :
```sh
$ git checkout develop
$ git pull --rebase
```

Puis, je retourne dans la branche de ma _feature_ et je récupère les changements fraichement récupérés de ma branche locale `develop` :
```sh
$ git checkout feature_branch
$ git pull --rebase
$ git merge origin/develop
$ git push
```
