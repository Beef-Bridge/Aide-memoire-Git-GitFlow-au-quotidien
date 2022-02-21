# Préparer une release

## Principe

Une fois que ma branche `develop` a acquis assez de fonctionnalités en vue d'une livraison (ou qu'une date de livraison prédéfinie approche), je créée une branche de livraison (_release_) à partir de `develop`.

La création de cette branche marque le début du cycle de livraison suivant : 
* **aucune fonctionnalité supplémentaire ne pourra être ajoutée**
* **cette branche sera uniquement dédiée aux corrections de bugs, à la génération de documentation et à d'autres tâches axées sur la livraison.**

Une fois qu'elle est prête, la branche `release` est mergée dans la branche `master`, mais aussi dans la branche `develop`, qui a certainement progressé depuis le début de la livraison.

## Utilisation

1. La création de la branche de livraison est basée sur la branche `develop` (comme pour une _feature_). Je crée la branche de la release de la manière suivante :
```sh
# Sans l'extension git-flow :
$ git checkout develop
$ git checkout -b release/1.2.3

# Avec l'extension git-flow :
$ git flow release start 1.2.3
Switched to a new branch 'release/1.2.3'
```

2. Dans l'éventualité où des collègues veulent/peuvent participer à la finalisation de la _release_, je la publie :
```sh
# Avec l'extension git-flow :
$ git flow release publish 1.2.3
```

3. Je continue d'ajouter/corriger les éléments prévus pour la livraison correspondante à la présente _release_.

4. Une fois la livraison prête, je clôture cette branche dans ma branche locale `master` :
```sh
# Sans les extensions git-flow :
$ git checkout master
$ git merge release/1.2.3

# Avec les extensions git-flow :
$ git flow release finish '1.2.3'
```

5. Une fois fermée, je reviens  sur ma branche locale `master` (qui contient la release)  et je pousse cette branche sur le dépot distant :
```sh
$ git checkout master
$ git push
```

6. Puis je bascule sur ma branche locale `develop` (qui contient aussi la release) eet de la même manière, je pousse cette branche aussi sur le dépot distant :
```sh
$ git checkout develop
$ git push
```

7. Depuis l'interface Git/Gitlab, je contrôle :
   * que la branche de la release n'existe plus
   * que les commits de la release apparaissent dans la branche `develop`
   * que les commits de la release apparaissent dans la branche `master`

8. Pour finir, je [créé le tag de la version que je dois livrer](04-creer-un-tag-de-livraison.md).