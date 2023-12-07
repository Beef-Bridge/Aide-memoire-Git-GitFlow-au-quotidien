# Préparer une release

[[_TOC_]]

## Principe

Une fois que ma branche `develop` a acquis assez de fonctionnalités en vue d'une livraison (ou qu'une date de livraison prédéfinie approche), je créé une branche de livraison (_release_) à partir de `develop`.

La création de cette branche marque le début du cycle de livraison suivant : 
* **aucune fonctionnalité supplémentaire ne pourra être ajoutée**
* **cette branche sera uniquement dédiée aux corrections de bugs, à la génération de documentation et à d'autres tâches axées sur la livraison.**

Une fois qu'elle est prête, la branche `release` est mergée dans la branche `<master|main>`, mais aussi dans la branche `develop`, qui a certainement progressé depuis le début de la livraison.

## Procédure

### Avec Git

1. Je créé la branche de la _release_ à partir de la branche `develop` (comme pour une _feature_) :
```sh
$ git checkout develop
$ git pull --rebase
$ git checkout -b release/1.2.3
```

2. Dans l'éventualité où des collègues veulent/peuvent participer à la finalisation de la _release_, je la publie :
```sh
$ git commit --allow-empty -m "Release v1.2.3"
$ git push --set-upstream origin release/1.2.3
```

3. Je continue d'ajouter/corriger les éléments prévus pour la livraison correspondante à la présente _release_.

4. Une fois la branche prête, je combine cette branche avec ma branche locale `<master|main>` :
```sh
$ git checkout <master|main>
$ git pull --rebase
$ git merge --no-ff -m "Merge branch 'release/1.2.3'" release/1.2.3
```

>**Note** : Il se peut que certains conflits surviennent à la suite de ce _merge_, dans ce cas je les résouds et je termine le _merge_ avec la commande : 
>
>```sh
>$ git merge --continue
>```

5. Je pousse le résultat sur la branche `<master|main>` distante :
```sh
$ git push -u origin <master|main>
```

>**Important : Maintenant la _release_ est contenue dans la branche `<master|main>` de mon dépôt distant !**

6. Je bascule sur ma branche `develop` et la prépare à recevoir le résulat du _merge_ avec la branche `<master|main>`, en m'assurant qu'elle soit bien à jour :
```sh
$ git checkout develop
$ git pull --rebase
```

7. Je m'assure une dernière fois que je suis bien sur ma branche locale `develop` :
```sh
$ git branch --show-current
develop
```

8. Je _merge_ ma branche `<master|main>` dans ma branche `develop` :
```sh
$ git merge <master|main>
```

9. Je pousse le résultat de cette action sur la branche `develop` distante :
```sh
$ git push -u origin develop
```

>**Important : Maintenant la _release_ est contenue dans la branche `develop` de mon dépôt distant !**

10. Je peux clôturer cette _release_ en la supprimant du dépôt distant :
```sh
$ git push origin --delete release/1.2.3
```

11. Je la supprime également de mon dépôt local :
```sh
$ git branch -d release/1.2.3
```

12. Depuis l'interface Github/Gitlab, je contrôle :
   * que la branche de la _release_ n'existe plus
   * que les _commit_ de la _release_ apparaissent dans la branche `develop`
   * que les _commit_ de la _release_ apparaissent dans la branche `<master|main>`


### Avec Gitflow

1. Je créé la branche de la _release_ de la manière suivante :
```sh
$ git checkout develop
$ git flow release start 1.2.3
Switched to a new branch 'release/1.2.3'
```

2. Je la publie de suite dans l'éventualité où des collègues veulent/peuvent participer à sa finalisation :
```sh
$ git flow release publish 1.2.3
```

3. Des ajouts/correctifs viennent enrichir la _release_.

4. Une fois prête, je clôture cette branche dans ma branche locale `<master|main>` :
```sh
$ git flow release finish '1.2.3'
```

5. Une fois fermée, je reviens sur ma branche locale `<master|main>` (qui contient la _release_) et je pousse cette branche sur le dépot distant :
```sh
$ git push
```

6. Puis je bascule sur ma branche locale `develop` (qui contient aussi la _release_) et de la même manière, je pousse cette branche aussi sur le dépot distant :
```sh
$ git checkou develop
$ git push
```

7. Je contrôle le résultat depuis l'interface Github/Gitlab.

## La suite

Il reste à [créer le tag de la version](04-creer-un-tag-de-livraison.md) que je dois livrer.