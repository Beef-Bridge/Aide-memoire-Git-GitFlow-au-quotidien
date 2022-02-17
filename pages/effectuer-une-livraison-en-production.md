# Effectuer une livraison en production

1. S'assurer que la branche locale `develop` est bien à jour :
```sh
$ git checkout develop # si nécéssaire
$ git pull --rebase
```

2. S'assurer que la branche locale `master` est bien à jour, elle aussi :
```sh
$ git checkout master # si nécéssaire
$ git pull --rebase
```

3. S'assurer que la branche locale de la `release` en question est bien à jour :
```sh
$ git checkout #MA_RELEASE # si nécéssaire
$ git pull --rebase
```

4. Clôturer la release :
```sh
$ git flow release finish #NOM_RELEASE
```

Après la clôture de la branche `release`, je suis replacé sur ma branche locale `develop`.

Le merge est envoyé dans les branches locales `develop` et `master`. **Il est donc impératif de les publier vers leur dépot distant correspondant !**

5. Publier le merge de la `release` vers la branche `develop` du dépot distant : 
m'assurer que je suis bien sur la branche locale `develop` !

```sh
$ git checkout develop # si nécéssaire
$ git push
```

6. Publier le merge de la `release` vers la branche `master` du dépot distant :
```sh
$ git checkout master
$ git push
```

7. Contrôler sur Github/Gitlab plusieurs points :
   * la branche de la release n'existe plus
   * les commits de la release apparaissent dans l'historique de la branche `develop`
   * les commits de la release apparaissent dans l'historique de la branche `master`

8. Il reste à créer le tag correspondant au numéro de version que l'on souhaite publier sur notre environnement de production.

9. Effectuer la livraison du package de ce tag.